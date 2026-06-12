---
layout: default
nav_order: 3
title: Supplier API
---

# Supplier API {#reference-supplier-api}
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

API on supplier side.

## Insert order {#reference-supplier-api--insert-order}

[/api/v1/order/{order}?token={token}]

***Required method.***

**Reserve** products for new order. Supplier is waiting for **Confirm order**.

If a reservation is not possible due to an insufficient quantity on a store, 
this method accepts `Out of stock` error code `-3`.

Currency of `purchasePriceWithoutFees` is in `itemsPriceCurrency`. This price is same as in
*[Availability][availability]* and serves only to compare prices.

**You *can* return list of `errorProducts` with invalid products:**
 - structure is similar as in *[Availability][availability]*, but you can omit all attributes except required supplier product `code`
 - you *can* specify actual *availability*
 - default *availability* is `0`, so the end customers can't order product again until next *[Availability][availability]*
 - you can ignore *errorProducts*, availability of all products in order will be set to `0`


#### Rules for HTTP response status codes
 - **201** - Created status code. Response successfully processed with `errorCode` `0`.
    It is invalid with status code `-3` but response is accepted and processed.
 - **200** - OK status code. Response successfully processed with `errorCode` `-3`.
    It is invalid with status code `0` but response is accepted and processed.
 - **400** - Bad request status code. It is invalid status code with `errorCode` `-3` but response is accepted and processed. 
    Otherwise it is as an error ocured on application layer. See `errorCode` and `errorMessage` for more. 
    The error must be corrected and the request sent again.
 - Any other status code is considered invalid and the request must be sent again.

+ Parameters
    + order: DD12345678 ([OrderNumber][ds-order-number], required) - Order Number 
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token

### Insert order request {#reference-supplier-api--insert-order--insert-order-request}

[POST]

Request ([OrderInsertRequest][ds-order-insert-request])  
Response ([OrderInsertResponse][ds-order-insert-response])


+ Request Successful reservation to the address (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "regNo": "5445454",
                "vatNo": "CZ123456",
                "itemsPriceCurrency": "CZK",
                "itemsPriceCountry": "CZ",
                "orderItems": [
                    {
                        "orderItemId": 480907779,
                        "code": "AXO001",
                        "quantity": 2,
                        "purchasePriceWithoutFees": 142.5,
                        "fees": {
                            "copyright": 0.59,
                            "recycling": 1.0
                        },
                        "serialNumbersExpected" : true,
                        "serialNumbersRequired" : false
                    },
                    {
                        "orderItemId": 480907780,
                        "code": "AXO002",
                        "quantity": 1,
                        "purchasePriceWithoutFees": 190.5,
                        "fees": {
                            "copyright": 0.59,
                            "recycling": 2.0
                        },
                        "serialNumbersExpected" : false,
                        "serialNumbersRequired" : false
                    }
                ]
            }
        ```

+ Response 201 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": 0,
                "errorMessage": "",
                "supplierOrder": "A56789123456",
                "validUntil": "2025-07-01T00:00:00.000"
            }
        ```

+ Request Successful reservation to the branch (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "regNo": "5445454",
                "vatNo": "CZ123456",
                "itemsPriceCurrency": "CZK",
                "itemsPriceCountry": "CZ",
                "orderItems": [
                    {
                        "orderItemId": 480907779,
                        "code": "AXO001",
                        "quantity": 2,
                        "purchasePriceWithoutFees": 142.5,
                        "fees": {
                            "copyright": 0.59,
                            "recycling": 1.0
                        },
                        "alzaBarCodes": [
                            "BCX4809077791",
                            "BCX4809077792"
                        ],
                        "serialNumbersExpected" : true,
                        "serialNumbersRequired" : true
                    },
                    {
                        "orderItemId": 480907780,
                        "code": "AXO002",
                        "quantity": 1,
                        "purchasePriceWithoutFees": 190.5,
                        "fees": {
                            "copyright": 0.59,
                            "recycling": 2.0
                        },
                        "alzaBarCodes": [
                            "BCX4809077801"
                        ],
                        "serialNumbersExpected" : false,
                        "serialNumbersRequired" : false
                    }
                ]
            }
        ```

+ Response 201 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": 0,
                "errorMessage": "",
                "supplierOrder": "A56789123456",
                "validUntil": "2025-07-01T00:00:00.000"
            }
        ```

