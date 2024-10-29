# Vertex AI pre-trained APIs - OCR Example

## Table of Content
- [Prerequisite](#prerequisite)
- [IAM](#iam)
- [Generate the trust bundle CA certificate file in a development environment](#generate-the-trust-bundle-ca-certificate-file-in-a-development-environment)
- [Setup service accounts](#setup-service-accounts)
- [Detect text in images using Vertex AI Workbench](#detect-text-in-images-using-vertex-ai-workbench)
- [Known Issues](#known-issues)
- [References](#references)

## Prerequisite
- Valid project with IAM permissions
- [Enable pre-trained APIs](/docs/vertex-ai-pretained-api.md)
- [Vertex AI Workbench in the project](/docs/vertex-ai-workbench.md)

## IAM
- **Project IAM Admin** (project-iam-admin: To create service account
- **AI OCR Developer** (ai-ocr-developer): OCR developer 
- **AI Speech Developer** (ai-speech-developer): Speech-to-Text developer 
- **AI Translation Developer** (ai-translation-developer): Translation developer 

## Generate the trust bundle CA certificate file in a development environment
If you are using a development environment, follow these steps to generate the trust bundle certificate authority (CA) certificate file:
```bash
curl -k https://<console url>/.well-known/login-config | grep
certificateAuthorityData | head -1 | cut -d : -f 2 | awk '{print $1}' | sed 's/"//g' | base64
--decode > trusted_certs.crt
```

Replace <console url> with your GDC air-gapped organization console url, e.g. console.org-1.acme.com


## Setup service accounts
Service accounts, also referred to as service identities, play a crucial role in managing your Vertex AI services. They are the accounts that your workloads use to access Vertex AI services and make authorized API calls programmatically. For example, service accounts can manage your Vertex AI Workbench notebook to transcribe audio files using the Speech-to-Text API. Similar to a user account, service accounts can be granted permissions and roles, providing a secure and controlled environment, but they can't sign in like a human user.

1. Ensure you have permission Project IAM Admin (project-iam-admin) role to create the service account
2. Login to GDC air-gapped CLI
3. Create a service account:
```bash
gdcloud iam service-accounts create <SERVICE_ACCOUNT> --project=<PROJECT_ID>
```
Replace the following:

- SERVICE_ACCOUNT: the name of the service account. The name must be unique within the project namespace.
- PROJECT_ID: the project ID where you want to create the service account. If gdcloud init is already set, then you can omit the --project flag.

4. Create the application default credentials JSON file and the public and private key pairs:
```bash
gdcloud iam service-accounts keys create APPLICATION_DEFAULT_CREDENTIALS_FILENAME \
    --project=PROJECT_ID \
    --iam-account=SERVICE_ACCOUNT \
    --ca-cert-path=CA_CERTIFICATE_PATH
```
Replace the following:

- APPLICATION_DEFAULT_CREDENTIALS_FILENAME: the name of the JSON file, for example, my-service-key.json.
- PROJECT_ID: the project to create the key for.
- SERVICE_ACCOUNT: the name of the service account to add the key for.
- CA_CERTIFICATE_PATH: an optional flag for the path to the certificate authority (CA) certificate that verifies the authentication endpoint. If you don't specify this path, the system CA certificates are used. You must install the CA in the system CA certificates.

Distributed Cloud adds the public key to the service account keys you use to verify the JSON web tokens (JWT) the private key signs. The private key is written to the application default credentials JSON file.

5. Grant the service account access to project resources by assigning a role binding. The name of the role depends on the Vertex AI service you want to use the service account for.

```bash
gdcloud iam service-accounts add-iam-policy-binding \
    --project=PROJECT_ID \
    --iam-account=SERVICE_ACCOUNT \
    --role=ROLE
```
Replace the following:

- PROJECT_ID: the project to create the role binding in.
- SERVICE_ACCOUNT: the name of the service account to use.
- ROLE: the predefined role to assign to the service account. Specify roles in the format role/name where role is the Kubernetes type, such as Roleor ProjectRole, and name is the name of the predefined role. For example, the following are roles that you can assign to service accounts to use Vertex AI pre-trained APIs:

    - To assign the AI OCR Developer (ai-ocr-developer) role, set the role torole/ai-ocr-developer.
    - To assign the AI Speech Developer (ai-speech-developer) role, set the role torole/ai-speech-developer.
    - To assign the AI Translation Developer (ai-translation-developer) role, set the role torole/ai-translation-developer.


## Detect text in images using Vertex AI Workbench
This example will use the created service account, trusted bundle and the Vertex AI Workbench notebook to test the OCR API endpoint.

1. Open the JupyterLab notebook
2. Upload the file [vertexai-setup.ipynb](/notebooks/vertexai-setup.ipynb) 
3. Upload the file [vertexai-pretrained-ocr.ipynb](/notebooks/vertexai-pretrained-ocr.ipynb)
4. Open vertexai-setup.ipynb and run all cells to install all the client libraries. Make sure you have updated the correct console url in the notebook.
5. Open vertexai-pretrained-ocr.ipynb and run all cells

## Known Issues
In the older version for getting the credentials, you will need to add the following to bypass the SSL certifcate verification:

```python
        sesh.verify = False #didn't work for 1.12.4
        creds._ca_cert_path = False #need to set the following to work
```

## References
- [Setup a project for Vertex AI](https://cloud.devsite.corp.google.com/distributed-cloud/hosted/docs/latest/gdch/application/ao-user/vertex-ai-set-up-project)
- [Detect text in images](https://cloud.devsite.corp.google.com/distributed-cloud/hosted/docs/latest/gdch/application/ao-user/vertex-ai-ocr)
- [Transcribe audio](https://cloud.devsite.corp.google.com/distributed-cloud/hosted/docs/latest/gdch/application/ao-user/vertex-ai-stt)
- [Translate a language into another language](https://cloud.devsite.corp.google.com/distributed-cloud/hosted/docs/latest/gdch/application/ao-user/vertex-ai-translation)

---
[Top](#) | [Home](/README.md) | [Vertex AI pre-trained APIs](/docs/vertex-ai-pretained-api.md)
