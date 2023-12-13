# v2 of [www.les.cx](https://www.les.cx)

## Branches

Short:

* main (merge branch)
* [fix,feature]_foo
* staging (lescx.github.io)
* production (www.les.cx)

### main

Work is done in feature branches which get merged into **main**.

The **main** branch doesn't get touched directly. The only this this "main" branch is used for is for feature branches to be merged into.
New releases get release tags.
After that the CI/CD pipeline kicks in, pushes the new website onto the **staging** branch and later onto **production**.
