---
title: API
layout: page
nav_order: 5
---

# API

```typescript
const session = new WebMessengerGuestSession({
  deploymentId: 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx',
  region: 'xxxx.pure.cloud',
});

const convo = new Conversation(session);
await convo.waitForConversationToStart();

await convo.sendText('hi');

await convo.waitForResponseContaining('Please enter your account number');

await convo.sendText('123');

await convo.waitForResponseContaining('Your account number is too short. It is the 6 digit number on your bills');
```

## Getting Started

Install using [`npm`](https://www.npmjs.com/package/@ovotech/genesys-web-messaging-tester):

```bash
npm install -g @ovotech/genesys-web-messaging-tester
```

Then write a test. In the example below we test the validation of an account number:

> [examples/api/src/js-script.js:(test-section)](https://github.com/ovotech/genesys-web-messaging-tester/tree/main/examples/api/src/js-script.js#L5-L33)

```javascript
const WebMsgTester = require('@ovotech/genesys-web-messaging-tester');

(async () => {
  const session = new WebMsgTester.WebMessengerGuestSession({
    deploymentId: process.env.DEPLOYMENT_ID,
    region: process.env.REGION,
  });

  const convo = new WebMsgTester.Conversation(session);
  await convo.waitForConversationToStart();

  await convo.sendText('hi');

  await convo.waitForResponseWithTextContaining(
    'Can we ask you some questions about your experience today?',
  );

  await convo.sendText('Yes');

  await convo.waitForResponseWithTextMatchingPattern(/Thank you! Now for the next question[.]+/im, {
    timeoutInSeconds: 10,
  });

  session.close();
})().catch((e) => {
  throw e;
});
```

Finally, run the test by executing the script:

```shell
node examples/api/src/js-script.js
```

## Debugging

Messages sent between the client and Genesys' server can be output by setting the environment variable:

```shell
DEBUG=WebMessengerGuestSession
```
