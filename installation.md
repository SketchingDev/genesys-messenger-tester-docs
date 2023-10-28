---
title: Installation
layout: page
nav_order: 2
---

# Installation

Prepare your system by installing [node](https://nodejs.org/en/download/)

Install the CLI tool using [`npm`](https://www.npmjs.com/package/@ovotech/genesys-web-messaging-tester-cli):

```shell
npm install -g @ovotech/genesys-web-messaging-tester-cli
```

Test it has installed properly by running:

```shell
web-messaging-tester scripted --help
```

You should see:
```
$ web-messaging-tester scripted --help
Usage: web-messaging-tester scripted [options] <filePath>

Arguments:
  filePath                             Path of the YAML test-script file

Options:
  -id, --deployment-id <deploymentId>  Web Messenger Deployment's ID
  -r, --region <region>                Region of Genesys instance that hosts the Web Messenger Deployment
  -o, --origin <origin>                Origin domain used for restricting Web Messenger Deployment
  -p, --parallel <number>              Maximum scenarios to run in parallel (default: 1)
  -a, --associate-id                   Associate tests their conversation ID.
                                       This requires the following environment variables to be set for an OAuth client
                                       with the role conversation:webmessaging:view:
                                       GENESYS_REGION
                                       GENESYSCLOUD_OAUTHCLIENT_ID
                                       GENESYSCLOUD_OAUTHCLIENT_SECRET (default: false)
  -fo, --failures-only                 Only output failures (default: false)
  -t, --timeout <number>               Seconds to wait for a response before
                                       failing the test (default: 10)
  -h, --help                           display help for command
```
