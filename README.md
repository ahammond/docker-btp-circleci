Docker Build Tag Push using CircleCI
===

Build Tag Push is an idiom we follow at AnchorFree.

Summary
---

We lock naming of containers down to "$github_orgname/$github_reponame".
For reponames that start with "docker-" we strip that prefix.
The container is tagged with the branch name associated with it at the time of build.
When a branch or a tag is added to a SHA after the container has been built,
the image is fetched from dockerhub using the SHA tag, rather than being rebuilt.
This adheres to the "Build Binaries Only Once" CI best practice.
Docker tags are then applied to match git tags and pushed back to dockerhub.
The master branch from git is mapped to the latest tag in docker.

Usage
---

Configure a context which provides the following env vars.

```bash
DOCKER_USER  (optional, defaults to CIRCLE_USERNAME)
DOCKER_PASS  (the dockerhub password associated with the user)
```

Copy `.circleci/config` to your repo.
Add integration tests as appropriate.
If your container has shell scripts, re-enable the shellcheck job.