+ Request Out of stock (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "regNo": "5445454",
                "vatNo": "CZ123456",
                "itemsPriceCurrency": "CZK",
                "itemsPriceCountry": "CZ",
                "orderItems": [
                    {
                        "orderItemId": 480907779,
                        "code": "AXO001",
                        "quantity": 2,
                        "purchasePriceWithoutFees": 142.5,
                        "fees": {
                            "copyright": 0.59,
                            "recycling": 1.0
                        },
                        "serialNumbersExpected" : true,
                        "serialNumbersRequired" : false
                    },
                    {
                        "orderItemId": 480907780,
                        "code": "AXO002",
                        "quantity": 1,
                        "purchasePriceWithoutFees": 190.5,
                        "fees": {
                            "copyright": 0.59,
                            "recycling": 2.0
                        },
                        "serialNumbersExpected" : false,
                        "serialNumbersRequired" : false
                    }
                ]
            }
        ```

+ Response 200 (application/json; charset=utf-8)

    + Body

        ```json
            {
                 "errorCode": -3,
                 "errorMessage": "Out of stock",
                 "errorProducts": [
                    {
                        "code": "AXO001",
                        "quantity": 1
                    }
                ]
            }
        ```

+ Request Invalid product (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "regNo": "5445454",
                "vatNo": "CZ123456",
                "itemsPriceCurrency": "CZK",
                "itemsPriceCountry": "CZ",
                "orderItems": [
                    {
                        "orderItemId": 480907779,
                        "code": "AXO001_XXX",
                        "quantity": 2,
                        "purchasePriceWithoutFees": 142.5,
                        "fees": {
                            "copyright": 0.59,
                            "recycling": 1.0
                        },
                        "serialNumbersExpected" : true,
                        "serialNumbersRequired" : false
                    }
                ]
            }
        ```

+ Response 400 (application/json; charset=utf-8)

    + Body

        ```json
            {
                 "errorCode": -2,
                 "errorMessage": "Uknown product AXO001_XXX"
            }
        ```


## Cancel order {#reference-supplier-api--cancel-order}

[/api/v1/order/{cancelOrder}?token={token}]

***Required method.***

When the buyer cancels the order before **[Confirm order][confirm-order]**, the supplier must cancel the order immediately.
In this state method doesn't accept error code `-5`.

When the buyer cancels the order after **[Confirm order][confirm-order]** and before **[Shipment departure][shipment-departure]**,
the supplier has right to reject the attempt. In this state method accepts error code `-5`.

After **[Shipment departure][shipment-departure]** is not possible to cancel order.

**Possible scenarios when order is confirmed**:
+ The supplier knows the order can be canceled. The supplier will respond with `errorCode` `0` and the order will be cancelled.
+ The supplier doesn't know if the order can be canceled. The supplier will respond with `errorCode` `-5` 
  and marks the order to cancellation. After manual or asynchronous processing, the supplier may call 
  **[Delivery Result Canceled][delivery-result]** if the order can be canceled.
+ The supplier knows the order can't be canceled due to the processing of the shipment. 
  The supplier will respond with `errorCode` `-5` and the order won't be canceled.
+ The supplier doesn't expect order cancel after **[Confirm order][confirm-order]**. The supplier will respond with `errorCode` `-1`. 
  The buyer's API gives a few tries and if still gets `-1` then the order won't be canceled.

#### Rules for HTTP response status codes
 - **200** - OK status code. Message successfully processed. `errorCode` must be also `0` or accepted `-5`.
 - **201** - Created status code. It is invalid status code but response is accepted and processed. `errorCode` must be also `0` or accepted `-5`.
 - **400** - Bad request status code. It is invalid status code with accepted `errorCode` `-5` but response is accepted and processed. 
    Otherwise it is as an error ocured on application layer. See `errorCode` and `errorMessage` for more. 
    The error must be corrected and the request sent again.
 - Any other status code is considered invalid and the request must be sent again.


+ Parameters
    + cancelOrder: DD12345678 ([OrderNumber][ds-order-number], required) - Order Number 
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token

### Cancel order request [DELETE] {#reference-supplier-api--cancel-order--cancel-order-request-delete}

