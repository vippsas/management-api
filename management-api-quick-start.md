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

This document covers the quick steps for getting started with the Management API.
You must have already signed up as an organization with Vipps MobilePay and have
your test credentials from the merchant portal, as described in the
[Getting started guide](https://developer.vippsmobilepay.com/docs/getting-started).

**Important:** The examples use standard example values that you must change to
use *your* values. This includes API keys, HTTP headers, reference, etc.

## Get information about your merchant sales units

Be aware that these are running on the production server, <https://api.vipps.no>.

**Important:** Partner keys must be kept secret. They can be used to act on behalf
of all the partner's merchants. It is the partner's responsibility to manage
the partner keys securely. See
[Partner keys](https://developer.vippsmobilepay.com/docs/partner/partner-keys).

### Step 1 - Setup

<Tabs
defaultValue="curl"
groupId="sdk-choice"
values={[
{label: 'curl', value: 'curl'},
{label: 'Postman', value: 'postman'},
]}>
<TabItem value="postman">

**Please note:** Postman is discontinuing their offline version. Use only your test keys and delete them after testing. Ensure that your company allows for cloud use before continuing.

To use Postman, import the following files:

* [Management API Postman collection](/tools/vipps-management-api-postman-collection.json)
* [Vipps API Global Postman environment](https://github.com/vippsas/vipps-developers/blob/master/tools/vipps-api-global-postman-environment.json)

In Postman, tweak the environment with your own values (see
[API keys](https://developer.vippsmobilepay.com/docs/common-topics/api-keys/)):

* `client-id` - Partner key is required for getting the access token.
* `client-secret` - Partner key is required for getting the access token.
* `Ocp-Apim-Subscription-Key` - Partner subscription key is required for all requests.
* `merchantSerialNumber` - Merchant ID is only required for `Get sales unit details based on MSN`, but can be included in all headers.
* `orgno` -The Organization number for the merchant. It is only used in `Get merchant by organization number`.
* `base_url_production` - Set to: `https://api.vipps.no`.

</TabItem>
<TabItem value="curl">

No setup needed :)

</TabItem>
</Tabs>

### Step 2 - Authentication

For all the following, you will need an `access_token` from the
[Access token API](https://developer.vippsmobilepay.com/docs/APIs/access-token-api):
[`POST:/accesstoken/get`](https://developer.vippsmobilepay.com/api/access-token#tag/Authorization-Service/operation/fetchAuthorizationTokenUsingPost).
This provides you with access to the API.

Note to use the address to the *production* server and provide keys for a *production* sales unit.

<Tabs
defaultValue="curl"
groupId="sdk-choice"
values={[
{label: 'curl', value: 'curl'},
{label: 'Postman', value: 'postman'},
]}>
<TabItem value="postman">

```bash
Send request Get Access Token
```

</TabItem>
<TabItem value="curl">

```bash
curl https://api.vipps.no/accessToken/get \
-H "client_id: YOUR-CLIENT-ID" \
-H "client_secret: YOUR-CLIENT-SECRET" \
-H "Ocp-Apim-Subscription-Key: YOUR-SUBSCRIPTION-KEY" \
-H "Merchant-Serial-Number: 123456" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-X POST \
--data ''
```

</TabItem>
</Tabs>

The property `access_token` should be used for all other API requests in the `Authorization` header as the Bearer token.

### Step 3 - Get merchant sales units by organization number

Send request
[`GET:v1/merchants/{orgno}/sales-units`](https://developer.vippsmobilepay.com/api/management/#tag/Merchants/operation/getMerchantSalesUnits),
where `orgno` is the organization number of the sales unit.
Details about the merchant will be provided.

<Tabs
defaultValue="curl"
groupId="sdk-choice"
values={[
{label: 'curl', value: 'curl'},
{label: 'Postman', value: 'postman'},
]}>
<TabItem value="postman">

```bash
Send request Get merchant by organization number
```

</TabItem>
<TabItem value="curl">

```bash
curl https://api.vipps.no/management/v1/merchants/{orgno}/sales-units \
-H "Content-Type: application/json" \
-H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1Ni <truncated>" \
-H "Ocp-Apim-Subscription-Key: 0f14ebcab0ec4b29ae0cb90d91b4a84a" \
-H "Vipps-System-Name: acme" \
-H "Vipps-System-Version: 3.1.2" \
-H 'Vipps-System-Plugin-Name: vipps-postman' \
-H 'Vipps-System-Plugin-Version: 2.0' \
-X GET
```

</TabItem>
</Tabs>

Take note of the merchant serial numbers and use one of these in the next step.

### Step 4 - Get sales unit by Merchant Serial Number

Send request
[`GET:v1/sales-units/{msn}/`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/getAllSalesUnits), where `msn` is the Merchant Serial Number.

This returns a JSON structure with the details, including the org number.

<Tabs
defaultValue="curl"
groupId="sdk-choice"
values={[
{label: 'curl', value: 'curl'},
{label: 'Postman', value: 'postman'},
]}>
<TabItem value="postman">

```bash
Send request Get sales unit details based on MSN
```

If necessary, update `msn` in the environment.

</TabItem>
<TabItem value="curl">

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

</TabItem>
</Tabs>


## Next steps

See the [Management API guide](management-api-guide.md) to read about the concepts and details.
