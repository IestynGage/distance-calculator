# Distance calculator

A website that calculates the total distance traveled using pace + distance.

## How to deploy

```sh
$ yarn build
# Remeber to change links in index.html from "/foo" to "./foo"
$ git subtree push --prefix dist/ origin gh-pages
```