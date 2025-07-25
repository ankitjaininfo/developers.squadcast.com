---
title: Outgoing Webhooks
pcx-content-type: overview
layout: single
weight: 0
meta:
  title: Outgoing webhooks
---

# Outgoing Webhooks

Outgoing webhooks in Squadcast allow you to receive real-time notifications about events as they happen, without polling the API or checking the web/mobile app manually. By configuring a webhook, Squadcast will send structured event data (as JSON) to your specified endpoint whenever selected triggers occur.

This enables seamless integration with your internal tools, third-party services, or custom workflows, making it easier to act on incidents, automate escalations, or maintain audit trails. This document outlines how to configure outgoing webhooks in Squadcast, details the supported event types, and explains delivery behavior, filtering options, and logging features.

Ensure that you have the necessary permissions before proceeding with webhook setup.

## Supported Events

The webhook that you have configured can be triggered for certain events occurring in Squadcast. 

You can choose multiple triggers for a webhook. Information is sent to the provided URLs if any of the triggers match.

In the legacy version v1, only limited events are supported, whereas the latest version v2, supports an exhaustive list of events.

For **v1 events**, [refer here](./payload/v1/).

For **v2 events**, [refer here](./payload/v2/).

If your use-case requires more Squadcast events to be supported, please reach out to our Support team with details of the same.

## Communication Protocol for Webhooks

A webhook is called whenever the configured events occur in Squadcast.

A webhook call is made using the HTTP POST method to the URL(s) that were added when the webhook was configured, with a body that is encoded using JSON.

Squadcast expects that the server that responds to the webhook will return a 2xx response code upon success. If a non-2xx response is received, Squadcast will retry the request for a maximum of 3 times.

## URLs and Headers

We support the addition of multiple URL endpoints, with POST, PUT and PATCH methods. 

Incident payloads will be sent to all the URL endpoints that are added. 
 
You can also configure additional headers. These headers will get attached to all the webhook calls that will be made based on this configuration.

## Filters
You can filter on top of events from the Services and Alert Sources drop-downs, either by having an individual expression or a combination of expressions/expression groups.

## Logs
Once the webhook call has been made, you can view the logs for it in the Logs tab.

Click on the expand icon on any of the individual logs to view the payload that has been sent across.

## Additional Settings
Configure the Name, Description and Failure Notification email in the Settings tab. This is particularly helpful when you (or an administrator) would want to be notified for webhook-related failures.


## Optional: Test Payloads

During integration, it’s often useful to observe and debug outbound webhook calls before forwarding them to production systems. This helps ensure that your receiving endpoint is ready and that the payloads from Squadcast are as expected. You can use [Beeceptor](https://beeceptor.com/webhook-integration/) to set up a temporary HTTPS endpoint to receive and inspect Squadcast’s outgoing webhook payloads. This allows you to:

- View full request bodies and headers
- Verify event formats for v1 or v2 payloads
- Confirm behavior across different Squadcast trigger conditions
- Identify any formatting or delivery issues before forwarding to downstream systems

Once validated, you can either update the Squadcast configuration with your real endpoint or configure Beeceptor to forward requests to your destination URL.
