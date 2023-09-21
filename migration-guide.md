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
Just change the following three endpoint paths.

## Get merchant by organization number

Replace
[`GET:partner-api/v0/merchants/{orgno}`](https://developer.vippsmobilepay.com/api/partner#tag/Merchants/operation/getMerchant)
with
[`GET:management/v1/merchants/{orgno}/sales-units`](https://developer.vippsmobilepay.com/api/management/#tag/Merchants/operation/getMerchantSalesUnits).

## Get sales unit by Merchant Serial Number

Replace
[`GET:partner-api/v0/salesunits/{msn}/`](https://developer.vippsmobilepay.com/api/partner#tag/Sales-units/operation/getMSN)
with
[`GET:management/v1/sales-units/{msn}/`](https://developer.vippsmobilepay.com/api/management/#tag/Sales-units/operation/getAllSalesUnits).

## Order products on behalf of merchants

Replace
[`POST:partner-api/v1/products/orders`](https://developer.vippsmobilepay.com/api/partner#tag/Vipps-Product-Orders/operation/orderProduct)
with
[`POST:management/v1/product-orders`](https://developer.vippsmobilepay.com/api/management/#tag/Product-orders).
