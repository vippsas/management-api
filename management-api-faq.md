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

The Vipps MobilePay Management API lets partners and merchants manage their sales units, etc.

See the
[Management API Guide](management-api-guide.md)
for all the technical details.

See also:
[Common API FAQ](https://developer.vippsmobilepay.com/docs/vipps-developers/faqs).

See also:
[Vipps MobilePay Getting Started guide](https://developer.vippsmobilepay.com/docs/vipps-developers/getting-started)
guide.

<!-- START_COMMENT -->

ℹ️ Please use the website:
[Vipps MobilePay Technical Documentation](https://developer.vippsmobilepay.com/).

## Table of contents

* [Where do I get the pricePackageId?](#where-do-i-get-the-pricepackageid)
* [Can I use the Management API in the test environment?](#can-i-use-the-partner-api-in-the-test-environment)
* [Why is the URL for a pre-filled product order not working?](#why-is-the-url-for-a-pre-filled-product-order-not-working)
* [Why do I get `HTTP 404 Not Found`?](#why-do-i-get-http-404-not-found)
* [When will it be possible to change an existing sales unit?](#when-will-it-be-possible-to-change-an-existing-sales-unit)

<!-- END_COMMENT -->

## Where do I get the pricePackageId?

The `pricePackageId` is a UUID, and you get it when you are activated as partner.
If you have lost it, please search in your email.
If you can not find it, please see
[Questions](https://developer.vippsmobilepay.com/docs/vipps-partner#questions)
at the bottom of
[Partners](https://developer.vippsmobilepay.com/docs/vipps-partner).

A UUID has a format like this: 81b83246-5c19-7b94-875b-ea6d1114f099.

## Can I use the Management API in the test environment?

Nope. We do not have all the required backend systems available in the test
environment.

## Why is the URL for a pre-filled product order not working?

If you send an invalid request to
[`POST:/products/orders`](https://developer.vippsmobilepay.com/api/management#tag/Vipps-Product-Orders/operation/orderProduct)
the pre-fill will fail, and the URL will lead to the standard, empty
product order form. Although we do _some_ input validation, it is not possible
to validate all data.

## Why do I get `HTTP 404 Not Found`?

You will get this error for requests to
[`GET:/merchants/{orgno}`](https://developer.vippsmobilepay.com/api/management#tag/Merchants/operation/getMerchant)
if the merchant does not yet have an active sales unit with you as partner.

See:
[How to check if a merchant is signed up with the partner as partner](https://developer.vippsmobilepay.com/docs/vipps-partner#how-to-check-if-a-merchant-is-signed-up-with-the-partner-as-partner).

## When will it be possible to change an existing sales unit?

We are working on this now, as fast as we can!
We know this is a very important feature, but can't give you a release date yet.
The documentation will be updated as soon as we have new information.

We recommend subscribing to the
[Technical newsletter for developers](https://developer.vippsmobilepay.com/docs/vipps-developers/newsletters).
