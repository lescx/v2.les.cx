# Second version of [www.les.cx](https://www.les.cx)

[www.les.cx](https://www.les.cx) has been moved [from a VPS](https://www.netcup.de) to GitHub Pages. This change was made because I only serve static content and there isn't any need to administrate a whole VPS for a single website. It also cuts the costs for this site and my workload.

I'm using a CI/CD to deploy my website to GitHub Pages.

Commits to **main** can only be done through a pull request from a feature branch (e.g. **hugo/bump-version-0.121.1**).
After the merge, the pipeline is triggered and builds the hugo website and pushes the `./public` folder to GitHub Pages.