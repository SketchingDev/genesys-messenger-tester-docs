---
layout: default
title: AI
parent: Writing Tests
has_children: true
nav_order: 2
---

# Testing Chatbots with AI

Start by setting up an API key for ChatGPT:

1. [Create an API key for OpenAI](https://help.openai.com/en/articles/4936850-where-do-i-find-my-api-key)
2. Set the key in the environment variable: `OPENAI_API_KEY`

Write a scenario file containing all the scenarios you wish to run along with
the [ID and region of your Web Messenger Deployment](https://help.mypurecloud.com/articles/deploy-messenger/).

The scenarios are written as ChatGPT Prompts, these can take some fine-tuning to get right. The `terminatingPhrases`
section defines the phrases you instruct ChatGPT to say to pass or fail a test.

> [examples/cli-ai-tests/example.yml](https://github.com/ovotech/genesys-web-messaging-tester/tree/main/examples/cli-ai-tests/example.yml)

```yaml
config:
  deploymentId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
  region: xxxx.pure.cloud
scenarios:
  "Accept survey":
    setup:
      prompt: |
        I want you to play the role of a customer talking to a company's online chatbot. You must not
        break from this role, and all of your responses must be based on how a customer would realistically talk to a company's chatbot.

        To help you play the role of a customer consider the following points when writing a response:
        * Respond to questions with as few words as possible
        * Answer with the exact word when given options e.g. if asked to answer with either 'yes' or 'no' answer with either 'yes' or 'no' without punctuation, such as full stops

        As a customer you would like to leave feedback of a recent purchase of a light bulb you made where a customer service
        rep was very helpful in finding the bulb with the correct fitting.

        If at any point in the company's chatbot repeats itself then say the word 'FAIL'.

        If you have understood your role and the purpose of your conversation with the company's chatbot then say the word 'Hello'
        and nothing else.
      terminatingPhrases:
        pass: ["PASS"]
        fail: ["FAIL"]
```

Then run the AI test by pointing to the scenario file in the terminal:

```shell
web-messaging-tester ai tests/example.yml
```
