## Dockerfile Best Practices

This is a summary from [Dockerfile Best Practices](https://www.youtube.com/watch?v=t2cDtDrNqc8)

- Enable Buildkit
- `# syntax = docker/dockerfile:1.0-experimental`
- Take care of order, order matters for caching (COPY at the end)
- More specific COPY to limit cache bust
- Use COPY, not ADD for local files
- Line buddies: apt-get update & install
- Remove innecessary dependencies
- Use apt-get install —no-install-recommends
- Reuse official images when possible
- Look for minimal flavors
- WORKDIR
- Multistage builds
- `docker build —target X`
- Context mounts
- Application cache
