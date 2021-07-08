---
title: Get a list of products (by country)
description: You can use the Product resource to get a collection of products by customer country.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: amitravat
ms.author: amrava
---

# Get a list of products (by country)

**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

You can use the following methods to get a collection of products available in a particular country.

## Prerequisites

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.

- A country.

## C\#

To get a list of products:

1. Use your **IAggregatePartner.Products** collection to select the country by using the **ByCountry()** method.

2. Select the catalog view using the **ByTargetView()** method.

3. (Optional) Select the reservation scope using the **ByReservationScope()** method.

4. (Optional) Select the target segment using the **ByTargetSegment()** method.

5. Call the **Get()** or **GetAsync()** method to return the collection.

```csharp
IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").Get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").ByTargetSegment("commercial").Get();

// Get the products for Azure reservations which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").Get();

// Get the products for Azure reservations which are applicable to Azure plans only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").ByReservationScope("AzurePlan").Get();

```

## Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

To get a list of products:

1. Use your **IAggregatePartner.getProducts** function to select the country by using the **byCountry()** function.

2. Select the catalog view using the **byTargetView()** function.
3. (Optional) Select the target segment using the **byTargetSegment()** function.

4. Call the **get()** function to return the collection.

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

To get a list of products:

1. Execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command.

2. Select the catalog by specifying the **Catalog** parameter.
3. (Optional) Select the target segment by specifying the **Segment** parameter.

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## REST request

### Request syntax

| Method  | Request URI                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1 |

#### URI parameters

Use the following path and query parameters to get a list of products.

| Name                   | Type     | Required | Description                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| country                | string   | Yes      | The country/region ID.                                                  |
| targetView             | string   | Yes      | Identifies the target view of the catalog. The supported values are: <br/><br/>**Azure**, which includes all Azure items<br/><br/>**AzureReservations**, which includes all Azure reservation items<br/><br/>**AzureReservationsVM**, which includes all virtual machine (VM) reservation items<br/><br/>**AzureReservationsSQL**, which includes all SQL reservation items<br/><br/>**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items<br/><br/>**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans<br/><br/>**OnlineServices**, which includes all online service items (including commercial marketplace products)<br/><br/>**Software**, which includes all software items<br/><br/>**SoftwareSUSELinux**, which includes all software SUSE Linux items<br/><br/>**SoftwarePerpetual**, which includes all perpetual software items<br/><br/>**SoftwareSubscriptions**, which includes all software subscription items    |
| targetSegment          | string   | No       | Identifies the target segment. The view for different target audiences. The supported values are: <br/><br/>**commercial**<br/>**education**<br/>**government**<br/>**nonprofit**  |
| reservationScope | string   | No | When querying for a list of products for Azure Reservations, specify `reservationScope=AzurePlan` to get a list of products that are applicable to Azure plans. Exclude this parameter to get a list of products for Azure reservations, which are applicable to Microsoft Azure (**MS-AZR-0145P**) subscriptions.  |

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None.

### Request examples

#### Products by country

Follow this example to get a list of products by country for Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### Azure VM reservations (Azure plan)

Follow this example to get a list of products by country for Azure VM reservations that are applicable to Azure plans.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### Azure VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions

Follow this example to get a list of products by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## REST response

If successful, the response body contains a collection of [**Product**](product-resources.md#product) resources.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).

This method returns the following error codes:

| HTTP Status Code     | Error code   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | Access to the requested targetSegment is not allowed.                                                     |
| 403                  | 400036       | Access to the requested targetView is not allowed.                                                        |

### Response example

```http
{
    "totalCount": 19,
    "items": [
        {
            "id": "DZH318Z0BQ3Q",
            "title": "Virtual Machines DSv2 Series",
            "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
            "productType": {
                "id": "Azure",
                "displayName": "Azure",
                "subType": {
                "id": "VirtualMachines",
                "displayName": "VirtualMachines"
                }
            },
            "isMicrosoftProduct": true,
            "publisherName": "Microsoft",
            "links": {
                "skus": {
                    "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ3Q?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        ...
    ],
    "links": {
        "self": {
            "uri": "/products?country=US&targetView=Azure",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
