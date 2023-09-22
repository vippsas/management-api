---
title: Quick start for the Management API
sidebar_label: Quick start
sidebar_position: 20
description: Quick steps for getting started with the Management API.
pagination_next: null
pagination_prev: null
---

import ApiSchema from '@theme/ApiSchema';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Quick start

## Before you begin

Be aware that these are running on the production server, <https://api.vipps.no>.

🔥 **Do not use production keys in Postman.** 🔥

**Important:** Partner keys must be kept secret. They can be used to act on behalf
of all the partner's merchants. It is the partner's responsibility to manage
the partner keys securely. See
[Partner keys](https://developer.vippsmobilepay.com/docs/partner/partner-keys).

The examples use standard example values that you must change to
use *your* values. This includes API keys, HTTP headers, reference, etc.

## Get information about your merchant sales units

### Step 1 - Setup

You must have already signed up as an organization with Vipps MobilePay and have
your test credentials from the merchant portal.

You will need the following values, as described in the
[Getting started guide](https://developer.vippsmobilepay.com/docs/getting-started):

* `client-id` - Partner key is required for getting the access token.
* `client-secret` - Partner key is required for getting the access token.
* `Ocp-Apim-Subscription-Key` - Partner subscription key is required for all requests.
* `merchantSerialNumber` - The unique ID for a test sales unit. Merchant ID is only required for `Get sales unit details based on MSN`, but can be included in all headers.
* `orgno` -The Organization number for the merchant. It is only used in `Get merchant by organization number`.


### Step 2 - Authentication

For all the following, you will need an `access_token` from the
[Access token API](https://developer.vippsmobilepay.com/docs/APIs/access-token-api):
[`POST:/accesstoken/get`](https://developer.vippsmobilepay.com/api/access-token#tag/Authorization-Service/operation/fetchAuthorizationTokenUsingPost).
This provides you with access to the API.

Note to use the address to the *production* server and provide keys for a *production* sales unit.

```bash
curl https://api.vipps.no/accessToken/get \
-H "client_id: YOUR-CLIENT-ID" \
-H "client_secret: YOUR-CLIENT-SECRET" \
-H "Ocp-Apim-Subscription-Key: YOUR-SUBSCRIPTION-KEY" \
-H "Merchant-Serial-Number: YOUR-MSN" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-X POST \
--data ''
```

The property `access_token` should be used for all other API requests in the `Authorization` header as the Bearer token.

### Step 3 - Get merchant sales units by organization number

Send request
[`GET:management/v1/merchants/{scheme}/{id}/sales-units`](https://developer.vippsmobilepay.com/api/management/#tag/Merchants/operation/getMerchantSalesUnits),
where `orgno` is the organization number of the sales unit.
Details about the merchant will be provided.

```bash
curl https://api.vipps.no/management/v1/merchants/{scheme}/{id}/sales-units \
-H "Content-Type: application/json" \
-H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1Ni <truncated>" \
-H "Ocp-Apim-Subscription-Key: 0f14ebcab0ec4b29ae0cb90d91b4a84a" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-H 'Vipps-System-Plugin-Name: vipps-postman' \
-H 'Vipps-System-Plugin-Version: 2.0' \
-X GET
```

Take note of the merchant serial numbers returned and use one of these in the next step.

### Step 4 - Get sales unit by Merchant Serial Number

Send request
[`GET:management/v1/sales-units/{msn}`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/getMsn), where `msn` is the Merchant Serial Number.

This returns a JSON structure with the details, including the org number.

```bash
curl https://api.vipps.no/management/v1/sales-units/{msn} \
-H "Content-Type: application/json" \
-H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1Ni <truncated>" \
-H "Ocp-Apim-Subscription-Key: 0f14ebcab0ec4b29ae0cb90d91b4a84a" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-H 'Vipps-System-Plugin-Name: vipps-postman' \
-H 'Vipps-System-Plugin-Version: 2.0' \
-X GET
```

See [Get information about a sales unit](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-information-about-a-sales-unit) for more information.

## Next steps

See the [Management API guide](management-api-guide.md) to read about the concepts and details.
