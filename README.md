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

It looks like the `ENV BASH_ENV /home/circleci/.circlerc` commands seen on the `cimg/node:16.16` is not something that is followed through for all cimg/node:* tags?


| Image tag | BASH_ENV set? | Remarks |
| --- | --- | -- |
| [cimg/node:16.16](https://github.com/CircleCI-Public/cimg-node/blob/main/16.16/Dockerfile) | :white_check_mark: ([here](https://github.com/CircleCI-Public/cimg-node/blob/6c4dd23c2ac191c107e1b6ac1438b2b80284a8f4/16.16/Dockerfile#L12-L19)) | |
| [cimg/node:16.17](https://github.com/CircleCI-Public/cimg-node/blob/main/16.17/Dockerfile) | NO | current LTS |
| [cimg/node:17.9](https://github.com/CircleCI-Public/cimg-node/blob/main/17.9/Dockerfile) | :white_check_mark: ([here](https://github.com/CircleCI-Public/cimg-node/blob/6c4dd23c2ac191c107e1b6ac1438b2b80284a8f4/17.9/Dockerfile#L12-L19)) | |
| [cimg/node:18.3](https://github.com/CircleCI-Public/cimg-node/blob/main/18.3/Dockerfile) | :white_check_mark: ([here](https://github.com/CircleCI-Public/cimg-node/blob/6c4dd23c2ac191c107e1b6ac1438b2b80284a8f4/18.3/Dockerfile#L12-L19)) | |
| [cimg/node:18.8](https://github.com/CircleCI-Public/cimg-node/blob/main/18.8/Dockerfile) | NO | |
