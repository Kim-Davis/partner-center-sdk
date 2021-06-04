---
title: Partner Center webhook events
description: Learn how to test and use Webhook events to note when subscriptions and other events change in Partner Center.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: cychua
ms.author: cychua
---

# Partner Center webhook events

**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Partner Center webhook events are resource change events delivered in the form of HTTP POSTs to a registered URL. To receive an event from Partner Center, you host a callback where Partner Center can POST the event. The event is digitally signed so you can validate that it was sent from Partner Center.

For information on how to receive events, authenticate a callback, and use the Partner Center webhook APIs to create, view, and update an event registration, see [Partner Center Webhooks](partner-center-webhooks.md).

## Supported Events

The following webhook events are supported by Partner Center.

### Test Event

This event allows you to self-onboard and test your registration by requesting a test event and then tracking its progress. You will be able to see the failure messages that are being received from Microsoft while trying to deliver the event. This will only apply to "test-created" events and data older than seven days will be purged.

>[!NOTE]
>There is a throttle limit of 2 requests per minute when posting a test-created event.

#### Properties

| Property                  | Type                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | The name of the event. In the form {resource}-{action}. For this event, the value is "test-created".                                          |
| ResourceUri               | URI                                | The URI to get the resource. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/registration/validationEvents/{{CorrelationId}}" |
| ResourceName              | string                             | The name of the resource that will trigger the event. For this event, the value is "test".                                  |
| AuditUri                  | URI                                | (Optional) The URI to get the audit record, if it exists. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | string in the UTC date-time format | The date and time when the resource change occurred.                                                         |

#### Example

```json
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{{CorrelationId}}",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### Subscription Updated Event

This event is raised when the specified subscription changes. A Subscription Updated event is generated when there is an internal change in addition to when changes are made through the Partner Center API.  This event will only be generated when there are commerce level changes, for example, when the number of licenses are modified and when the state of the subscription changes. It will not be generated when resources are created within the subscription.

>[!NOTE]
>There is a delay of up to 48 hours between the time a subscription changes and when the Subscription Updated event is triggered.

#### Properties

| Property                  | Type                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | The name of the event. In the form {resource}-{action}. For this event, the value is "subscription-updated".                                  |
| ResourceUri               | URI                                | The URI to get the resource. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}" |
| ResourceName              | string                             | The name of the resource that will trigger the event. For this event, the value is "subscription".                          |
| AuditUri                  | URI                                | (Optional) The URI to get the audit record, if it exists. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | string in the UTC date-time format | The date and time when the resource change occurred.                                                         |

#### Example

```json
{
    "EventName": "subscription-updated",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}",
    "ResourceName": "subscription",
    "AuditUri": "https://api.partnercenter.microsoft.com/v1/auditrecords/{{AuditId}}",
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### Threshold Exceeded Event

This event is raised when the amount of Microsoft Azure usage for any customer exceeds their usage spending budget (their threshold). For more information, see  [Set an Azure spending budget for your customers/partner-center/set-an-azure-spending-budget-for-your-customers).

#### Properties

| Property                  | Type                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | The name of the event. In the form {resource}-{action}. For this event, the value is "usagerecords-thresholdExceeded".                                  |
| ResourceUri               | URI                                | The URI to get the resource. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/usagerecords" |
| ResourceName              | string                             | The name of the resource that will trigger the event. For this event, the value is "usagerecords".                          |
| AuditUri                  | URI                                | (Optional) The URI to get the audit record, if it exists. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | string in the UTC date-time format | The date and time when the resource change occurred.                                                         |

#### Example

```json
{
    "EventName": "usagerecords-thresholdExceeded",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/customers/usagerecords",
    "ResourceName": "usagerecords",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### Referral Created Event

This event is raised when the referral is created.

#### Properties

| Property                  | Type                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | The name of the event. In the form {resource}-{action}. For this event, the value is "referral-created".                                  |
| ResourceUri               | URI                                | The URI to get the resource. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" |
| ResourceName              | string                             | The name of the resource that will trigger the event. For this event, the value is "referral".                          |
| AuditUri                  | URI                                | (Optional) The URI to get the audit record, if it exists. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | string in the UTC date-time format | The date and time when the resource change occurred.                                                         |

#### Example

```json
{
    "EventName": "referral-created",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### Referral Updated Event

This event is raised when the referral is updated.

#### Properties

| Property                  | Type                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | The name of the event. In the form {resource}-{action}. For this event, the value is "referral-updated".                                  |
| ResourceUri               | URI                                | The URI to get the resource. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" |
| ResourceName              | string                             | The name of the resource that will trigger the event. For this event, the value is "referral".                          |
| AuditUri                  | URI                                | (Optional) The URI to get the audit record, if it exists. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | string in the UTC date-time format | The date and time when the resource change occurred.                                                         |

#### Example

```json
{
    "EventName": "referral-updated",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### Invoice Ready Event

This event is raised when the new invoice is ready.

| Property                  | Type                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName | string | The name of the event. In the form {resource}-{action}. For this event, the value is "invoice-ready". |
| ResourceUri | URI | The URI to get the resource. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{{InvoiceId}}" |
| ResourceName | string | The name of the resource that will trigger the event. For this event, the value is "invoice". |
| AuditUri |  URI | (Optional) The URI to get the audit record, if it exists. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}") |
| ResourceChangeUtcDate | string in the UTC date-time format | The date and time when the resource change occurred. |

#### Example

```json
{
    "EventName": "invoice-ready",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/invoices/{{InvoiceId}}",
    "ResourceName": "invoice",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}

```
