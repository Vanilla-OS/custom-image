# Custom Vib Image

This template repository is a starting point for creating custom [Vib images](https://github.com/Vanilla-OS/Vib) on top of our desktop image. It contains a basic recipe and an example module to get you started.

It is suggested to checkout the [Vib repository's README](https://github.com/Vanilla-OS/Vib?tab=readme-ov-file#recipe-format) to know more about the recipe format, structure of modules and the supported fields.

## Explore

Now, that you are aware of the basic syntax, let's explore the files and directories present in this repository:

- `.github/workflows/vib-build.yml`: This file contains the GitHub Actions workflow to check for updates to base image and build the Vib image. It uses the `vib` action to build the recipe and upload it as an artifact. The generated artifact is then built using Docker and pushed to GHCR. The action runs automatically on a schedule checking updates to the base image using [Differ](https://github.com/Vanilla-OS/Differ).
- `.github/workflows/vib-pr.yml`: This file contains the GitHub Actions workflow to build the Vib image on pull requests. It uses the `vib` action to build the recipe and upload it as an artifact. You can view the artifact to verify that your changes are performed as expected.
- `.github/dependabot.yml`: This file contains the configuration for Dependabot to check for updates to the GitHub actions used in the workflow files monthly and when it finds a new version it creates a PR in your repository.
- `includes.container`: The files included in this directory are added by default to your image (It also contains ABRoot's configuration file).
- `modules`: This directory contains the modules that are used to customize the image. You can add your own modules to this directory.
- `recipe.yml`: This file contains the recipe for the image. It contains the base image, modules and other fields to be present in the image.

## Getting Started
