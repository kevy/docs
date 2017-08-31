---
title: Kevy API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='mailto:support@kevy.co'>Request a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Kevy API! You can use our API to access Kevy API endpoints, which can get information on various orders, contacts, campaigns, lists, and automations in our database.

We have language bindings in Shell! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "https://api.kevy.co/"
  -H "Authorization: Token kevyapikey"
```

> Make sure to replace `kevyapikey` with your API key.

Kevy uses API keys to allow access to the API. You can request a new Kevy API key at by contacting [Kevy Support](mailto:support@kevy.co).

Kevy expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Token kevyapikey`

<aside class="notice">
You must replace <code>kevyapikey</code> with your personal API key.
</aside>

# Contacts

## Contact Properties

Attribute | Type | Description
--------- | ------- | -----------
email | string | Contact's email address.
first_name | string | Contact's first name.
middle_name | string | Contact's middle name.
last_name | string | Contact's first name.
phone_number | string | Contact's phone number.
prefix | string | Contact's prefix.
suffix | string | Contact's suffix.
company | string | Contact's company name.
birthday | string | Contact's birthday in format YYYY-MM-DD.
accepts_emails | boolean | Whether contact accepts emails.
is_mailable | boolean | Whether contact accepts direct mail.
accepts_texts | boolean | Whether contact accepts text messages.
orders_count | integer | Quantity orders made by the contact.
total_spent | string | Total amount spent.
created_at | datetime | The date the contact was created.
updated_at | datetime | The date the contact was last updated.

## Contact Address Properties

Attribute | Type | Description
--------- | ------- | -----------
first_name | string | Contact's first name.
middle_name | string | Contact's middle name.
last_name | string | Contact's first name.
phone_number | string | Contact's phone number.
prefix | string | Contact's prefix.
suffix | string | Contact's suffix.
company | string | Company name.
address_one | string | Address line 1.
address_two | string | Address line 2.
city | string | City name.
state | string | ISO code or name of the state, province or district.
zip | string | Postal code.
country | string | ISO code of the country.

# Orders

The order API allows you to create batch orders.

## Order Properties

Attribute | Type | Description
--------- | ------- | -----------
order_number | string | Order number.
subtotal_price | string | Line subtotal (before discounts).
total_price | string | Total price.
discount | string | Total discount amount for the order.
shipping | string | Total shipping amount for the order.
store_id | string | Kevy Store ID.
email_address | string | Customer email address.
contact | object | Contact data. See Contact - Contact properties
contact_address | object | Contact address data. See Contact - Contact Address properties
coupon_codes | array | Coupon code data.
order_items | array | Order items data. See Order - Line items properties.
order_date | datetime | Date order was placed.
ip_address | string | Customer IP address.
referrer | string | Referring URL.
currency | string | Currency the order was created with, in ISO format.
status | string | Order status.
cart_token | string | Cart token associated with order.
created_at | datetime | The date the order was created.
updated_at | datetime | The date the order was last updated.

## Order - Order Item Properties

Attribute | Type | Description
--------- | ------- | -----------
name | string | Product name.
sku | string | Product SKU.
price | string | Product price.
quantity | string | Quantity ordered.

## Batch Create Orders

This API helps you to batch create multiple orders.

```shell
curl "https://api.kevy.co/orders/batch/:store_id/"
  -H "Authorization: Token kevyapitoken"
  -d '{
  [
    {
      "order_number"=>"351586",
      "total_price"=>"259.00",
      "discount"=>"0.00",
      "store_id"=>"12"
      "email_address": "john.doe@example.com",
      "coupon_codes": ["WELN0615","DOGFOOD"]
      "order_date": "2017-03-22T16:28:02"
      "order_items": [
        {
          "sku"=>"3EFN",
          "name"=>"Evergreen Tree",
          "price"=>"17.00",
          "quantity"=>"1"
        },
        {
          "sku"=>"3TRNS",
          "name"=>"3TRNS",
          "price"=>"0.90",
          "quantity"=>"25"
        }
      "contact": {
        "email": "john.doe@example.com",
        "first_name": "John",
        "last_name": "Doe",
        "accepts_emails" true,
        "company": "",
        "phone": "(555) 555-5555"
      },
      "contact_address": {
        "first_name": "John",
        "last_name": "Doe",
        "company": "",
        "address_one": "969 Market",
        "address_two": "",
        "city": "San Francisco",
        "state": "CA",
        "zip": "94103",
        "country": "US",
        "email": "john.doe@example.com",
        "phone": "(555) 555-5555"
      }
    },
    {
      "order_number"=>"358131",
      "total_price"=>"280.00",
      "discount"=>"0.00",
      "store_id"=>"12"
      "email_address": "jane.doe@example.com",
      "coupon_codes": ["WELN0615","DOGFOOD"]
      "order_date": "2017-03-22T16:58:02"
      "order_items": [
        {
          "sku"=>"3EFN",
          "name"=>"Evergreen Tree",
          "price"=>"17.00",
          "quantity"=>"1"
        },
        {
          "sku"=>"3TRNS",
          "name"=>"3TRNS",
          "price"=>"0.90",
          "quantity"=>"25"
        }
      "contact": {
        "email": "jane.doe@example.com",
        "first_name": "Jane",
        "last_name": "Doe",
        "accepts_emails" true,
        "company": "",
        "phone": "(555) 555-5555"
      },
      "contact_address": {
        "first_name": "Jane",
        "last_name": "Doe",
        "company": "",
        "address_one": "969 Market",
        "address_two": "",
        "city": "San Francisco",
        "state": "CA",
        "zip": "94103",
        "country": "US",
        "email": "jane.doe@example.com",
        "phone": "(555) 555-5555"
      }
    }
  ]
}'
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```
