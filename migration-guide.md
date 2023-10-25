---
title: Migrating to the Management API
sidebar_label: Migration guide
sidebar_position: 90
description: Migration to the Management API from Partner API
pagination_next: null
pagination_prev: null
---

# Migration to the Management API from Partner API

It is easy to migrate from the [Partner API](https://developer.vippsmobilepay.com/docs/APIs/partner-api/).
Just update the following three endpoint paths.

## Get merchant by organization number (now business identifier)

Replace `GET:/partner-api/v0/merchants/{orgno}` with
[`GET:/management/v1/merchants/{scheme}/{id}/sales-units`](https://developer.vippsmobilepay.com/api/management/#tag/Merchants/operation/getMerchantSalesUnits).

* The `orgno` field is now called `id`. For Norwegian companies, this is the organization number.
* The `scheme` field. This is used for identifying a merchant. For Norwegian companies, this is always `business:NO:ORG`.

See [Get the sales units for a merchant by business identifier](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-the-sales-units-for-a-merchant-by-business-identifier).

## Get sales unit by merchant serial number

Replace `GET:/partner-api/v0/salesunits/{msn}/` with
[`GET:/management/v1/sales-units/{msn}/`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/getMsn).

* The `msn` field is the same as before - the Merchant Serial Number for the sales unit.

See [Get information about a sales unit](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#get-information-about-a-sales-unit).

## Order products on behalf of merchants

Replace `POST:/partner-api/v1/products/orders` with
[`POST:/management/v1/product-orders`](https://developer.vippsmobilepay.com/api/management/#tag/Product-orders).

 See [Pre-fill a product order](https://developer.vippsmobilepay.com/docs/APIs/management-api/management-api-guide/#pre-fill-a-product-order).
