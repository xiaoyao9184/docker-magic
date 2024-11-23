# Docker Magic

A Docker image built through Github Actions with Git commit version tag

# Why

I found that Magic's Docker image is difficult to find.
The code on [GitHub](https://github.com/opendatalab/MinerU.git) does not provide a pre-built Docker image.

This project will use GitHub Actions and Docker Hub to build and publish images,
aiming to keep the process as clean as possible without custom configuration files.

# Tags

The images of this project will be published to Docker Hub under the repository [xiaoyao9184/magic](https://hub.docker.com/r/xiaoyao9184/magic).

Since this project references the Magic project via a submodule, it cannot monitor push events on the Magic project, and therefore cannot automatically create an image for every commit.
A good solution is to manually trigger the action and tag it with the commit id. For more details, see this article [set-dynamic-parameters-github-workflows-en](https://damienaicheh.github.io/github/actions/2022/01/20/set-dynamic-parameters-github-workflows-en.html).

The default image name format is `${DOCKERHUB_USERNAME}/magic`.

The tag uses the input parameter `commit_id`,
which can be either a branch name or a commit id, 
when manually triggering the [docker-image-tag-commit](./.github/workflows/docker-image-tag-commit.yml) job.
if the job is triggered by a submodule update push,
the default branch name `main` will be used instead of the `commit_id` parameter.
This job will also use the shortened commit id as the tag.

If the job [docker-image-tag-version](./.github/workflows/docker-image-tag-version.yml) is triggered with the `magic_version` parameter set to the PyPI Magic version number,
the Magic package published on PyPI will be installed for the build,
and `magic_version` will be used as the tag.

Currently, only the `linux/amd64` platform is supported.

# Change

You can fork this project and build your own image. You will need to provide the following variables: `DOCKERHUB_USERNAME`, `DOCKERHUB_TOKEN`.
See [this](https://github.com/docker/login-action#docker-hub) for more details.