Request ([OrderCancelRequest][ds-order-cancel-request])  
Response ([GeneralResponse][ds-general-response])

 
+ Request Successful Cancel order (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "regNo": "5445454",
                "vatNo": "CZ123456"
            }
        ```

+ Response 200 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": 0,
                "errorMessage": ""
            }
        ```

+ Request Unsuccessful Cancel order (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "regNo": "5445454",
                "vatNo": "CZ123456"
            }
        ```

+ Response 200 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": -5,
                "errorMessage": "The order could not be canceled in the departure state."
            }
        ```

+ Request Failed Cancel order (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "regNo": "5445454",
                "vatNo": "CZ123456"
            }
        ```

+ Response 400 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": -2,
                "errorMessage": "Unknown order."
            }
        ```



## Confirm order {#reference-supplier-api--confirm-order}

[/api/v1/order/{order}/confirm?token={token}]

***Required method.***

**Starts Order** processing. Attributes contains *delivery address*, selected *shipping carrier* and *cash on delivery value*.

`demandedExpeditionDate` and `shipmentDepartureTime` are demanded date and time for shipment departure. 
It is not allowed to send the shipment earlier or later. The shipment is planned according to the customer's requirements.

#### Rules for HTTP response status codes
 - **200** - OK status code. Response successfully processed. `errorCode` must be also `0`.
 - **201** - Created status code. It is invalid status code but response is accepted and processed. `errorCode` must be also `0`.
 - **400** - Bad request status code. An error ocured on application layer. See `errorCode` and `errorMessage` for more. 
    The error must be corrected and the request sent again.
 - Any other status code is considered invalid and the request must be sent again.

+ Parameters
    + order: DD12345678 ([OrderNumber][ds-order-number], required) - Order Number 
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token

### Confirm order request  {#reference-supplier-api--confirm-order--confirm-order-request}

[POST]

Request ([OrderConfirmRequest][ds-order-confirm-request])  
Response ([GeneralResponse][ds-general-response])

 
+ Request Successful Confirm order (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "regNo": "5445454",
                "vatNo": "CZ123456",
                "shippingCarrier": {
                    "shippingCarrierCode": "GEISPARCEL",
                    "shippingCarrierDeliveryType": "GEISPOINT"
                },
                "parcelShop": {
                    "parcelShopIdentification": "GEISPOINT",
                    "parcelShopBranchCode": "123"
                },
                "shipmentDeliveryType": "ParcelShop",
                "shipmentShippingMode": "Supplier",
                "demandedExpeditionDate": "2025-06-02",
                "shipmentDepartureTime": "2025-06-02T08:00:00.000",
                "cashOnDeliveryValue": 450.0,
                "cashOnDeliveryValueCurrency": "CZK",
                "packageSorting": {
                    "packageSortingGroup": "Linehaul",
                    "packageSortingPrint": "L"
                },                
                "shipmentValue": 500.0,
                "shipmentValueCurrency": "CZK",
                "paymentVS": "123456781",
                "shipmentExternalOrderNumber":"A2026010901",
                "deliveryAddress": {
                    "companyName": "",
                    "addressName": "Franta Veverka",
                    "streetWithNumber": "HornĂ­ 147/4",
                    "city": "Praha 4",
                    "country": "CZ",
                    "zip": "14000",
                    "phone": "+420777666555",
                    "email": "franta@veverka.cz",
                    "note": "Pozor na Barbara (kocour), kouĹˇe"
                }
            }
        ```

+ Response 200 (application/json; charset=utf-8)
 
    + Body

        ```json
            {
                "errorCode": 0,
                "errorMessage": ""
            }
        ```

+ Request Failed Confirm order (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "regNo": "5445454",
                "vatNo": "CZ123456",
                "shippingCarrier": {
                    "shippingCarrierCode": "GEISPARCEL",
                    "shippingCarrierDeliveryType": "GEISPOINT"
                },
                "parcelShop": {
                    "parcelShopIdentification": "GEISPOINT",
                    "parcelShopBranchCode": "123"
                },
                "shipmentDeliveryType": "ParcelShop",
                "demandedExpeditionDate": "2025-06-02",
                "shipmentDepartureTime": "2025-06-02T08:00:00.000",
                "cashOnDeliveryValue": 450.0,
                "cashOnDeliveryValueCurrency": "CZK",
                "packageSorting": {
                    "packageSortingGroup": "RegularDirect"
                },               
                "shipmentValue": 500.0,
                "shipmentValueCurrency": "CZK",
                "paymentVS": "123456781",
                "deliveryAddress": {
                    "companyName": "",
                    "addressName": "Franta Veverka",
                    "streetWithNumber": "HornĂ­ 147/4",
                    "city": "Praha 4",
                    "country": "CZ",
                    "zip": "14000",
                    "phone": "+420777666555",
                    "email": "franta@veverka.cz",
                    "note": "Pozor na Barbara (kocour), kouĹˇe"
                }
            }
        ```

