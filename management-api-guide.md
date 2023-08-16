---
title: Management API guide
sidebar_label: API guide
sidebar_position: 1
pagination_next: null
pagination_prev: null
---

# API guide

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

| Endpoint (without `/management/v1/`)                              | Description                                           | Status            | 
| -------------------------------------- | ----------------------------------------------------- | ----------------- |
| Merchants: | | |
| [`GET:/merchants`](https://developer.vippsmobilepay.com/api/management/#tag/Merchants/operation/getAllMerchants) | [Get all merchants](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-all-merchants). | 💡 Idea/proposal |
| [`GET:/merchants/{orgno}`](https://developer.vippsmobilepay.com/api/management/#tag/Merchants/operation/getMerchant) | [Get one merchant by organization number](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-one-merchant-by-organization-number). | 🟡  Available in Q3 |
| [`GET:/merchants/{orgno}/contracts`](https://developer.vippsmobilepay.com/api/management/#tag/Merchants/operation/getMerchantContracts) | [Get a merchant's contract(s)](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-a-merchants-contracts). | 💡 Idea/proposal |
| [`GET:/merchants/{orgno}/sales-units`](https://developer.vippsmobilepay.com/api/management/#tag/Merchants/operation/getMerchantSalesUnits) | [Get the sales units for a merchant by orgno](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-the-sales-units-for-a-merchant-by-orgno). | ✅ Available |
| Sales units: | | |
| [`GET:/sales-units`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/getAllSalesUnits) | [Get all sales units](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-all-sales-units). | 💡 Idea/proposal |
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

### Future improvements

Future versions of the API will _probably_ return more information,
and we will work with our partners to find out what is useful and possible.
Some candidates:

* Company address
* Contact information for the main person (depends on GDPR, etc.)
* Contact information for the technical person (depends on GDPR, etc.)
* A list of people with admin rights on [portal.vipps.no](https://portal.vipps.no) (depend on GDPR, etc.)
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

For partners using
[partner keys](https://developer.vippsmobilepay.com/docs/partner/partner-keys):
Get a (long) list of all sales units registered with the partner making the API call,
containg sales units that are active for a merchant that is active.

[`GET:/management/v1/sales-units/v1/merchants`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/getAllSalesUnits)

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
[`GET:/management/v1/sales-units/v1/merchants/{msn}`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/getMsn)
to get each MSN's details, including the orgno of the merchant it belongs to.

## Get information about a sales unit

Status: Available.

This endpoint is for retrieving details about one sales unit (MSN), but only
when the merchant is active and the sales unit is active.
If the merchant is not active, or the sales unit is not active, the response
will be a `HTTP 404 Not Found` error.

[`GET:/management/v1/sales-units/v1/merchants/{msn}`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/getMsn)

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

* Vipps products: Which Vipps products and APIs are available for this MSN ("eCom API", "Recurring API", "Login API", etc.).
* Transaction cost (price package)
* Status: Active or deactivated

## Update sales unit

Status: Idea/proposal.

May be used to update a sales unit, for instance the name or the status.

[`PATCH:/management/v1/sales-units/v1/merchants/{msn}`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/updateMsn)

Example `PATCH` request body:

```json
{
  "name": "ACME Fantastic Fitness DeLuxe",
  "status": "ACTIVE"
}
```

## Pre-fill a product order

Status: Available.

This endpoint allows a partner or a merchant (typically, a large company with subsidiaries)
to "pre-fill" the product order form on
[portal.vipps.no](https://portal.vipps.no),
on behalf of a merchant.
This makes it possible to ensure that all the data in the form is correct,
including parameters that are normally selectable.

For example, a partner can send a link which allows a merchant to sign up with pre-filled information.
This can also include pre-filled information about sales units which will be created and be ready to use.

The merchant can log in, check the data, and submit the pre-filled product order.

### Request

Here is a sample request to
[`POST:/management/v1/products/orders`](https://developer.vippsmobilepay.com/api/management/#tag/Product-orders/operation/orderProduct):

```json
{
  "businessIdentifier": {
    "scheme": "business:NO:ORG",
    "id": "9876543221"
  },
  "salesUnitName": "ACME Fantastic Fitness",
  "salesUnitLogo": "VGhlIGltYWdlIGdvZXMgaGVyZQ==",
  "settlementAccountNumber": "86011117947",
  "pricePackageId": "8a11afb7-c223-48ed-8ca6-4722b97261aa",
  "productType": "VIPPS_PA_NETT",
  "productUseCase": "WebsiteWithTest",
  "annualTurnover": 100000,
  "intendedPurpose": "Gym membership for accessing the gym's facilities.\nGuest will be not physically present when buying the subscription,\nas that is done on the gym's website.",
  "website": {
    "url": "https://example.com",
    "termsUrl": "https://example.com/terms-and-conditions",
    "testWebsiteUrl": "https://example.com/test ",
    "testWebsiteUsername": "test-user",
    "testWebsitePassword": "test-password"
  },
  "complianceData": {
    "giftCard": {
      "isSalesPercentageLessThanTen": false,
      "validityDuration": "3 years",
      "giftCardTurnoverShare": "about 25%"
    },
    "membership": {
      "turnoverShare": "about 25%",
      "membershipValidity": "CurrentCalendarYear",
      "periodDistribution": "50% yearly 20% monthly"
    },
    "subscription": {
      "turnoverShare": "about 25%",
      "periodDistribution": "50% yearly 20% monthly"
    },
    "course": {
      "turnoverShare": "about 25%",
      "timeBeforeOrder": "10 days",
      "period": "once every 6. week",
      "isOnlineCourseOffered": false,
      "onlineAccessibleTime": "for 3 months"
    },
    "ticket": {
      "turnoverShare": "about 25%",
      "prepurchaseTime": "10 weeks"
    },
    "rent": {
      "turnoverShare": "about 25%",
      "prepurchaseTime": "15 days",
      "averageRentalDuration": "3 weeks"
    },
    "prepaidServices": {
      "turnoverShare": "about 25%",
      "prepurchaseTime": "10 weeks"
    },
    "donation": {
      "acceptsDonation": false
    }
  }
}
```

**Important:** Please provide all the required fields, so it will not be necessary for
merchants to request more details. This is the most
[typical reason for delays](https://developer.vippsmobilepay.com/docs/partner/#typical-reasons-for-delays).

We have made as many of the fields as possible optional, but please
try to send as much as possible, to make it easy for the merchant

**Please note:** The merchant can not change the information provided by the partner, so if
something needs to be corrected, the merchant must contact the partner to have
the partner submit a new pre-fill product order with the correct details.

### Response

Response:

```json
{
  "prefilledOrderId": "81b83246-5c19-7b94-875b-ea6d1114f099",
  "prefillUrl": "https://portal.vipps.no/register/vippspanett/81b83246-5c19-7b94-875b-ea6d1114f099"
}
```

### Processing of the pre-filled product order

When the submitted product order has been processed, an email is sent to both the
partner/merchant making the request and the merchant that submitted the pre-filled product order.
This will include information about:

* The merchant's organization number
* The merchant's name
* The sales unit's MSN
* The sales unit's name

### About "Product Order" (PO) and "Merchant Agreement" (MA)

Merchants must have both a valid Merchant Agreement (MA) and an approved
Product Order (PO) to be able to use Vipps products.

* MA: An agreement between the merchant and Vipps, signed with BankID.
  The MA contains information about all direct and indirect owners, any
  politically exposed persons, etc.
* PO: This is an order for "Vipps på nett", "Vipps Login", etc. The merchant
  must provide some information about the use, whether the cardholder is
  present, etc. The PO is not signed with BankID.
  A merchant may have several Vipps products, each created with a separate PO.

A merchant may order a Vipps product (submit a product order, "PO") with or
without an existing Merchant Agreement ("merchant agreement", "MA").

Both MA and PO are described in detail in
[Scenarios](#scenarios).

### Sequence diagram for pre-fill

PO: Product order. MA: Merchant agreement.

```mermaid
sequenceDiagram
    participant Partner/Merchant
    participant Merchant
    participant Portal
    participant API
    participant Vipps
    Partner/Merchant->>API: POST:/products-orders
    API->>Partner/Merchant: URL to pre-filled signup form
    Partner/Merchant->>Merchant: Here is your pre-filled form on Portal
    Merchant->>Portal: Logs in with BankID and accesses form
    Portal->>API: Requests pre-filled data
    Portal->>Portal: Validate MA and pre-fill request?
    opt Invalid pre-fill request
        Portal-->>Merchant: Show warning
    end
    opt Merchant does not have a Merchant Agreement (MA)
        Portal-->>Merchant: Show information and navigation to the MA form
        Merchant-->>Portal: Fill out MA
        Portal-->>Vipps: MA is sent for processing
        Merchant->>Portal: Re-access pre-filled form
    end
    API->>Portal: Provides pre-filled data
    Portal->>Merchant: Show pre-filled form
    Merchant->>Portal: Submit form
    Portal->>Vipps: PO is sent for processing
    Vipps->>Vipps: Processing
    opt Vipps requires additional information
        Vipps->>Merchant: Sometimes: Ask for additional information
        Merchant->>Vipps: Sometimes: Provide additional information
    end
    Vipps->>Merchant: Email with MSN and other details
    Vipps->>Partner/Merchant: Email with MSN and other details
```

### Scenarios

**Please note:** The only method Vipps has to verify that a user has the right
to sign a merchant agreement for a merchant is by using data from
[Brønnøysundregistrene](https://brreg.no).
It is therefore a requirement that the user logging in on
[portal.vipps.no](https://portal.vipps.no)
is registered as chairman of the board ("styreleder") or CEO ("daglig leder").
The user will then automatically be presented with the pre-filled PO.

#### Scenario 1: The merchant does not have a Merchant Agreement

1. The partner/merchant pre-fills the PO using
   [`POST:/management/v1/products-orders`](https://developer.vippsmobilepay.com/api/partner#tag/Vipps-Product-Orders/operation/orderProduct)
   and gets a link to the pre-filled PO on
   [portal.vipps.no](https://portal.vipps.no).
2. The merchant uses the link and logs in with BankID on
   [portal.vipps.no](https://portal.vipps.no).
3. The merchant is presented with a page informing them that they need to
   sign an MA before filling in the PO.
4. The merchant re-uses the link or finds the link to the pre-filled form on the
   front page on
   [portal.vipps.no](https://portal.vipps.no)
   and is presented with the pre-filled PO,
   checks the details in the PO and submits it.
5. Vipps processes the PO and sends both the merchant and partner/merchant who made the pre-fill request an
   email when done. The partner/merchant who made the pre-fill request can also check with the API:
   [`GET:/management/v1/merchants/{orgno}`](https://developer.vippsmobilepay.com/api/partner#tag/Merchants/operation/getMerchant).

When using the pre-fill link without a valid MA:
![Screenshot from using link without MA](images/screenshot_without_ma.png)

The most important part of the MA form is the "reelle rettighetshavere"
("real rights holders"), meaning the people with direct or direct ownership or
rights for the company. This is not something the partner can be expected to
know, and in any case this is information that must be signed with BankID by a
person that has signatory rights for the merchant. The form looks like this:

![Screenshot from the MA form](images/merchant-agreement-form.png)

#### Scenario 2: The merchant has an active or processing Merchant Agreement

The merchant has an MA, and probably also a Vipps product.

1. The partner/merchant pre-fills the PO using
   [`POST:/management/v1/products/orders`](https://developer.vippsmobilepay.com/api/partner#tag/Vipps-Product-Orders/operation/orderProduct)
   and gets a link to the pre-filled PO on
   [portal.vipps.no](https://portal.vipps.no).
2. The merchant uses the link and logs in with BankID on
   [portal.vipps.no](https://portal.vipps.no).
3. The merchant is presented with the pre-filled PO,
   checks the details in the PO and submits it.
4. Vipps processes the PO and sends both the merchant and partner/merchant an
   email when done.
   The partner/merchant who made the pre-fill request can also check with the API:
   [`GET:/management/v1/merchants/{orgno}`](https://developer.vippsmobilepay.com/api/partner#tag/Merchants/operation/getMerchant).

### Future improvements

* We may allow the merchant to change some data pre-filled by the
  partner, but this is not trivial. If the merchant changes any data, the
  partner must be notified and also get the updated data - then merge and sync that
  with the "old" data that was sent in the first place.

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
   "level": "Vipps Partner Premium",
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

This will make monitoring the usage of Vipps MobilePay's API easier.

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

**Please note:** Monitoring API errors, and fixing them quickly is already a requirement in
the checklists for all APIs, such as:

* [ePayment API checklist](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/checklist/)
* [Recurring API checklist](https://developer.vippsmobilepay.com/docs/APIs/recurring-api/vipps-recurring-api-checklist/)

See also:
[Errors](https://developer.vippsmobilepay.com/docs/common-topics/errors/).
