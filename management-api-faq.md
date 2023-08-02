---
title: Management API Frequently Asked Questions
sidebar_label: FAQ
sidebar_position: 45
description: Frequently asked questions for the Management API.
pagination_next: null
pagination_prev: null
---

# Frequently asked questions

💥
**DRAFT!** The Management API is in development, but not yet available.
This documentation is a working document, and used in discussions with
merchants and partners to make sure we are prioritizing right,
and that we are implementing the right functionality.
The Management API will replace the
[Partner API](https://developer.vippsmobilepay.com/docs/APIs/partner-api/).
💥

See the
[Management API Guide](management-api-guide.md)
for all the technical details.

See also:
[Common API FAQ](https://developer.vippsmobilepay.com/docs/faqs).

See also:
[Vipps MobilePay Getting Started guide](https://developer.vippsmobilepay.com/docs/getting-started).

<!-- START_COMMENT -->

ℹ️ Please use the website:
[Vipps MobilePay Technical Documentation](https://developer.vippsmobilepay.com/).

<!-- END_COMMENT -->

## When will the Management API be available?

We're aiming for August.

## What will be included in the initial version?

See the API guide and API specification for the status of each endpoint.

## How can I make feature requests and give input?

Contact your partner manager or key account manager.

## Where do I get the pricePackageId?

The `pricePackageId` is a UUID, and you get it by email when you are activated as partner.
A UUID has a format like this: 81b83246-5c19-7b94-875b-ea6d1114f099.

Use
[`GET:/partners/{partner-id}/price-packages`](https://developer.vippsmobilepay.com/api/management/#tag/Partners/operation/getPartnerPricePackages)
to retrieve your price packages.

## Can I use the Management API in the test environment?

Nope. We do not have all the required backend systems available in the test
environment. See
[Limitations of the test environment](https://developer.vippsmobilepay.com/docs/test-environment/#limitations-of-the-test-environment).

## Why is the URL for a pre-filled product order not working?

If you send an invalid request to
[`POST:/products/orders`](https://developer.vippsmobilepay.com/api/management#tag/Vipps-Product-Orders/operation/orderProduct),
the pre-fill will fail, and the URL will lead to the standard, empty
product order form. Although we do _some_ input validation, it is not possible
to validate all data.

## Why do I get `HTTP 404 Not Found`?

Partners will get this error if the merchant does not yet have an active sales unit connected with the partner.

See:
[How to check if a merchant is signed up with the partner as partner](https://developer.vippsmobilepay.com/docs/partner#how-to-check-if-a-merchant-is-signed-up-with-the-partner-as-partner).

## When will it be possible to change an existing sales unit?

We are working on this now, as fast as we can!
We know this is a very important feature, but can't give you a release date yet.
The documentation will be updated as soon as we have new information.

We recommend subscribing to the
[Technical newsletter for developers](https://developer.vippsmobilepay.com/docs/newsletters).