+ Response 400 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": -1,
                "errorMessage": "Unknown error"
            }
        ```


+ Request Confirm order with route (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "regNo": "5445454",
                "vatNo": "CZ123456",
                "shippingCarrier": {
                    "shippingCarrierCode": "GEISPARCEL",
                    "shippingCarrierDeliveryType": "GEISPOINT"
                },
                "parcelShop": {
                    "parcelShopIdentification": "GEISPOINT",
                    "parcelShopBranchCode": "123"
                },
                "route": {    
                    "routeName": "DS MP00001 -> CZLC4 -> CZLC3 -> PoÄŤernice",
                    "routeStops": [
                        {
                            "branchName": "CZLC4",
                            "ramp": "L321"     
                        },
                        {
                            "branchName": "CZLC3",
                            "ramp": "L05"
                        }
                    ]
                },                 
                "shipmentDeliveryType": "ParcelShop",
                "shipmentShippingMode": "Supplier",
                "demandedExpeditionDate": "2025-06-02",
                "shipmentDepartureTime": "2025-06-02T08:00:00.000",
                "cashOnDeliveryValue": 450.0,
                "cashOnDeliveryValueCurrency": "CZK",
                "packageSorting": {
                    "packageSortingGroup": "CrossLC",
                    "packageSortingPrint": "C"
                },                
                "shipmentValue": 500.0,
                "shipmentValueCurrency": "CZK",
                "paymentVS": "123456781",
                "deliveryAddress": {
                    "companyName": "",
                    "addressName": "Franta Veverka",
                    "streetWithNumber": "HornĂ­ 147/4",
                    "city": "Praha 4",
                    "country": "CZ",
                    "zip": "14000",
                    "phone": "+420777666555",
                    "email": "franta@veverka.cz",
                    "note": "Pozor na Barbara (kocour), kouĹˇe"
                }
            }
        ```

+ Response 200 (application/json; charset=utf-8)
 
    + Body

        ```json
            {
                "errorCode": 0,
                "errorMessage": ""
            }
        ```
            

