# Vertex AI pre-trained APIs

Vertex AI on Distributed Cloud includes three APIs, one for each of its pre-trained models, which are Optical Character Recognition (OCR), Speech-to-Text, and Translation. To learn more about these pre-trained models, see the following documentation:

- Optical Character Recognition (OCR): Detect text in images.
- Speech-to-Text: Transcribe audio.
- Translation: Translate a language into another language.

## Table of Content
- [Prerequisite](#prerequisite)
- [IAM](#iam)
- [Enable pre-trained APIs](#enable-pre-trained-apis)
- [Disable pre-trained APIs](#disable-pre-trained-apis)
- [View service status and endpoints](#view-service-status-and-endpoints)
- [Known Issues](#known-issues)
- [References](#references)

## Prerequisite
- Valid project with IAM permissions

## IAM
- **AI Platform Admin** (ai-platform-admin): Manage Vertex AI pre-trained APIs

## Enable pre-trained APIs
You can enable the OCR, Speech-to-Text, and Translation pre-trained APIs using the GDC console.

1. Sign in to the GDC console.
2. On the navigation menu, click Vertex AI > Pre-trained APIs.
3. On the Pre-trained APIs page, perform one of the following actions:

- Click Enable all APIs to enable all the pre-trained APIs.
- Click Enable on a specific service to enable that API.
- Note: The GDC console doesn't display the buttons to enable the pre-trained APIs if you don't have the correct permissions.
4. In the confirmation dialog, click Enable. A progress message displays.

The enablement duration varies. It might take between 15 and 45 minutes to finish, depending on the state of the cluster.

## Disable pre-trained APIs
You can disable the OCR, Speech-to-Text, and Translation pre-trained APIs using the GDC console.

1. Sign in to the GDC console.
2. On the navigation menu, click Vertex AI > Pre-trained APIs.
3. On the Pre-trained APIs page, perform one of the following actions:

- Click Disable all APIs to disable all the pre-trained APIs.
- Click Disable on a specific service to disable that API.
- Note: The GDC console doesn't display the buttons to disable the pre-trained APIs if you don't have the correct permissions.
4. In the confirmation dialog, enter disable in the text field to confirm that you want to take that action. Then, click Disable. A progress message displays.

## View service status and endpoints 
You use pre-trained API endpoints to interact with Vertex AI services programmatically. For example, you need the endpoint when using a Vertex AI pre-trained model in a JupyterLab notebook or interacting with a pre-trained API from the command-line interface.

Follow these steps to view the status and endpoints of the Optical Character Recognition (OCR), Speech-to-Text, and Translation pre-trained APIs:

1. Sign in to the GDC console.
2. On the navigation menu, click Vertex AI > Pre-trained APIs.
3. On the Pre-trained APIs page, you can review the following information:

- View the status of each pre-trained API on the central panel. The status is either Enabled or Not enabled. If the status is Not enabled, you can enable the corresponding API. For more information, see Provision GPUs and enable Vertex AI pre-trained APIs.

- If the status of an API is Enabled, you can view its endpoint on the central panel. To use this endpoint for programmatically interacting with the Vertex AI service, click content_copy Copy to copy it to your clipboard.


## Known Issues
N/A

## References
- [Enable and Disable pre-trained APIs](https://cloud.google.com/distributed-cloud/hosted/docs/latest/gdch/application/ao-user/vertex-ai-enable-pre-trained-apis#before-you-enable-apis)
- [View service status and endpoints](https://cloud.google.com/distributed-cloud/hosted/docs/latest/gdch/application/ao-user/vertex-ai-api-status)

---
[Top](#) | [Home](/README.md) | [OCR](/docs/vertex-ai-pretained-ocr.md) | [Speech-to-Text](/docs/vertex-ai-pretained-stt.md) | [Translation](/docs/vertex-ai-pretained-translate.md)
