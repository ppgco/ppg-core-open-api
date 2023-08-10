# **CORE** _by PushPushGo_ SDK for JavaScript / TypeScript

[![npmjs version](https://img.shields.io/npm/v/@pushpushgo/core-sdk-js?style=flat-square)](https://www.npmjs.com/package/@pushpushgo/core-sdk-js)
![GitHub Workflow Status (main)](https://img.shields.io/github/actions/workflow/status/ppgco/ppg-core-js-sdk/publish.yml?style=flat-square)
![GitHub tag (latest)](https://img.shields.io/github/v/tag/ppgco/ppg-core-js-sdk?style=flat-square)
[![Discord](https://img.shields.io/discord/1108358192339095662?color=%237289DA&label=Discord&style=flat-square)](https://discord.gg/NVpUWvreZa)

## Product Info

**CORE** _by PushPushGo_ is a hassle-free building block for all your web and mobile push needs.

Send your transactional and bulk messages, and we'll take care of the rest.

#### What we offer:
 - Ready SDK for client/server integration - we have SDK for the most popular platforms.
 - Mobile and WebPush implementation (APNS, FCM, VAPID).
 - Transactional and bulk push notifications through API.
 - Hassle-free usage. Our servers handle traffic peaks and store images.
 - Event aggregation in bulk sent to your webhook for easy analysis or running your business logic.
 - GDPR-ready solution protecting private data in accordance with EU regulations.
 - No vendor lock-in - build and own your subscriber base (stateless solution).

#### What you get:
 - Cost-effective solution: pay for sent pushes, not for infrastructure, traffic, and storage.
 - Save time and effort on developing the sender and infrastructure.
 - Simple API interface for all channels with bulk support.
 - Support on our [Discord Server](https://discord.gg/NVpUWvreZa).
 - You can implement notification features your way.

#### Try it if:
 - You want to control the flow in your transactional messages and add a push notification channel.
 - You're looking for an easy push notifications tool for your organization, whether it's finance, e-commerce, online publishing, or any other sector.
 - You work in a software house and build solutions for your clients.
 - You want a hassle-free solution to focus on other tasks at hand.
 - You want to implement an on-premise solution for sending notifications.
 - You have issues with an in-house solution.
 - You're looking for a reliable provider and cooperation based on your needs.

## How it works

When client register for notifications you will get object with:
 - Credentials
 - Token/endpoint
 - Type of provider
 - Identifier of provider

We call this **Recipient** - it's your subscription data, store it in your database.

When you try to send message you will prepare:

 - **Bucket** - your temporary credentials bucket - this bucket can be reused any time, or recreated when credentials changed,

 - **Context** - your message - this context can be reused to send bulk messages or just used once when you send transactional message then is context is **temporary**

When you send message you will _authorize_ via **bucket** data, prepare message with **context** and send to **recipients** that can be bulked up to 1000 per request.

On the server side:
 - We validate and prepare the message body.
 - Then, we upload and resize images to our CDN.
 - Next, we connect and send to different providers.

On the client side:
 - Get notifications via our SDK in your App/Website.
 - When interacting with a notification, we collect events with our API.

On the server side:
 - We aggregate events and deliver them in bulk to your webhook endpoint.

### Architecture

![image](https://i.ibb.co/tst39rS/architecture.png "Architecture")

When a message is delivered to the device and interacts with the user, we collect events and pass them to our API. The collected events are resent to your webhook endpoint.

#### Webhooks events
During the journey of push we will trigger webhook events.

| Push Type    | Event      | Foreground | Background |
|---------|------------|------------|------------|
| Data    |            |            |            |
|         | delivered  | ✓          | ✓          |
|         | clicked    | ✓          | ✓          |
|         | sent       | ✓          | ✓          |
|         | close      | ✓          | ✓          |
| Silent<sup>1</sup>  |            |            |            |
|         | delivered  | ✓          | ✓          |
|         | sent       | ✓          | ✓          |

<small><sup>1</sup> - webpush doesn't support silent messages due to Push API implementation</small>

If `foreignId` field was passed with `receiver` then it will also be included in event in message.

Example events package:

```json
{
    "messages": [
        {
            "messageId": "8e3075f1-6b21-425a-bb4f-eeaf0eac93a2",
            "foreignId": "my_id",
            "result": {
                "kind": "delivered"
            },
            "ts": 1685009020243
        }
    ]
}
```

## Pricing

We charge $0.50 USD for every 1000 sent notifications.

## Support & Sales

Join our [Discord](https://discord.gg/NVpUWvreZa) for docs, support, talk or just to keep in touch.

<sub>**CORE** _by PushPushGo_ is not the same as our main **PushPushGo** product - are you looking for [PushPushGo - Push Notifications Management Platform?](https://pushpushgo.com)</sub>

## Swagger

You can get actual API specification via [our swagger](https://swagger)