+ Request Upcoming feature: Confirm order with GLN list (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 2934,
                "supplierBranchId": 529,
                "regNo": "5445454",
                "vatNo": "CZ123456",
                "taxNo": "CZ123456",
                "shippingCarrier": {
                    "shippingCarrierCode": "ALZA",
                    "shippingCarrierDeliveryType": "ALZABOX"
                },
                "parcelShop": {
                    "parcelShopIdentification": "ALZABOX",
                    "parcelShopBranchCode": "AB1790"
                },
                "route": {
                    "routeName": "DS321654 CZ 01 -> LC04 -> Liberecko B3",
                    "routeStops": [{ "branchName": "LC04", "ramp": "L12" }]
                },
                "shipmentDeliveryType": "ParcelShop",
                "shipmentShippingMode": "Buyer",
                "demandedExpeditionDate": "2025-06-02",
                "shipmentDepartureTime": "2025-06-02T08:00:00.000",
                "cashOnDeliveryValue": 0.0,
                "cashOnDeliveryValueCurrency": "CZK",
                "packageSorting": {
                    "packageSortingGroup": "CrossLC",
                    "packageSortingPrint": "C"
                },                
                "paymentVS": "123456781",
                "deliveryAddress": {
                    "companyName": "",
                    "addressName": "Andrea NovĂˇkovĂˇ",
                    "streetWithNumber": "VinohradskĂˇ 105",
                    "city": "Praha",
                    "phone": "+420777666555",
                    "email": "novakova@gmail.com",
                    "country": "CZ",
                    "zip": "10000"
                },
                "shipmentValue": 368.0,
                "shipmentValueCurrency": "CZK",
                "glnList": {
                    "buyerGln": "8532165490005",
                    "orderedByGln": "8532165490005",
                    "invoiceeGln": "8532165490002",
                    "shipmentDeliveryGln": "8532165490011"
                },
                "shipmentDeliveryAddress": {
                    "companyName": "AlzaBox 19 BeneĹˇov",
                    "streetWithNumber": "NĂˇdraĹľnĂ­ 2105",
                    "city": "BeneĹˇov",
                    "country": "CZ",
                    "zip": "25601"
                },
                "buyerAddress": {
                    "companyName": "Buyer.cz a.s.",
                    "streetWithNumber": "NĂˇmÄ›stĂ­ mĂ­ru 1/1",
                    "city": "Praha 1",
                    "country": "CZ",
                    "zip": "10000"
                }
            }
        ```

+ Response 200 (application/json; charset=utf-8)
 
    + Body

        ```json
            {
                "errorCode": 0,
                "errorMessage": ""
            }
        ```
            

+ Request Upcoming feature: Delivery services (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2026-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "regNo": "5445454",
                "vatNo": "CZ123456",
                "shippingCarrier": {
                    "shippingCarrierCode": "TOPTRANS",
                    "shippingCarrierDeliveryType": "TOPTRANS"
                },
                "shipmentDeliveryType": "B2C",
                "shipmentShippingMode": "Supplier",
                "shipmentDeliveryServices": {
                    "oldApplianceRemoval": true,
                    "carryIn": true
                },                
                "demandedExpeditionDate": "2026-06-03",
                "shipmentDepartureTime": "2026-06-03T08:00:00.000",
                "cashOnDeliveryValue": 0.0,
                "cashOnDeliveryValueCurrency": "CZK",              
                "shipmentValue": 5000.0,
                "shipmentValueCurrency": "CZK",
                "paymentVS": "123456781",
                "shipmentExternalOrderNumber":"A2026010901",
                "deliveryAddress": {
                    "addressName": "Franta Veverka",
                    "streetWithNumber": "HornĂ­ 147/4",
                    "city": "Praha 4",
                    "country": "CZ",
                    "zip": "14000",
                    "phone": "+420777666555",
                    "email": "franta@veverka.cz"
                }
            }
        ```

+ Response 200 (application/json; charset=utf-8)
 
    + Body

        ```json
            {
                "errorCode": 0,
                "errorMessage": ""
            }
        ```




## Extend order {#reference-supplier-api--extend-order}

[/api/v1/order/{order}/extend?token={token}]

***Required method.***

Some suppliers offers only limited-time reservation. This action will **extend order reservation**.

If the implementation of this method is not desirable, always return an error code `-5`.
This method accepts this error code.

In case of refusal to extend the reservation of the order, a [Order Cancel][cancel-order] will be sent.

#### Rules for HTTP response status codes
 - **200** - OK status code. Response successfully processed. `errorCode` must be also `0` or `-5`.
 - **201** - Created status code. It is invalid status code but response is accepted and processed. `errorCode` must be also `0` or `-5`.
 - **400** - Bad request status code. It is invalid status code with `errorCode` `-5` but response is accepted and processed. 
    Otherwise it is as an error ocured on application layer. See `errorCode` and `errorMessage` for more.
    The error must be corrected and the request sent again.
 - Any other status code is considered invalid and the request must be sent again.

+ Parameters
    + order: DD12345678 ([OrderNumber][ds-order-number], required) - Order Number
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token

### Extend order request {#reference-supplier-api--extend-order--extend-order-request}

[POST]

Request ([OrderExtendRequest][ds-order-extend-request])  
Response ([OrderExtendResponse][ds-order-extend-response])


+ Request Successful Extend order (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "regNo": "5445454",
                "vatNo": "CZ123456",
                "validUntil": "2025-07-01T00:00:00.000"
            }
        ```

+ Response 200 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": 0,
                "errorMessage": "",
                "validUntil": "2025-07-01T00:00:00.000"
            }
        ```

+ Request Unsuccessful Extend order (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "regNo": "5445454",
                "vatNo": "CZ123456",
                "validUntil": "2025-07-01T00:00:00.000"
            }
        ```

+ Response 200 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": -5,
                "errorMessage": "Reservation expired."
            }
        ```

