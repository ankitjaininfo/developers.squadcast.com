---
title: Outgoing Webhooks
pcx-content-type: overview
layout: single
weight: 0
meta:
  title: Outgoing webhooks
---

# Outgoing Webhooks

Outgoing webhooks allow Squadcast to notify external systems in real time when specific events occur—eliminating the need to poll APIs or manually monitor the Squadcast UI. You can configure Squadcast to send event data to your own services or third-party tools using HTTP requests.

This feature enables deeper integration with your infrastructure, automation workflows, and incident response tooling.

This guide explains how to configure outgoing webhooks in Squadcast, the list of supported events, and how data is delivered to your endpoint. Before starting, ensure you have the necessary permissions to manage webhook settings.

## Supported Events

You can configure a webhook to be triggered by one or more events within Squadcast. Once configured, Squadcast sends a JSON payload to your specified URL(s) whenever a matching event occurs.

- v1 Webhooks: Support a limited set of event types. View [v1 event schema](./payload/v1/).
- v2 Webhooks: Offer a broader range of events. View [v2 event schema](./payload/v2/).

If you need support for additional events, contact our Support team with your use case.

## Communication Protocol for Webhooks

Squadcast sends webhook payloads using the HTTP POST method with a `Content-Type: application/json` header. A webhook is triggered every time a selected event occurs.

Successful delivery expects a `2xx` HTTP response code from your server. If a non-2xx response is returned, Squadcast retries the request up to **three times**.

## Setting up Webhooks

### URLs and Headers

We support the addition of multiple URL endpoints, with POST, PUT and PATCH methods. 

Incident payloads will be sent to all the URL endpoints that are added. 
 
You can also configure additional headers. These headers will get attached to all the webhook calls that will be made based on this configuration.

### Filters
You can filter on top of events from the Services and Alert Sources drop-downs, either by having an individual expression or a combination of expressions/expression groups.

### Logs

After a webhook is triggered, you can inspect the delivery status in the Logs tab. Click the expand icon on any log entry to view:

- Timestamp
- Full payload
- Delivery response

### Additional Settings
In the Settings tab, you can configure:
- Webhook name and description
- Failure notification email, so admins or owners are alerted in case of delivery issues

## Test and Validate Webhook Payloads

To safely observe outgoing webhook behavior during development or troubleshooting, consider using a tool like [Beeceptor](https://beeceptor.com/webhook-integration/) to create a temporary HTTPs catch all endpoint. This allows you to:
- Capture and inspect headers and JSON payloads from Squadcast
- Validate behavior for different event triggers
- Confirm formatting before forwarding to your production systems

Once verified, replace the temporary URL with your actual endpoint or configure forwarding within Beeceptor for ongoing visibility.
