# Firebase Function Save Payload - Deployment

This repo deploys the [`savePayload`](https://github.com/TechArtists/backend-firebase-function-save-payload) Firebase Cloud Function to our projects using a reusable GitHub Actions workflow from the upstream repo.

## How It Works

The [deploy workflow](.github/workflows/deploy.yml) calls the reusable workflow from [TechArtists/backend-firebase-function-save-payload](https://github.com/TechArtists/backend-firebase-function-save-payload) to deploy the `savePayload` function across multiple Firebase projects.

## Deploying

1. Go to the **Actions** tab in this repository
2. Select **Deploy Firebase Functions**
3. Click **Run workflow**

The function will be deployed to all configured projects in parallel.

## Adding a New Project

1. Run the setup script to configure permissions:

   ```bash
   ./scripts/setup-project-permissions.sh <PROJECT_ID>

   # Or with bucket permissions in one go:
   ./scripts/setup-project-permissions.sh <PROJECT_ID> firebase-function-deploy@appex-data-imports.iam.gserviceaccount.com <BUCKET_PROJECT> <BUCKET_NAME>
   ```

   See [scripts/README.md](scripts/README.md) for full documentation.

2. Add the project ID to the `projects` list in [.github/workflows/deploy.yml](.github/workflows/deploy.yml)

## Prerequisites

- A `GCP_SA_KEY` GitHub secret with the service account key (already configured)
- Target projects must have the required IAM permissions and APIs enabled — see the [upstream README](https://github.com/TechArtists/backend-firebase-function-save-payload#readme) for details

## Project Structure

```
.github/workflows/deploy.yml   # Calls the upstream reusable workflow
scripts/                        # Project setup/permissions scripts
```