+ Request Failed Extend Order (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "regNo": "5445454",
                "vatNo": "CZ123456",
                "validUntil": "2025-07-01T00:00:00.000"
            }
        ```

+ Response 400 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": -1,
                "errorMessage": "Uknown order."
            }
        ```


[introduction]:                         ../#introduction
[upcoming-features]:                    ../#introduction--upcoming-features
[versions]:                             ../#introduction--versions
[simplified-communication-scheme]:      ../#introduction--simplified-communication-scheme
[communication-basics]:                 ../#introduction--communication-basics
[api-basics]:                           ../#introduction--api-basics
[maintenance-free-design]:              ../#introduction--maintenance-free-design
[authentication-token]:                 ../#introduction--authentication-token

[data-types]:                           ../#introduction--data-types
[basic-data-types]:                     ../#introduction--data-types--basic-data-types
[enumerated-data-types]:                ../#introduction--data-types--enumerated-data-types
[country-code]:                         ../#introduction--data-types--enumerated-data-types--country-code
[country-vs-currency]:                  ../#introduction--data-types--enumerated-data-types--country-vs-currency
[currency-code]:                        ../#introduction--data-types--enumerated-data-types--currency-code
[delivery-result-status]:               ../#introduction--data-types--enumerated-data-types--delivery-result-status
[error-code]:                           ../#introduction--data-types--enumerated-data-types--error-code
[import-type]:                          ../#introduction--data-types--enumerated-data-types--import-type
[parcel-shop-identification]:           ../#introduction--data-types--enumerated-data-types--parcel-shop-identification
[shipment-shipping-mode]:               ../#introduction--data-types--enumerated-data-types--shipment-shipping-mode
[shipping-carrier-code]:                ../#introduction--data-types--enumerated-data-types--shipping-carrier-code
[shipping-carrier-delivery-type]:       ../#introduction--data-types--enumerated-data-types--shipping-carrier-delivery-type
[track-and-trace-status]:               ../#introduction--data-types--enumerated-data-types--track-and-trace-status

[error-handling]:                       ../#introduction--error-handling--error-handling
[common-error-codes]:                   ../#introduction--error-handling--common-error-codes--common-error-codes
[resend-intervals]:                     ../#introduction--error-handling--resend-intervals
[timeout-settings]:                     ../#introduction--error-handling--timeout-settings
[rate-limits]:                          ../#introduction--error-handling--rate-limits
[shipping-modes]:                       ../#introduction--shipping-modes
[buyer-shipping-mode]:                  ../#introduction--shipping-modes--buyer-shipping-mode
[supplier-shipping-mode]:               ../#introduction--shipping-modes--supplier-shipping-mode
[product-pricing]:                      ../#introduction--product-pricing
[supplier-product-pricing]:             ../#introduction--product-pricing--supplier-product-pricing
[buyer-product-pricing]:                ../#introduction--product-pricing--buyer-product-pricing
[faq]:                                  ../#introduction--faq

[supplier-api]:                         ../supplier-api/#reference-supplier-api
[insert-order]:                         ../supplier-api/#reference-supplier-api--insert-order
[cancel-order]:                         ../supplier-api/#reference-supplier-api--cancel-order
[extend-order]:                         ../supplier-api/#reference-supplier-api--extend-order
[confirm-order]:                        ../supplier-api/#reference-supplier-api--confirm-order

[buyer-api]:                            ../buyer-api/#reference-buyer-api
[availability]:                         ../buyer-api/#reference-buyer-api--availability
[create-shipment]:                      ../buyer-api/#reference-buyer-api--create-shipment
[delete-shipment]:                      ../buyer-api/#reference-buyer-api--delete-shipment
[shipment-departure]:                   ../buyer-api/#reference-buyer-api--shipment-departure
[track-and-trace]:                      ../buyer-api/#reference-buyer-api--track-and-trace
[delivery-result]:                      ../buyer-api/#reference-buyer-api--delivery-result

[testing-supplier-api]:                 ../testing-supplier-api/#reference-testing-supplier-api
[testing-insert-order]:                 ../testing-supplier-api/#reference-testing-supplier-api--insert-order
[testing-cancel-order]:                 ../testing-supplier-api/#reference-testing-supplier-api--cancel-order
[testing-confirm-order]:                ../testing-supplier-api/#reference-testing-supplier-api--confirm-order
[testing-extend-order]:                 ../testing-supplier-api/#reference-testing-supplier-api--extend-order

