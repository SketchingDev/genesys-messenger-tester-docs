---
title: Quick Start
layout: page
nav_order: 3
---

# Quick Start

Write a test-script containing all the scenarios you wish to run along with
the [ID and region of your Web Messenger Deployment](https://help.mypurecloud.com/articles/deploy-messenger/).

> [examples/cli-scripted-tests/example-pass.yml](https://github.com/ovotech/genesys-web-messaging-tester/tree/implement-chatgpt/examples/cli-scripted-tests/example-pass.yml)

```yaml
config:
  deploymentId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
  region: xxxx.pure.cloud
scenarios:
  "Accept Survey":
    - say: hi
    - waitForReplyContaining: Can we ask you some questions about your experience today?
    - say: Yes
    - waitForReplyMatching: Thank you! Now for the next question[\.]+
  "Decline Survey":
    - say: hi
    - waitForReplyContaining: Can we ask you some questions about your experience today?
    - say: No
    - waitForReplyContaining: Maybe next time. Goodbye
  "Provide Incorrect Answer to Survey Question":
    - say: hi
    - waitForReplyContaining: Can we ask you some questions about your experience today?
    - say: Not sure
    - waitForReplyContaining: Sorry I didn't understand you. Please answer with either 'yes' or 'no'
    - waitForReplyContaining: Can we ask you some questions about your experience today?
```

Then run the test by pointing to the test-script in the terminal:

```shell
web-messaging-tester scripted tests/example.yml
```

## Examples

Override Deployment ID and Region in test-script file:

```shell
web-messaging-tester scripted test-script.yaml -id 00000000-0000-0000-0000-000000000000 -r xxxx.pure.cloud
```

Run 10 scenarios in parallel:

```shell
web-messaging-tester scripted test-script.yaml --parallel 10
```
