---
title: Management API features
sidebar_label: Features
sidebar_position: 25
pagination_next: null
pagination_prev: null
---

# Features

## Important information

**Please note:**
The Management API replaces the
[Partner API](https://developer.vippsmobilepay.com/docs/APIs/partner-api/):
All the functionality in the Partner API is available in the Management API now,
and more functionality will be added. See each endpoint and the
[API specification](https://developer.vippsmobilepay.com/api/management/)
for details.

## Integrating with this API

Both partners and _soon_ merchants can use the Management API, and we use "partner/merchant" to
indicate that this is the actor making the API request.

Authentication:

* Partners use their [partner keys](https://developer.vippsmobilepay.com/docs/partner/partner-keys)
  if they have them, and the merchant's API keys if not.
* Soon: Merchants use their normal
  [API keys](https://developer.vippsmobilepay.com/docs/common-topics/api-keys/).

See the Postman collection and environment, and the
[Quick start guide](management-api-quick-start.md).
The Postman collection can also be used to manually make API calls,
even without an integration in place.

## Endpoints and availability

| Endpoint | Description | Status |
| -------- | ----------- | ------ |
| Merchants: | | |
| [`GET:/merchants`](https://developer.vippsmobilepay.com/api/management/#tag/Merchants/operation/getAllMerchants) | [Get all merchants](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-all-merchants). | 💡 Idea/proposal |
| [`GET:/merchants/{orgno}`](https://developer.vippsmobilepay.com/api/management/#tag/Merchants/operation/getMerchant) | [Get one merchant by organization number](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-one-merchant-by-organization-number). | 🟡 Available in Q3 |
| [`GET:/merchants/{orgno}/contracts`](https://developer.vippsmobilepay.com/api/management/#tag/Merchants/operation/getMerchantContracts) | [Get a merchant's contract(s)](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-a-merchants-contracts). | 💡 Idea/proposal |
| [`GET:/merchants/{orgno}/sales-units`](https://developer.vippsmobilepay.com/api/management/#tag/Merchants/operation/getMerchantSalesUnits) | [Get the sales units for a merchant by orgno](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-the-sales-units-for-a-merchant-by-orgno). | ✅ Available |
| Sales units: | | |
| [`GET:/sales-units`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/getAllSalesUnits) | [Get all sales units](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-all-sales-units). | 🟡 Available in Q4 |
| [`GET:/sales-units/{msn}`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/getMsn) | [Get information about a sales unit](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-information-about-a-sales-unit). | ✅ Available |
| [`PATCH:/sales-units/{msn}`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/updateMsn) | [Update sales unit](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#update-sales-unit). | 💡 Idea/proposal |
| Product orders: | | |
| [`POST:/products/orders`](https://developer.vippsmobilepay.com/api/management/#tag/Product-orders/operation/orderProduct) | [Pre-fill a product order](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#pre-fill-a-product-order). | ✅ Available |
| [`GET:/product-orders/{product-order-id}`](https://developer.vippsmobilepay.com/api/management/#tag/Product-orders/operation/productOrderDetails) | [Get information about a product order](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-information-about-a-product-order). | 💡 Idea/proposal |
| [`DELETE:/product-orders/{product-order-id}`](https://developer.vippsmobilepay.com/api/management/#tag/Product-orders/operation/deleteProductOrder) | [Delete a product order](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#delete-a-product-order). | 💡 Idea/proposal |
| Partners: | | |
| [`GET:/partners/whoami`](https://developer.vippsmobilepay.com/api/management/#tag/Partners/operation/getPartnerWhoami) | [Get information about a partner](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-information-about-a-partner).  |💡 Idea/proposal |
| [`GET:/partners/price-packages`](https://developer.vippsmobilepay.com/api/management/#tag/Partners/operation/getPartnerPricePackages) | [Get the price packages for a partner](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-the-price-packages-for-a-partner). | ✅ Available |
| API quality: | | |
| [`GET:/api-quality/sales-units/{msn}`](https://developer.vippsmobilepay.com/api/management/#tag/API-quality) | [API quality](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#api-quality). | 💡 Idea/proposal |

## Get all merchants

Status: Idea/proposal.

For partners using
[partner keys](https://developer.vippsmobilepay.com/docs/partner/partner-keys):
Get a (long) list of all `orgno`s that have one or more sales units registered with the partner making the API call.

[`GET:/management/v1/merchants`](https://developer.vippsmobilepay.com/api/management/#tag/Merchants/operation/getAllMerchants)

Response:

```json
{
   "MerchantList":[
      {
         "orgno": 987654321,
         "name": "ACME Fantastic Fitness"
      }
      {
         "orgno": 987654322,
         "name": "ACME Fantastic Fitness 2"
      }
   ]
}
```

If this endpoint is used with normal API keys (not partner keys), it will return just one merchant:
The one making the API request.

## Get one merchant by organization number

Status: Available in Q3.

This endpoint is for retrieving basic information about the merchant:

[`GET:/management/v1/merchants/{orgno}`](https://developer.vippsmobilepay.com/api/management/#tag/Merchants/operation/getMerchant)

Response:

```json
{
  "orgno": 987654321,
  "name": "ACME Fantastic Fitness"
}
```

Future versions of the API will _probably_ return more information,
and we will work with our partners to find out what is useful and possible.
Some candidates:

* Company address
* Contact information for the main person (depends on GDPR)
* Contact information for the technical person (depends on GDPR)
* A list of people with admin rights on [portal.vipps.no](https://portal.vipps.no) (depend on GDPR)
* Changelog: What was changed when by whom?


## Get a merchant's contract(s)

Status: Idea/proposal.

Return a (link to a) PDF.

[`GET:/management/v1/merchants/{orgno}/contracts`](https://developer.vippsmobilepay.com/api/management/#tag/Merchants/operation/getMerchantContracts)

Response:

```json
{
  "urls": [
    "https://example.com/contracts/contract-12345.pdf"
  ]
}
```

## Get the sales units for a merchant by orgno

Status: Available.

[`GET:/management/v1/merchants/{orgno}/sales-units`](https://developer.vippsmobilepay.com/api/management/#tag/Merchants/operation/getMerchantSalesUnits)

Response:

```json
[
  "123456",
  "123457"
]
```

## Get all sales units

Status: Idea/proposal.

Get all sales units that a merchant or partner has access to.

For partners using
[partner keys](https://developer.vippsmobilepay.com/docs/partner/partner-keys):
Get a (long) list of all sales units registered with the partner making the API call,
containing sales units that are active for an active merchant.

[`GET:/management/v1/sales-units`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/getAllSalesUnits)

Response:

```json
{
  "msn": [
     "123456",
     "123457"
   ]
}
```

It is then possible to use
[`GET:/management/v1/sales-units/{msn}`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/getMsn)
to get each MSN's details, including the orgno of the merchant it belongs to.

## Get information about a sales unit

Status: Available.

The [`GET:/management/v1/sales-units/{msn}`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/getMsn) endpoint is for retrieving details about one sales unit (MSN), but only
when both the merchant and sales unit are active.
If the merchant is not active, or the sales unit is not active, the response
will be a `HTTP 404 Not Found` error.

[`GET:/management/v1/sales-units/{msn}`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/getMsn)

Response (now):

```json
{
   "msn":"123456",
   "name":"ACME Fantastic Fitness",
   "businessIdentifier":{
      "scheme":"business:NO:ORG",
      "id":"9876543221"
   },
   "configuration":{
      "paymentAllowed":true,
      "captureType":"ReserveCapture",
      "skipLandingPageAllowed":false,
      "recurringAllowed":false
   }
}
```

Response (this improvement is provided for discussions of what we should investigate further):

```json
{
   "msn":"123456",
   "name":"ACME Fantastic Fitness",
   "businessIdentifier":{
      "scheme":"business:NO:ORG",
      "id":"9876543221"
   },
   "configuration":{
      "paymentAllowed":true,
      "captureType":"ReserveCapture",
      "skipLandingPageAllowed":false,
      "recurringAllowed":false,
      "customerMustBePresent":false,
      "userinfoNinAllowed":false,
   }
   "bankDetails": {
      "bankAccountBban":"86011117947",
      "bankAccountIban":"NO93 8601 1117 947",
   },
   "changelog": [
      {
         "timestamp": "2022-12-31T00:00:00Z",
         "change": "MSN created",
         "changedBy":"Vipps MobilePay"
      },
      {
         "timestamp": "2023-01-01T00:00:00Z",
         "change": "skipLandingPage set to true",
         "changedBy": "Merchant, using Management API"
      },
      {
         "timestamp": "2023-11-15T00:00:00Z",
         "change": "NIN allowed",
         "changedBy": "Vipps MobilePay"
      },
      {
         "timestamp": "2023-06-01T00:00:00Z",
         "change": "Updated MSN name",
         "changedBy": "Merchant, using the portal"
      },
   ]   
}
```

The `orgno` is included to make it possible to find out the merchant that is associated with an MSN.
This is useful when only the MSN is known.

Future versions of the API will _probably_ return more information,
and we will work with our partners to find out what is useful and possible.
Some candidates:

* Products: Which products and APIs are available for this MSN ("ePayment API", "Recurring API", "Login API", etc.).
* Transaction cost (price package)
* Status: Active or deactivated

## Update sales unit

Status: Idea/proposal.

May be used to update a sales unit, for instance the name or the status.

[`PATCH:/management/v1/sales-units/{msn}`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/updateMsn)

Example `PATCH` request body:

```json
{
  "name": "ACME Fantastic Fitness DeLuxe",
  "status": "ACTIVE"
}
```

## Pre-fill a product order

Status: Available.

This endpoint allows for "pre-fill" of the product order form on
[portal.vipps.no](https://portal.vipps.no):

[`POST:/management/v1/products/orders`](https://developer.vippsmobilepay.com/api/management/#tag/Product-orders/operation/orderProduct)

Example `POST` request body:

```json
{
  "businessIdentifier": {
    "scheme": "business:NO:ORG",
    "id": "9876543221"
  },
  "salesUnitName": "ACME Fantastic Fitness",
  "settlementAccountNumber": "86011117947",
  "pricePackageId": "8a11afb7-c223-48ed-8ca6-4722b97261aa",
  "productType": "VIPPS_PA_NETT",
  "website": {
    "url": "https://example.com",
    "termsUrl": "https://example.com/terms-and-conditions",
  },
}
```

The response from a pre-fill request contains a URL to
[portal.vipps.no](https://portal.vipps.no).
The merchant simply uses the URL to get to the pre-filled product order, checks the data, and submits.

Response:

```json
{
  "prefilledOrderId": "81b83246-5c19-7b94-875b-ea6d1114f099",
  "prefillUrl": "https://portal.vipps.no/register/vippspanett/81b83246-5c19-7b94-875b-ea6d1114f099"
}
```

See [Order pre-fill](prefill.md) for more details.

## Get information about a product order

Status: Idea/proposal.

For both merchants and partners. The best way to check the status of a product order is on
[portal.vipps.no](https://portal.vipps.no).

We are considering an endpoint like this:

[`GET:/management/v1/product-orders/{product-order-id}`](https://developer.vippsmobilepay.com/api/management/#tag/Product-orders/operation/productOrderDetails)

Response:

```json
{
  "prefilledOrderId": "81b83246-5c19-7b94-875b-ea6d1114f099",
  "prefillStatus": "PROCESSING"
}
```

**Please note:** There are strict rules for what information we are
allowed to share with a partner, as this requires active consent from the merchant,
and the merchant must also be able to withdraw the consent.

## Delete a product order

Status: Idea/proposal.

An "undo" endpoint to delete a PO.
This may be used if an incorrect PO has been pre-filled with
[`POST:/management/v1/product-orders`](https://developer.vippsmobilepay.com/api/management/#tag/Product-orders/operation/orderProduct).

[`DELETE:/management/v1/product-orders/{product-order-id}`](https://developer.vippsmobilepay.com/api/management/#tag/Product-orders/operation/deleteProductOrder)

## Get information about a partner

Status: Idea/proposal.

For partners using
[partner keys](https://developer.vippsmobilepay.com/docs/partner/partner-keys):
Get details for the partner making the request.

[`GET:/management/v1/partners/whoami`](https://developer.vippsmobilepay.com/api/management/#tag/Partners/operation/getPartnerWhoami)

Response:

```json
{
   "partnerId": "123456",
   "name": "ACME Partner Inc",
   "level": "Partner Premium",
   "partnerContactName": "firstName lastName",
   "partnerContactEmail": "firstname.lastname@vippsmobilepay.com",
   "status": "ACTIVE"
}
```

If this endpoint is used with normal API keys (not partner keys), it will return an error.

## Get the price packages for a partner

Status: Available.

Partners can use this endpoint to get a list of all their price packages, with the
`pricePackageId` to use for
[`POST:/management/v1/products/orders`](https://developer.vippsmobilepay.com/api/management/#tag/Product-orders/operation/orderProduct),
as well as other details.

[`GET:/management/v1/partners/price-packages`](https://developer.vippsmobilepay.com/api/management/#tag/Partners/operation/getPartnerPricePackages)

Response:

```json
[
  {
    "pricePackageId": "8a11afb7-c223-48ed-8ca6-4722b97261aa",
    "name": "POS standard",
    "description": "2.99%",
    "visibleInSignupForm": true,
    "productType": "ePayment"
  }
]
```

## API quality

Status: Idea/proposal.

We want to offer an API endpoint that lets merchants and partners retrieve the same
information that is available on the
[API Dashboard](https://developer.vippsmobilepay.com/docs/developer-resources/api-dashboard/).

This will make it easier to monitor usage the API platform.

[`GET:/management/v1/api-quality/sales-units/{msn}`](https://developer.vippsmobilepay.com/api/management/#tag/API-quality)

Response:

```json
{
   "ApiQualityItems":[
      {
         "endpoint":"POST://epayment/v1/payments",
         "total Requests":1000,
         "successRate":95,
         "status200":950,
         "status400":10,
         "status401":10,
         "status403":10,
         "status404":10,
         "status429":10,
         "status500":0
      }
   ]
}
```

**Please note:** Monitoring API errors and fixing them quickly is a requirement in
the checklists for all APIs. For example, see:

* [ePayment API checklist](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/checklist/)
* [Recurring API checklist](https://developer.vippsmobilepay.com/docs/APIs/recurring-api/vipps-recurring-api-checklist/)

See [Errors](https://developer.vippsmobilepay.com/docs/common-topics/errors/) for examples of common errors.