[testing-buyer-api]:                    ../testing-buyer-api/#reference-testing-buyer-api
[testing-availability]:                 ../testing-buyer-api/#reference-testing-buyer-api--availability
[testing-create-shipment]:              ../testing-buyer-api/#reference-testing-buyer-api--create-shipment
[testing-delete-shipment]:              ../testing-buyer-api/#reference-testing-buyer-api--delete-shipment
[testing-delivery-result]:              ../testing-buyer-api/#reference-testing-buyer-api--delivery-result
[testing-shipment-departure]:           ../testing-buyer-api/#reference-testing-buyer-api--shipment-departure
[testing-track-and-trace]:              ../testing-buyer-api/#reference-testing-buyer-api--track-and-trace

[data-structures]:                      ../data-structures/#data-structures
[ds-timestamp]:                         ../data-structures/#data-structures--timestamp
[ds-timestamputc]:                      ../data-structures/#data-structures--timestamputc
[ds-date]:                              ../data-structures/#data-structures--date
[ds-int-16]:                            ../data-structures/#data-structures--int-16
[ds-int-32]:                            ../data-structures/#data-structures--int-32
[ds-int-64]:                            ../data-structures/#data-structures--int-64
[ds-float]:                             ../data-structures/#data-structures--float
[ds-string-10]:                         ../data-structures/#data-structures--string-10
[ds-string-20]:                         ../data-structures/#data-structures--string-20
[ds-string-30]:                         ../data-structures/#data-structures--string-30
[ds-string-50]:                         ../data-structures/#data-structures--string-50
[ds-string-100]:                        ../data-structures/#data-structures--string-100
[ds-string-500]:                        ../data-structures/#data-structures--string-500
[ds-customer-id]:                       ../data-structures/#data-structures--customer-id
[ds-supplier-product-code]:             ../data-structures/#data-structures--supplier-product-code
[ds-weight]:                            ../data-structures/#data-structures--weight
[ds-volume]:                            ../data-structures/#data-structures--volume
[ds-money]:                             ../data-structures/#data-structures--money
[ds-vat]:                               ../data-structures/#data-structures--vat
[ds-hmac-token]:                        ../data-structures/#data-structures--hmac-token
[ds-country]:                           ../data-structures/#data-structures--country
[ds-currency]:                          ../data-structures/#data-structures--currency
[ds-guid]:                              ../data-structures/#data-structures--guid
[ds-gln-list]:                          ../data-structures/#data-structures--gln-list
[ds-gln]:                               ../data-structures/#data-structures--gln
[ds-number]:                            ../data-structures/#data-structures--number
[ds-order-number]:                      ../data-structures/#data-structures--order-number
[ds-id]:                                ../data-structures/#data-structures--id
[ds-id-64]:                             ../data-structures/#data-structures--id-64

[ds-error-code]:                        ../data-structures/#data-structures--error-code
[ds-success-error-code]:                ../data-structures/#data-structures--success-error-code
[ds-fail-error-code]:                   ../data-structures/#data-structures--fail-error-code
[ds-import-type]:                       ../data-structures/#data-structures--import-type
[ds-track-and-trace-status]:            ../data-structures/#data-structures--track-and-trace-status
[ds-delivery-result-status]:            ../data-structures/#data-structures--delivery-result-status
[ds-shipment-delivery-type]:            ../data-structures/#data-structures--shipment-delivery-type
[ds-shipment-shipping-mode]:            ../data-structures/#data-structures--shipment-shipping-mode
[ds-shipment-delivery-services]:        ../data-structures/#data-structures--shipment-delivery-services
[ds-shipping-carrier-code]:             ../data-structures/#data-structures--shipping-carrier-code
[ds-shipping-carrier-delivery-type]:    ../data-structures/#data-structures--shipping-carrier-delivery-type
[ds-parcel-shop-identification]:        ../data-structures/#data-structures--parcel-shop-identification
[ds-route]:                             ../data-structures/#data-structures--route
[ds-route-stop]:                        ../data-structures/#data-structures--route-stop
[ds-delivery-address]:                  ../data-structures/#data-structures--delivery-address
[ds-company-address]:                   ../data-structures/#data-structures--company-address
[ds-shipment-address]:                  ../data-structures/#data-structures--shipment-address
[ds-package-sorting-group]:             ../data-structures/#data-structures--package-sorting-group

