
## Who it’s for
Anyone who wants a simple, secure way to call a **Google Cloud Run** endpoint from n8n—without exposing it publicly. 

People who want a cheap/free-tier way to run custom API logic without hosting n8n or spinning up servers. Example: you’ve got scraping code that needs specific system/python libs—build it into a Dockerfile on Cloud Run, then call it as a secure endpoint from n8n.


## How it works
This is a **conjunctive workflow**: the main workflow calls **Service Auth (sub-workflow)** to get a Google **ID token**, merges that auth with your context, then calls your Cloud Run URL with `Authorization: Bearer &lt;id_token&gt;`. Works great for single calls or looping over items.

## How to set up

General instructions below—see my detailed guide for more info: 

**[Build a Secure Google Cloud Run API, Then Call It from n8n (Free Tier)](https://medium.com/@marcocodes/build-a-secure-google-cloud-run-api-then-call-it-from-n8n-88c03291a95f)**

Setup:
1. Create a Cloud Run service and enable **Require authentication (Cloud IAM)**.
2. Create a Google **Service Account** and grant **Cloud Run Invoker** on that service.
3. In n8n, import the workflows and update the **Vars** node (`service_url`, optional `service_path`).
4. Create a **JWT (PEM)** credential from your service account key, then run.
5. Make sure to read the **sticky notes** in the workflows—they contain helpful pointers and optional configurations.

## Requirements
- Cloud Run service URL (auth required)  
- Google Service Account with **Cloud Run Invoker**  
- Private key JSON fields downloaded from Service Account | needed to generate JWT credentials

## How to customize
Change the HTTP method/path/body in **Cloud Run Request**, or drop the **Service Auth (sub-workflow)** into other workflows to reuse the same auth pattern.

## More details
Full write-up (minimal + modular flows), screenshots, and more:  

**[Build a Secure Google Cloud Run API, Then Call It from n8n (Free Tier)](https://medium.com/@marcocodes/build-a-secure-google-cloud-run-api-then-call-it-from-n8n-88c03291a95f)** 
— by Marco Cassar