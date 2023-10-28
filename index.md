---
title: Home
layout: home
nav_order: 1
---

<p class="text-center">
Automatically test your Web Messenger Deployments
</p>

This tool automatically
tests [Genesys' Web Messenger Deployments](https://help.mypurecloud.com/articles/web-messaging-overview/)
against scenarios in a YAML file. This makes testing:

* **Fast** - spot problems with your flow sooner than manually testing
* **Repeatable** - scenarios in test scripts are run exactly as defined. Any response that deviates is flagged
* **Customer focused** - expected behaviour can be defined as test-script scenarios before development commences
* **Automatic** - being a CLI tool means it can be integrated into your CI/CD pipeline, or run on a scheduled basis e.g.
  to monitor production

![Demo of tool executing two scenarios that pass](./assets/images/cli/demo.gif?raw=true)

The above test is using the test-script:

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

## How it works

The tool uses [Web Messenger's guest API](https://developer.genesys.cloud/api/digital/webmessaging/websocketapi) to
simulate a customer talking to a Web Messenger Deployment. Once the tool starts an interaction it follows instructions
defined in a file called a 'test-script', which tells it what to say and what it should expect in response. If the
response deviates from the test-script then the tool flags the test as a failure, otherwise the test passes.

![Tool using test-script file to test Web Messenger Deployment](https://github.com/ovotech/genesys-web-messaging-tester/blob/main/docs/assets/cli/overview.png?raw=true)
