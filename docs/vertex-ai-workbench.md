# Vertex AI Workbench

Vertex AI Workbench is a single development environment used for the entire data science workflow. To set up an end-to-end notebook-based production environment, create JupyterLab instance notebook instances that come with built-in integrations.

## Table of Content
- [Prerequisite](#prerequisite)
- [IAM](#iam)
- [Create a JupyterLab instance](#create-a-jupyterlab-instance)
- [Open a JupyterLab notebook](#open-a-jupyterlab-notebook)
- [Share a JupyterLab notebook](#share-a-jupyterlab-notebook)
- [Known Issues](#known-issues)
- [References](#references)

## Prerequisite
- Valid project with IAM permissions

## IAM
- **Workbench Notebooks Admin**: Create and manage notebooks
- **Workbench Notebooks Viewer**: View notebooks

## Create a JupyterLab instance
1. If you aren't signed in to the GDC console, sign in using the steps in Sign in to the GDC console.
2. In the navigation pane, expand Vertex AI, and click Workbench.
3. Click Create Notebook.
4. For Notebook name, type a name for your JupyterLab instance. Vertex AI uses the name you choose to create a URL for accessing your notebook.
5. From Environment, select a Docker image for your JupyterLab instance.
6. From Cluster, select a cluster for your JupyterLab instance. If a cluster isn't available, work with your Platform Administrator (PA) to add one or more clusters.
7. In CPUs / Memory, choose how many CPUs and how many GBs of RAM you want. For CPU-intensive workloads, you can choose more than one CPU.
8. From GPUs, select how many GPUs you want. In Vertex AI Workbench, a GPU is one NVIDIA Multi-Instance GPU (MIG) slice of an A100 Tensor Core GPU. For more information about MIGs, refer to https://www.nvidia.com/en-us/technologies/multi-instance-gpu in Nvidia's documentation.
9. In Workspace volume, choose the size of your volume in GBs.
10. Click Create.

## Open a JupyterLab notebook
If you know the URL for your JupyterLab notebook, open your JupyterLab notebook by typing its URL into a web browser. You can bookmark the URL to quickly open it in the future.

If you don't know the URL for your JupyterLab notebook, use the GDC console to open it:

1. If you aren't signed in to the GDC console, sign in using the steps in Sign in to the GDC console.
2. In the navigation pane, expand Vertex AI, and click Workbench.
3. Find the JupyterLab instance you want to open, and click its Open JupyterLab link.
4. If you are prompted to authenticate, follow the authentication steps for your identity provider.
5. In the JupyterLab instance, open or create a JupyterLab notebook.

## Share a JupyterLab notebook
To share a JupyterLab notebook, do the following:
1. Get the URL for the JupyterLab notebook. To locate the URL, follow the steps in Open a JupyterLab notebook, and make a note of its URL.
2. Confirm the person you want to share the JupyterLab notebook with is bound to the Workbench Notebooks Viewer role. For more information, see Grant IAM permission to open a JupyterLab notebook.
3. Share the URL of the JupyterLab notebook with the person you want to open the JupyterLab notebook.

## Known Issues
If you encountered 404: Not Found error when opening a JupyterLab notebook, please remove [/lab]() from the URL in the browser.

## References
- [Create a notebook](https://cloud.google.com/distributed-cloud/hosted/docs/latest/gdch/application/ao-user/vertex-ai-workbench)
- [Back up and restore notebook data](https://cloud.google.com/distributed-cloud/hosted/docs/latest/gdch/application/ao-user/backup-restore-notebook-data)

---
[Top](#) | [Home](/README.md)