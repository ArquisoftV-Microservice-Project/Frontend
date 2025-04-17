# Vue Frontend with GCP Image Build & Deployment

This repository contains a frontend application built with Vue.js. It includes a GitHub Actions workflow that builds a Docker image and automatically deploys it to a Google Kubernetes Engine (GKE) cluster whenever there is a push to the `main` branch, which is protected to prevent direct commits and enforce pull requests.

---

## 🚀 CI/CD Workflow

The `.github/workflows/build.yml` file defines a GitHub Action that performs the following steps:

1. **Checkout the code**: Retrieves the source code from the `main` branch.
2. **Authenticate with GCP**: Uses a service account (`GCP_SA_CREDENTIALS`) to authenticate with Google Cloud.
3. **Set up GCP SDK**: Installs and configures the `gcloud` CLI.
4. **Configure Docker with Artifact Registry**: Allows Docker to push images to GCP’s container registry.
5. **Get GKE credentials**: Connects to the GKE cluster to run `kubectl` commands.
6. **Set image tag**: Generates a unique image tag per commit using the branch name and timestamp.
7. **Build Docker image**: Builds and tags the Docker image with both the generated tag and `latest`.
8. **Push the image**: Pushes both `latest` and timestamped tags to GCP's Artifact Registry.
9. **Update deployment on GKE**: If a deployment named `frontend` exists, it updates the container image for `frontend-container`.

---

## 📁 Project Structure

```
.
├── src/                 # Frontend source code (Vue.js)
├── build/               # Webpack config and build utilities
├── config/              # Environment configurations (dev/prod)
├── Dockerfile           # Docker image used in the pipeline
└── .github/workflows/   # GitHub Actions workflows
```

---

## 🛠️ Requirements

To make the workflow run successfully, you need to set up the following in your GitHub repository:

### 🔐 Secrets

- `GCP_SA_CREDENTIALS`: JSON with credentials for a service account that has permissions for:
  - Artifact Registry
  - GKE (get-credentials and set image)
- `GCP_PROJECT`: Google Cloud project ID
- `GKE_CLUSTER`: Name of your GKE cluster

### ⚙️ Variables

- `GCP_ZONE`: Zone where the cluster is located (e.g. `us-central1`)
- `REGISTRY`: Artifact Registry repository name (e.g. `my-registry`)
- `IMAGE_NAME`: Name of the image to be built (e.g. `frontend`)

---

## 🐳 Docker

This project includes a `Dockerfile` that packages the Vue.js app for production. Make sure the Dockerfile is properly configured for your production environment.

---

## 🖥️ Local Development

UI for sample distributed TODO application.

## Configuration

- `PORT` - a port the application binds to
- `AUTH_API_ADDRESS` - address of `auth-api` for authentication
- `TODOS_API_ADDRESS` - address of `todos-api` for TODO CRUD

## Building

```bash
# install dependencies
npm install

# build application
npm run build
```

## Running

```bash
PORT=8080 AUTH_API_ADDRESS=http://127.0.0.1:8000 TODOS_API_ADDRESS=http://127.0.0.1:8082 npm start
```

## Dependencies

Here you can find the software required to run this microservice, as well as the version we have tested.
| Dependency | Version |
|-------------|----------|
| Node | 8.17.0 |
| NPM | 6.13.4 |
