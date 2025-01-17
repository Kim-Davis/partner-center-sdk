---
title: Gets a single promotion
description: Gets a single promotion for a given promotion ID and country.
ms.date: 09/23/2021
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
---

# Get promotion by ID

**Applies To**

- Partner Center

**Appropriate roles**

- Global admin
- Admin agent

> [!Note] 
> New Commerce changes are currently available only to partners who are part of the Microsoft 365 and Dynamics 365 new commerce experience technical preview.

Partners can get a single promotion for a given promotion ID and country. This method returns the promotion data, ignoring the promotion start and end dates. This method is used primarily for reconciliation purposes to retrieve promotion details even after the promotion has expired.



## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

- Promotion ID is delimited set of strings that represent a specific promotion.

- Country represents the customer country promotions are available for. Country is represented by a two character country code.

## REST request

### Request syntax

| Method   | Request URI                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **GET**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/productpromotions/{promotion-id}?country={country-code HTTP/1.1 |

### URI parameter

Use the following query parameters to return available promotions.

| Name                    | Type     | Required | Description                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **promotion-id**  | **string** | Y        | A string defining the promotion to retrieve.           |
| **country** | **string** | Y        | A two letter country code determining which customer country promotions are available for. |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/productpromotions/CFQ7TTC0HD33:0003:CFQ7TTC0K59M?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## REST response

If successful, this method returns a single promotion.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and more debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 24 Sep 2021 20:42:26 GMT

 
        {
            "id": "39NFJQT1PJQB:0001:39NFJQT1Q5KN",
            "name": "Visio Plan 1",
            "description": "Visio Plan 1",
            "startDate": "2021-09-23T00:00:00+00:00",
            "endDate": "2021-10-14T23:59:59+00:00",
            "properties": {
                "isAutoApplicable": true
            },
            "requiredProducts": [
                {
                    "productId": "CFQ7TTC0HD33",
                    "skuId": "0003",
                    "term": {
                        "duration": "P1Y",
                        "billingCycle": "Annual"
                    },
                    "pricingPolicies": [
                        {
                            "policyType": "PercentDiscount",
                            "value": "0.05"
                        }
                    ]
                }
            ]
        }
```