[ds-shipping-list]:                     ../data-structures/#data-structures--shipping-list
[ds-shipping-list-group]:               ../data-structures/#data-structures--shipping-list-group
[ds-departured-shipment]:               ../data-structures/#data-structures--departured-shipment
[ds-product]:                           ../data-structures/#data-structures--product
[ds-error-product]:                     ../data-structures/#data-structures--error-product
[ds-parcel-shop]:                       ../data-structures/#data-structures--parcel-shop
[ds-shipping-carrier-confirm]:          ../data-structures/#data-structures--shipping-carrier-confirm
[ds-shipping-carrier]:                  ../data-structures/#data-structures--shipping-carrier
[ds-shipping-carrier-strict]:           ../data-structures/#data-structures--shipping-carrier-strict
[ds-country-price]:                     ../data-structures/#data-structures--country-price
[ds-country-price-fees]:                ../data-structures/#data-structures--country-price-fees
[ds-created-shipment]:                  ../data-structures/#data-structures--created-shipment
[ds-created-package]:                   ../data-structures/#data-structures--created-package
[ds-shipment-create-item]:              ../data-structures/#data-structures--shipment-create-item
[ds-shipment-create-package]:           ../data-structures/#data-structures--shipment-create-package
[ds-shipment-departure-package]:        ../data-structures/#data-structures--shipment-departure-package
[ds-shipment-departure-item]:           ../data-structures/#data-structures--shipment-departure-item
[ds-order-item]:                        ../data-structures/#data-structures--order-item
[ds-package-sorting]:                   ../data-structures/#data-structures--package-sorting

[ds-availability-request]:              ../data-structures/#data-structures--availability-request
[ds-order-insert-request]:              ../data-structures/#data-structures--order-insert-request
[ds-order-insert-response]:             ../data-structures/#data-structures--order-insert-response
[ds-order-extend-request]:              ../data-structures/#data-structures--order-extend-request
[ds-order-extend-response]:             ../data-structures/#data-structures--order-extend-response
[ds-order-cancel-request]:              ../data-structures/#data-structures--order-cancel-request
[ds-order-confirm-request]:             ../data-structures/#data-structures--order-confirm-request
[ds-shipment-create-request]:           ../data-structures/#data-structures--shipment-create-request
[ds-shipment-create-response]:          ../data-structures/#data-structures--shipment-create-response
[ds-shipment-delete-request]:           ../data-structures/#data-structures--shipment-delete-request
[ds-shipment-departure-request]:        ../data-structures/#data-structures--shipment-departure-request
[ds-shipment-departure-response]:       ../data-structures/#data-structures--shipment-departure-response
[ds-track-and-trace-request]:           ../data-structures/#data-structures--track-and-trace-request
[ds-delivery-result-request]:           ../data-structures/#data-structures--delivery-result-request
[ds-general-response]:                  ../data-structures/#data-structures--general-response

[ds-invoker-simple-request]:            ../data-structures/#data-structures--invoker-simple-request
[ds-invoker-order-insert-request]:      ../data-structures/#data-structures--invoker-order-insert-request
[ds-invoker-order-insert-response]:     ../data-structures/#data-structures--invoker-order-insert-response
[ds-invoker-order-extend-response]:     ../data-structures/#data-structures--invoker-order-extend-response
[ds-invoker-order-confirm-response]:    ../data-structures/#data-structures--invoker-order-confirm-response
[ds-invoker-order-cancel-response]:     ../data-structures/#data-structures--invoker-order-cancel-response

[hmac]:                                 https://en.wikipedia.org/wiki/Hash-based_message_authentication_code
[base64]:                               https://msdn.microsoft.com/library/system.convert.tobase64string.aspx
[percent-encoding]:                     https://en.wikipedia.org/wiki/Percent-encoding

[wiki-country-code]:                    https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2
[wiki-currency-code]:                   https://en.wikipedia.org/wiki/ISO_4217
[iso-country-code]:                     https://www.iso.org/iso-3166-country-codes.html
[iso-currency-code]:                    https://www.iso.org/iso-4217-currency-codes.html
