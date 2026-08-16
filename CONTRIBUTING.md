# Contributing

The following information provides a set of guidelines for contributing to the tungbq/cmd chain main repo. Use your best judgment, and, if you see room for improvement, please propose changes to this document.

## First steps

The first step is to find an [**issue**](https://github.com/tungbq/cmd/issues) you want to fix. To identify issues we think are good for first-time contributors, we add the **good first issue** label.
Once you find an existing issue that you want to work on or if you have a new issue to create, continue below.

## Proposing changes

To contribute a change proposal, use the following workflow:

1. [Fork the repository](https://github.com/tungbq/cmd).
2. If you find this repository helpful, kindly consider showing your appreciation by giving it a star ⭐ Thanks! 💖
3. [Add an upstream](https://docs.github.com/en/github/collaborating-with-pull-requests/working-with-forks/syncing-a-fork) so that you can update your fork.
4. Clone your fork to your computer.
5. Create a branch and name it appropriately.
6. Work on only one major change in one pull request.
7. Make sure all tests are passing locally.
8. Next, rinse and repeat the following:

   1. Commit your changes. Write a simple, straightforward commit message. To learn more, see [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/).
   2. Push your changes to your remote fork. To add your remote, you can copy/paste the following:

   ```bash

   #Remove origin

   git remote remove origin

   #set a new remote

   git remote add my_awesome_new_remote_repo [insert-link-found-in-source-subtab-of-your-repo]

   #Verify new remote

   git remote -v

   > my_awesome_new_remote_repo  [link-found-in-source-subtab-of-your-repo] (fetch)
   > my_awesome_new_remote_repo  [link-found-in-source-subtab-of-your-repo] (push)

   #Push changes to your remote repo

   git push <your_remote_name>

   #e.g. git push my_awesome_new_remote_repo
   ```

   3. Create a PR on the **tungbq/cmd** repository. There should be a PR template to help you do so.
   4. Wait for your changes to be reviewed. If you are a maintainer, you can assign your PR to one or more reviewers. If you aren't a maintainer, one of the maintainers will assign a reviewer.
   5. After you receive feedback from a reviewer, make the requested changes, commit them to your branch, and push them to your remote fork again.
   6. Once approval is given, feel free to squash & merge!

## Previewing the website locally

All content lives in `README.md`. The website at [tungbq.github.io/cmd](https://tungbq.github.io/cmd) renders that same file through the Jekyll layout in `_layouts/default.html` and the styles in `assets/css/style.css`.

Content changes need no local setup, but if you touch the layout or the styles you can preview the built site with Docker:

```bash
# Build the site into ./_site
docker run --rm -v "$PWD":/src -w /src -e PAGES_REPO_NWO=tungbq/cmd \
  --entrypoint github-pages ghcr.io/actions/jekyll-build-pages:latest \
  build --destination /src/_site

# Serve it (the site expects the /cmd base path)
mkdir -p preview && cp -r _site preview/cmd && (cd preview && python3 -m http.server 8000)
# Then open http://localhost:8000/cmd/
```

Note: Jekyll runs `README.md` through Liquid, so a command example containing `{{` (for example a Go template in `docker inspect -f`) is parsed as a template tag and that line disappears from the website. Prefer an equivalent that avoids double curly braces.
