# Second version of [www.les.cx](https://www.les.cx)

[www.les.cx](https://www.les.cx) has been moved [from a VPS](https://www.netcup.de) to GitHub Pages. This change was made because I only serve static content and there isn't any need to administrate a whole VPS for a single website. It also cuts the costs for this site and my workload.

## Branches

As I'm using a CI/CD to deploy my website, I do have a few rules on where development takes place.

### Short:

* main (merge branch; no direct commits)
* [fix,feature,pipeline,…]/branch-description
* production (known as gh-pages in other repos; CD to www.les.cx)