# Node.js Demo App

A simple Node.js Express application styled with Tailwind CSS.

## Features

- Express server running on port 3000
- Static frontend files from `public/`
- `/api/status` endpoint
- Tailwind CSS build script
- Docker container support
- GitHub Actions CI/CD pipeline

## Local Setup

```bash
npm ci
npm run build:css
npm start
```

Open http://localhost:3000

## Testing

Run the syntax check with:

```bash
npm test
```

## Docker

Build and run the application:

```bash
docker build -t node-demo-app .
docker run -p 3000:3000 node-demo-app
```

The application will be available at http://localhost:3000.

## CI/CD Pipeline

The GitHub Actions workflow in `.github/workflows/main.yml`:

1. Installs dependencies.
2. Runs `npm test`.
3. Builds the Docker image.
4. Pushes the image to Docker Hub using both `latest` and the commit SHA tags.

Required GitHub Actions secrets:

- `DOCKERHUB_USERNAME`
- `DOCKERHUB_TOKEN`

The Docker Hub token must have Read and Write permissions.

## Problems Faced and Solutions

### Missing test script

The workflow initially failed because `package.json` did not contain a `test` script.

**Solution:** Added:

```json
"test": "node --check server.js"
```

### Docker Hub authorization error

The Docker image built successfully, but pushing it initially failed with a 401 Unauthorized error.

**Solution:** Created a Docker Hub access token with Read and Write permissions and saved it as `DOCKERHUB_TOKEN` in GitHub repository secrets.