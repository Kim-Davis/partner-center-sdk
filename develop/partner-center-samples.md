---
title: Partner Center samples
description: To help you get up and running quickly with the Partner Center APIs, we provide a sample program, C\ managed code snippets, and REST sample requests and responses.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: cychua
ms.author: cychua
---

# Partner Center samples

**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

To help you get up and running quickly with the Partner Center APIs, we provide a sample program, C# managed code snippets, and REST sample requests and responses.

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<table>
  <thead>
    <th>Sample</th>
    <th>Details</th>
  </thead>
  <tbody>
    <tr>
      <td>Code snippets</td>
      <td>For pointers and .NET, Java, and PowerShell code snippets that show how to use the Partner Center managed API to manage customer accounts, get analytics, place orders, manage billing and subscriptions, provide support, and manage accounts and profiles, see <a href="scenarios.md">Scenarios</a>.</td>
    </tr>
    <tr>
      <td>REST samples</td>
      <td>For sample requests and responses that show how to use the Partner Center REST API to manage customer accounts, get analytics, place orders, manage billing and subscriptions, provide support, and manage accounts and profiles, see <a href="scenarios.md">Scenarios</a>.</td>
    </tr>
    <tr>
      <td><a href="console-test-app.md">Console test app</a></td>
      <td>This app is available in C# and Java, it provides code and some error handling for all of the scenarios listed in the scenarios section.</td>
    </tr>
    <tr>
      <td><a href="csp-customer-web-storefront.md">CSP customer web storefront</a></td>
      <td>This site shows a working online store that your customers could use to buy subscriptions to Microsoft products. You can easily create a website for your company with the <a href="csp-customer-storefront-builder-quick-start-guide-.md">CSP Customer Storefront Builder Quickstart Guide</a>.</td>
    </tr>
    <tr>
      <td>Store web site</td>
      <td><p><strong>Description:</strong></p>
          <p>This application shows how to build a web store based on the catalog of offers available to Cloud Solution Provider partners. Customers can create a store account and order software subscriptions through your site.</p>
        <p><strong>Get the code:</strong></p>
        <p><a href="https://go.microsoft.com/fwlink/p/?LinkId=746683">Download the sample code</a></p>
        <p><strong>What to configure before release:</strong></p>
        <ul>
          <li><p>Authentication: App ID & secret.</p></li>
          <li><p>Branding: logo and company name.</p></li>
          <li><p>Welcome message.</p></li>
          <li><p>Offers, including descriptions and prices. The app assumes that the list prices include any applicable taxes. Alternatively, you can add additional logic to calculate tax during checkout.</p></li>
          <li><p>Payment information: provide your own credit card options, PayPal, or other payment types. Before you configure this part, please read the guide <a href="/partner-center/non-payment-fraud-misuse">Non-payment, fraud, or misuse</a>.</p></li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>