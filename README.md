# Group Spring Boot Project

An initial group application built with Java 17 and Spring Boot, ready to deploy on Render.

## Run locally

Install Java 17 or newer. Maven is included through the Maven Wrapper.

Windows PowerShell:

```powershell
.\mvnw.cmd spring-boot:run
```

macOS / Linux:

```bash
./mvnw spring-boot:run
```

Open http://localhost:8080.

| Path | Purpose |
| --- | --- |
| `/` | Welcome page |
| `/api/hello` | Example JSON endpoint |
| `/actuator/health` | Health check used by Render |

## Build and test

```powershell
.\mvnw.cmd --batch-mode --no-transfer-progress verify
```

On macOS / Linux, replace `.\mvnw.cmd` with `./mvnw`.

## Deploy on Render

1. Connect the repository owner's GitHub account to Render.
2. Create a new **Blueprint** and select this repository and its `main` branch.
3. Render reads `render.yaml`, builds the `Dockerfile`, and creates a free web service.
4. Open the service's assigned `https://...onrender.com` URL after the deploy succeeds.

The application listens on Render's `PORT` environment variable. Render checks `/actuator/health` before routing traffic. Automatic deployment is configured to follow successful GitHub checks on `main`.

Keep the service connected through GitHub so automatic deployment is available. Commit and push every deployed change; use GitHub as the source for all Render releases.

Free services can sleep when idle, so their first request may take longer.

## Group collaboration

The repository owner should add each member under **Settings > Collaborators > Add people**. Each member must accept the invitation to receive push access.

Each member should use their own GitHub account and Git identity:

```bash
git config user.name "Your name"
git config user.email "Your GitHub-verified email or GitHub noreply email"
git switch -c feature/short-description
# Make and test your changes.
git add .
git commit -m "Describe the change"
git push -u origin feature/short-description
```

Open a pull request into `main`, review it with your group, and merge after checks pass. Preserve contributors' actual commits and authorship when merging. The group’s commits and review activity document individual contributions.

## Deployment references

- [Render Blueprint reference](https://render.com/docs/blueprint-spec)
- [Render automatic deployments](https://render.com/docs/deploys)
- [Render Docker deployments](https://render.com/docs/docker)
