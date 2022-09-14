# custom-docker-images

Investigating custom Docker image building off cimg images

## Nuance

It seems `cimg/node:lts` image at some point refer/alias to `cimg/node:16.16`.

The `cimg/node:16.16` Docker image is somehow set up to include a BASH_ENV env var (via the ENV command).
See https://github.com/CircleCI-Public/cimg-node/blob/main/16.16/Dockerfile#L13

This is not observed for other cimg/node:* images though.

I understand the `cimg/node:16.16` Dockerfile was contributed by an external contributor (outside CircleCI).
https://github.com/CircleCI-Public/cimg-node/pull/264

More recently, the `cimg/node:lts` image looks to now refer/alias to `cimg/node:16.17`, which does not have BASH_ENV env var set.

It can be that the `ENV BASH_ENV /home/circleci/.circlerc` command seen on the `cimg/node:16.16` is not something CircleCI wants to do officially?
