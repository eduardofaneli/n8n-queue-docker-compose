# Custom n8n Worker

## Context
In environments like Azure Container Apps, it is not possible to set the entrypoint correctly to run n8n in worker mode using the official image (`n8nio/n8n:latest`). This can result in errors such as:

```
Error: Command "worker" not found
```

## Solution
The `custom-worker` folder contains a `Dockerfile` that forces the entrypoint and command so the container always runs n8n as a worker:

```dockerfile
FROM n8nio/n8n:latest
ENTRYPOINT ["n8n"]
CMD ["worker"]
```

## How to use
1. Build the custom image:
   ```sh
   docker build -t n8n-custom-worker ./custom-worker
   ```
2. Push the image to your registry (e.g., Azure Container Registry).
3. Use this image in Azure Container Apps or any environment where you cannot set the entrypoint properly.

## Advantages
- Ensures n8n worker runs correctly regardless of platform or panel limitations.
- Avoids command not found errors.
- Allows scaling workers in cloud environments without manual tweaks.

---

If you need examples for Docker Compose or Azure, add them as needed.