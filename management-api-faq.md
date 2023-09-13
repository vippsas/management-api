---
title: Management API Frequently Asked Questions
sidebar_label: FAQ
sidebar_position: 45
description: Frequently asked questions for the Management API.
pagination_next: null
pagination_prev: null
---

# Frequently asked questions

See the
[Management API Guide](management-api-guide.md)
for all the technical details, and
[Partners](https://developer.vippsmobilepay.com/docs/partner/)
for all partner information.

See also:
* [Common API FAQ](https://developer.vippsmobilepay.com/docs/faqs).
* [Vipps MobilePay Getting Started guide](https://developer.vippsmobilepay.com/docs/getting-started).

<!-- START_COMMENT -->

ℹ️ Please use the website:
[Vipps MobilePay Technical Documentation](https://developer.vippsmobilepay.com/).

<!-- END_COMMENT -->

## When will the Management API be available?

It's available now. We are continuously improving it, and have documented both existing functionality
and upcoming functionality. 

## How can I get access?

See:[Integrating with this API](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#integrating-with-this-api).

## What will be included in the initial version?

See the
[API guide](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/)
and
[API spec](https://developer.vippsmobilepay.com/api/management/)
for the status of each endpoint.

## What are the benefits of the Management API over the Partner API?

* The Management API contains everything the
  [Partner API](https://developer.vippsmobilepay.com/docs/APIs/partner-api/) does, and more.
* The Management API is actively developed, the Partner API will be phased out.
* Both APIs use the same API keys.
* The endpoints are practically identical, with the Management API endpoints offering better
  error handling, more detailed responses, etc.
* The
  [Pre-fill a product order](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#pre-fill-a-product-order)
  endpoint in the Management API will give an error if the partner sends incorrect or invalid data.
  In the Partner API the error will not be discovered until the merchant attempts to use the URL
  to the incorrectly submitted pre-filled product order.  

## How can I make feature requests and give input for the Management API?

Contact your partner manager or key account manager.

## Will there be a partner portal?

It is not possible for partners to sign in on
[portal.vipps.no](https://portal.vipps.no)
_as partners_, but merchants may give access to individual users
as described here:
[How to add a user on portal.vipps.no](https://developer.vippsmobilepay.com/docs/partner/add-portal-user/).

Allowing partners to log in on
[portal.vipps.no](https://portal.vipps.no)
_as partners_ is not possible,
and there is no decision or concrete plan to implement the required functionality.

The Management API is our priority and our aim is to offer as much functionality for partners
as possible.

## How can I check the status of a merchant's product order?

See:
[How to check if a merchant is signed up with the partner as partner](https://developer.vippsmobilepay.com/docs/partner/#how-to-check-if-a-merchant-is-signed-up-with-the-partner-as-partner).

## Where do I get the `pricePackageId`?

The `pricePackageId` is a UUID, and you get it by email when you are activated as partner.
A UUID has a format like this: `81b83246-5c19-7b94-875b-ea6d1114f099`.

Use
[`GET:/partners/{partner-id}/price-packages`](https://developer.vippsmobilepay.com/api/management/#tag/Partners/operation/getPartnerPricePackages)
to retrieve your price packages.

## Can I use the Management API in the test environment?

Nope. We do not have all the required backend systems available in the test
environment. See
[Limitations of the test environment](https://developer.vippsmobilepay.com/docs/test-environment/#limitations-of-the-test-environment).

## Why is the URL for a pre-filled product order not working?

It is probably because the pre-fill request was invalid.

If you send an invalid request to
[`/management/v1/product-orders`](https://developer.vippsmobilepay.com/api/management/#tag/Product-orders/operation/orderProduct),
the pre-fill will _in most cases_ fail with an error message.

Although we do as much input validation as possible, it is not possible to validate all data, so in some cases the
pre-fill request will succeed, and the pre-fill URL will lead to an empty product order form.

## Why do I get `HTTP 404 Not Found`?

It depends on which request has been made.
Partners will get this error if they attempt to retrieve data for a merchant that does not yet have
an active sales unit connected with the partner.

See:
[How to check if a merchant is signed up with the partner as partner](https://developer.vippsmobilepay.com/docs/partner#how-to-check-if-a-merchant-is-signed-up-with-the-partner-as-partner).

## When will it be possible to update an existing sales unit?

We are working on this now, as fast as we can!
We know this is a very important feature, but can't give you a release date yet.

See
[Endpoints and availability](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#endpoints-and-availability).
The documentation will be updated as soon as we have new information.

We recommend subscribing to the
[Technical newsletter for developers](https://developer.vippsmobilepay.com/docs/newsletters).
