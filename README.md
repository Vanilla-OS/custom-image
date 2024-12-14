# Custom Vib Image

This template repository is a starting point for creating custom [Vib images](https://github.com/Vanilla-OS/Vib) on top of the [official Vanilla OS images](https://images.vanillaos.org) like [desktop image](https://github.com/Vanilla-OS/desktop-image). It contains a basic recipe and an example module to get you started.

> [!TIP]
> It is suggested to check the [Vib documentation](https://docs.vanillaos.org/collections/vib) to know more about the recipe format, structure of modules and the supported fields.

## Getting Started

- First, click on the <kbd>Use this template</kbd> button in the top right corner, then from the drop-down menu select <kbd>Create a new repository</kbd>. This would create a new repository with the same files and directories as this repository.
- Go to **Settings → Actions → General** and ensure "_Allow all actions and reusable workflows_" are enabled.
- Now, clone the repository to your local machine and let's start customizing your image. You can also use the GitHub online editor if you prefer.
- Open the `vib-build.yml` workflow file and replace the custom image name with an image name of your choosing in line 14.
- Open the `recipe.yml` file and replace the image name and ID with your image name and ID in lines 1 and 2.
- Now, perform your additions and modifications to the recipe as per your requirements.
- If you just want to install `.deb` files, you can just put them in `includes.container/deb-pkgs` (if you choose this option, make sure to keep the .deb file up to date, it will not be upgraded automatically)
- Optionally, add your modules to the `modules` directory and add them to the package-modules `includes` in `recipe.yml`.
- You can check the Actions tab in GitHub to see the build progress of your image.

> [!NOTE]
> It is suggested to add `vib-image` and `vib` tags to your repository for your image to be easily discoverable to others.

## Use your custom image

If your image is successfully built, you can then point ABRoot to your custom image to use it.

- Edit the configuration file with the command: `abroot config-editor`.
- Change the "name" entry from something like `vanilla-os/desktop` to `your-github-name/your-image-name` (for example `taukakao/custom`).  [**Note**: All characters must be in lowercase.]
- Now, Run `abroot upgrade` to switch to your custom image.

## Explore

Now, that you are aware of the basics, let's explore the files and directories present in this repository:

- `.github/workflows/vib-build.yml`: This file contains the GitHub Actions workflow to check for updates to the base image and build the Vib image on push and pull requests.
  - It uses the [`vib-gh-action`](https://github.com/Vanilla-OS/vib-gh-action) to build the recipe and upload it as an artifact. The generated artifact is then built using Docker's actions and pushed to GHCR (**Note**: The image with the respective branch tags is published to GHCR only on push actions to the branches in your repository or on tags and not on pull requests).
  - The action runs automatically on a schedule checking updates to the base image using [Differ](https://github.com/Vanilla-OS/Differ).
- `.github/workflows/release.yml`: This file contains the GitHub Actions workflow to automatically create a GitHub release when a tag is created and it uploads the generated Containerfile to the release for future reference.
- `.github/dependabot.yml`: This file contains the configuration for GitHub's Dependabot to check for updates to the GitHub actions used in the workflow files monthly and when it finds a new version it creates a PR in your repository.
- `includes.container`: The files included in this directory are added by default to your image to the specified location (**Note**: It also contains ABRoot's configuration file).
- `modules`: This directory contains the modules that are used to customize the image. You can add your modules to this directory.
- `recipe.yml`: This file contains the recipe for the image. It specifies the base image, modules and other fields to be present in the custom image.
