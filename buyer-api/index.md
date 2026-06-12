---
layout: default
nav_order: 2
title: Buyer API
---


# Buyer API {#reference-buyer-api}
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

API on buyer side.

## Availability {#reference-buyer-api--availability}

[/api/v1/availability?token={token}]

***Required method.***

It mainly updates *store* **availability** and *product* **price**.

 - The `Update` import type is used to update all changes to products.
 - The `PartialFull` import type is used to update the available product portfolio overnight to prevent it from being removed from the store.
 - Values older that approx `36 hours` are considered as unavailable.
 - **Limitation:** The current limit is 30 MB per API message.

#### Rules for Update `importType`
 - It is recommended to **not** send *name* attribute.
 - It is required to **not** send *dimensions* and *weight* attribute. They will be removed in the future.
 - It is required to send only products where is a change in attributes from previous successfully delivered product attributes.
 - It is required to accumulate changes with minimal 10-minute intervals.
 - It is required to send accumulated changes with maximal 1-hour intervals, if any.
 - It is forbidden to send all products at once. And not even divided into a series of consecutive messages.
 - If product count exceeds unwanted limits it could be message rejected with error code `-5`. This method accepts this error code.
   Resend could lead to another error.
 - Unwanted limits are dynamic, they can change according to system load and cannot be expressed by a simple constant.

#### Rules for PartialFull `importType`
 - Replaces Full `importType`.
 - Maximum number of products in one message is `10,000`.
 - If more than 10,000 products need to be send, please follow the *[resend intervals][resend-intervals]* for next message.
 - It is required to **not** send *dimensions* and *weight* attribute. They will be removed in the future.
 - It is required to send only products with `productList[].quantity` higher then 0.
 - `PartialFull` is only allowed to be sent at night between `00:00` and `06:00`.
 - It is not allowed to repeat products in individual successfully delivered messages during one night.
 - At least one message must be sent per night to avoid branch cleanup. If `Full` import is not send.

#### Rules for Full `importType` Deprecated
 - **This `importType` is deprecated. Use PartialFull instead.**
 - Products that are missing in `Full` import are considered as unavailable.
 - It is required to **not** send *dimensions* and *weight* attribute. They will be removed in the future.
 - It is restricted to one successful request per day. Further requests by prior arrangement only.

#### Product price modes

Due to the development and the need for backward compatibility, two modes have emerged. 
**Legacy price mode** and **Latest price mode**.  
Each mode uses own set of attributes and these attributes are not compatible. Combining these modes is not allowed!

 - **Legacy price mode** attributes **(Deprecated)**
    - `productList[].price`
    - `productList[].priceWithFee`
    - `productList[].fee`
    - `productList[].vat`
 - **Latest price mode** attributes **(Recommended)**
    - `productList[].countryPrices`

#### Rules for HTTP response status codes
 - **200** - OK status code. Message successfully processed. `errorCode` must be also `0`.
 - **400** - Bad request status code. Error ocured on application layer. See more in `errorCode` and `errorMessage`.
 - Any other status code is considered invalid and the request must be sent again according to the resend rules.

+ Parameters
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token


### Availability request {#reference-buyer-api--availability--availability-request}

[POST]

Request ([AvailabilityRequest][ds-availability-request])  
Response ([GeneralResponse][ds-general-response])  

+ Request PartialFull import for Supplier product pricing  (application/json; charset=utf-8)

    + Body

         ```json
            {
                "supplierId": 12345,
                "supplierBranchId": 123,
                "timestamp": "2025-06-01T19:33:43.513",
                "importType": "PartialFull",
                "currency": "CZK",
                "productList": [
                    {
                        "name": "Product name 1",
                        "code": "Supplier-Code-01",
                        "ean": "Product-EAN-01",
                        "quantity": 1,
                        "countryPrices": [
                            {
                                "vat": 10.0,
                                "sellingPriceWithoutVat": 19.99,
                                "fees": {
                                    "copyright": 2,
                                    "recycling": 3.1
                                }
                            }
                        ]
                    },
                    {
                        "name": "Product name 2",
                        "code": "Supplier-Code-02",
                        "ean": "Product-EAN-02",
                        "quantity": 50,
                        "limited": true,
                        "countryPrices": [
                            {
                                "vat": 21.0,
                                "sellingPriceWithoutVat": 24.99,
                                "fees": {
                                    "copyright": 2,
                                    "recycling": 3.1
                                }
                            }
                        ]
                    }
                ]
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

+ Request PartialFull import for Buyer product pricing  (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 12345,
                "supplierBranchId": 123,
                "timestamp": "2025-06-01T19:33:43.513",
                "importType": "PartialFull",
                "currency": "CZK",
                "productList": [
                    {
                        "name": "Product name 1",
                        "code": "Supplier-Code-01",
                        "ean": "Product-EAN-01",
                        "quantity": 1,  
                        "countryPrices": [
                            {
                                "vat": 10.0,
                                "purchasePriceWithoutFees": 10.12,
                                "fees": {
                                    "copyright": 2,
                                    "recycling": 3.1
                                } 
                            }
                        ]
                    },
                    {
                        "name": "Product name 2",
                        "code": "Supplier-Code-02",
                        "ean": "Product-EAN-02",
                        "quantity": 50,
                        "limited": true,
                        "countryPrices": [
                            {
                                "vat": 21.0,
                                "purchasePriceWithoutFees": 10.12,
                                "fees": {
                                    "copyright": 2,
                                    "recycling": 3.1
                                } 
                            }
                        ]
                    }
                ]
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

+ Request Invalid PartialFull import (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 12345,
                "supplierBranchId": 123,
                "timestamp": "2025-06-01T19:33:43.513",
                "importType": "PartialFull",
                "currency": "CZK",
                "productList": [
                    {
                        "name": "Product name 1",
                        "ean": "Product-EAN-01",
                        "quantity": 1, 
                        "countryPrices": [
                            {
                                "vat": 10.0,
                                "purchasePriceWithoutFees": 15.7
                            }
                        ]
                    }
                ]
            }
        ```

+ Response 400 (application/json; charset=utf-8)

    + Body

        ```json
            {
                 "errorCode": -1,
                 "errorMessage": "productList[0].code missing"
            }
        ```


+ Request Update import for Supplier product pricing  (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 12345,
                "supplierBranchId": 123,
                "timestamp": "2025-06-01T19:33:43.513",
                "importType": "Update",
                "currency": "CZK",
                "productList": [
                    {
                        "code": "Supplier-Code-01",
                        "ean": "Product-EAN-01",
                        "quantity": 1,
                        "countryPrices": [
                            {
                                "vat": 10.0,
                                "sellingPriceWithoutVat": 19.99,
                                "fees": {
                                    "copyright": 2,
                                    "recycling": 3.1
                                } 
                            }
                        ]
                    }
                ]
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


+ Request Update import for Buyer product pricing  (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 12345,
                "supplierBranchId": 123,
                "timestamp": "2025-06-01T19:33:43.513",
                "importType": "Update",
                "currency": "CZK",
                "productList": [
                    {
                        "code": "Supplier-Code-01",
                        "ean": "Product-EAN-01",
                        "quantity": 1,
                        "countryPrices": [
                            {
                                "vat": 10.0,
                                "purchasePriceWithoutFees": 10.12,
                                "fees": {
                                    "copyright": 2,
                                    "recycling": 3.1
                                } 
                            }
                        ]
                    }
                ]
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

+ Request Invalid Update import (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 12345,
                "supplierBranchId": 123,
                "timestamp": "2025-06-01T19:33:43.513",
                "importType": "Update",
                "currency": "CZK",
                "productList": [
                    {
                        "ean": "Product-EAN-01",
                        "quantity": 1,
                        "countryPrices": [
                            {
                                "vat": 10.0,
                                "purchasePriceWithoutFees": 15.7
                            }
                        ]
                    }
                ]
            }
        ```

+ Response 400 (application/json; charset=utf-8)

    + Body

        ```json
            {
                 "errorCode": -1,
                 "errorMessage": "productList[0].code missing"
            }
        ```

## Create shipment {#reference-buyer-api--create-shipment}

[/api/v1/shipment?token={token}]

***Buyer shipping mode method***

Create **shipment**. Shipment contains order items from one supplier branch which are 
transported to one address. The address could be the buyer's branch, parcel shop or end customer address. 
For the shipments delivered to the buyer's branch are required to group the orders to the consolidate packages.
It is also required to send the entire order in one shipment.

Generate carrier **shipping stickers** for packages and return them as `PDF`, ready to print as label on package. 

Method may be provided in the case of limited capabilities of the supplier.

**Shipment consolidation rules**

| shipmentDeliveryType | Allowed | Required |
|----------------------|---------|----------|
| `B2C`                | No      | No       |
| `B2B`                | No      | No       |
| `Branch`             | Yes     | Yes      |
| `ParcelShop`         | No      | No       |

#### Rules for HTTP response status codes
 - **201** - Created status code. Message successfully processed and shipment created. `errorCode` must be also `0`.
 - **400** - Bad request status code. Error ocured on application layer. See more in `errorCode` and `errorMessage`.
 - Any other status code is considered invalid and the request must be sent again according to the resend rules.

+ Parameters
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token

### Create shipment request {#reference-buyer-api--create-shipment--create-shipment-request}

[POST]

Request ([ShipmentCreateRequest][ds-shipment-create-request])  
Response ([ShipmentCreateResponse][ds-shipment-create-response])
 
+ Request Successful creation (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 12345,
                "supplierBranchId": 212,
                "timestamp": "2025-06-01T19:33:43.513",
                "shippingCarrier": {
                    "shippingCarrierCode": "GEISPARCEL",
                    "shippingCarrierDeliveryType": "GEISPOINT"
                },
                "parcelShop": {
                    "parcelShopIdentification": "GEISPOINT",
                    "parcelShopBranchCode": "123"
                },
                "cashOnDeliveryValue": 250.0,
                "cashOnDeliveryValueCurrency": "CZK",
                "shipmentValue": 300.0,
                "shipmentValueCurrency": "CZK",
                "shipmentWeight": 0.9,
                "shipmentVolume": 750,
                "packages": [
                    {
                        "packageId": 1,
                        "weight": 0.4,
                        "volume": 200
                    },
                    {
                        "packageId": 2,
                        "weight": 0.5,
                        "volume": 550
                    }
                ],
                "items": [
                    {
                        "order": "DD12345678",
                        "orderItemId": 54879848461,
                        "quantity": 1,
                        "packageId": 1
                    },
                    {
                        "order": "DD12345678",
                        "orderItemId": 54879848462,
                        "quantity": 3,
                        "packageId": 2
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
                "shipment": {
                    "shipmentNumber": "SHIP8765412",
                    "packages": [
                        {
                            "packageId": 1,
                            "number": "135NUM000B1",
                            "fullNumber": "700135NUM000B10000Q1",
                            "pdf": "https://test.buyer.cz/Apps/pdfdoc.asp?s=1112223344&i=1&x=27s40308532101134N2D17264233"
                        },
                        {
                            "packageId": 2,
                            "number": "135NUM000B2",
                            "fullNumber": "700135NUM000B20000DW",
                            "pdf": "https://test.buyer.cz/Apps/pdfdoc.asp?s=1112223344&i=2&x=27s40308532105133N2D17264251"
                        }
                    ],
                    "pdf": "https://test.buyer.cz/Apps/pdfdoc.asp?s=1112223344&x=27s40308532105133N2D17267704"
                }
            }
        ```

+ Request Invalid creation (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 12345,
                "supplierBranchId": 212,
                "timestamp": "2025-06-01T19:33:43.513",
                "shippingCarrier": {
                    "shippingCarrierCode": "GEISPARCEL",
                    "shippingCarrierDeliveryType": "GEISPOINT"
                },
                "parcelShop": {
                    "parcelShopIdentification": "GEISPOINT",
                    "parcelShopBranchCode": "123"
                },
                "cashOnDeliveryValue": 250.0,
                "cashOnDeliveryValueCurrency": "CZK",
                "shipmentValue": 300.0,
                "shipmentValueCurrency": "CZK",
                "shipmentWeight": 0.9,
                "shipmentVolume": 750,
                "packages": [
                    {
                        "weight": 0.4,
                        "volume": 200
                    },
                    {
                        "packageId": 2,
                        "weight": 0.5,
                        "volume": 550
                    }
                ],
                "items": [
                    {
                        "order": "DD12345678",
                        "orderItemId": 54879848461,
                        "quantity": 1,
                        "packageId": 1
                    },
                    {
                        "order": "DD12345678",
                        "orderItemId": 54879848462,
                        "quantity": 3,
                        "packageId": 2
                    }
                ]
            }
        ```

+ Response 400 (application/json; charset=utf-8)

    + Body

        ```json
            {
              "errorCode": -2,
              "errorMessage": "Missing packageId in packages!"
            }
        ```



## Delete shipment {#reference-buyer-api--delete-shipment}

[/api/v1/shipment/{shipment}?token={token}]

***Buyer shipping mode method***

Deletes shipment created by *[Create shipment][create-shipment]* API message before *[Shipment departure][shipment-departure]*.


#### Rules for HTTP response status codes
 - **200** - OK status code. Message successfully processed. `errorCode` must be also `0`.
 - **400** - Bad request status code. Error ocured on application layer. See more in `errorCode` and `errorMessage`.
 - Any other status code is considered invalid and the request must be sent again according to the resend rules.

+ Parameters
    + shipment: SHIP123456789 ([String50][ds-string-50], required) - Shipment Number to delete
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token

### Delete shipment request [DELETE] {#reference-buyer-api--delete-shipment--delete-shipment-request-delete}

Request ([ShipmentDeleteRequest][ds-shipment-delete-request])  
Response ([GeneralResponse][ds-general-response])


+ Request Successful deletion (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 12345,
                "supplierBranchId": 212,
                "timestamp": "2025-06-01T19:33:43.513"
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

+ Request Failed deletion (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 12345,
                "supplierBranchId": 212,
                "timestamp": "2025-06-01T19:33:43.513"
            }
        ```

+ Response 400 (application/json; charset=utf-8)
    
    + Body

        ```json
            {
                "errorCode": -2,
                "errorMessage": "Unknown shipment!"
            }
        ```

## Shipment departure {#reference-buyer-api--shipment-departure}

[/api/v1/shipment/{shipment}/departure?token={token}]

***Required method***

Report **shipment** departure for one **shipment**. Shipment contains order items from one supplier branch which are 
transported to one address. The address could be the buyer's branch, parcel shop or end customer address. 
For the shipments delivered to the buyer's branch are required to group the orders to the consolidate packages.
It is also required to send the entire order in one shipment.

**Shipment consolidation rules**

| shipmentDeliveryType | Allowed | Required |
|----------------------|---------|----------|
| `B2C`                | No      | No       |
| `B2B`                | No      | No       |
| `Branch`             | Yes     | Yes      |
| `ParcelShop`         | No      | No       |

#### Rules for HTTP response status codes
 - **200** - OK status code. Message successfully processed. `errorCode` must be also `0`.
 - **400** - Bad request status code. Error ocured on application layer. See more in `errorCode` and `errorMessage`.
 - Any other status code is considered invalid and the request must be sent again according to the resend rules.

+ Parameters
    + shipment: SHIP12345678 ([String50][ds-string-50], required) - Shipment Number
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token

### Shipment departure request {#reference-buyer-api--shipment-departure--shipment-departure-request}

[POST]

Request ([ShipmentDepartureRequest][ds-shipment-departure-request])   
Response ([ShipmentDepartureResponse][ds-shipment-departure-response])  


+ Request Supplier shipping mode (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 12345,
                "supplierBranchId": 212,
                "timestamp": "2025-06-01T19:33:43.513",
                "shippingCarrier": {
                    "shippingCarrierCode": "GEISPARCEL",
                    "shippingCarrierDeliveryType": "GEISPOINT"
                },
                "parcelShop": {
                    "parcelShopIdentification": "GEISPOINT",
                    "parcelShopBranchCode": "123"
                },
                "expectedDeliveryDate": "2025-06-02",
                "cashOnDeliveryValue": 250.0,
                "cashOnDeliveryValueCurrency": "CZK",
                "shipmentValue": 300.0,
                "shipmentValueCurrency": "CZK",
                "shipmentWeight": 0.9,
                "shipmentVolume": 750,
                "packages": [
                    {
                        "number": "135NUM000A1",
                        "weight": 0.4,
                        "volume": 200
                    },
                    {
                        "number": "135NUM000A2",
                        "weight": 0.5,
                        "volume": 550
                    }
                ],
                "items": [
                    {
                        "order": "DD12345678",
                        "orderItemId": 54879848461,
                        "quantity": 1,
                        "packageNumber": "135NUM000A1",
                        "serials": ["SDF8774X1"]
                    },
                    {
                        "order": "DD12345678",
                        "orderItemId": 54879848462,
                        "quantity": 3,
                        "packageNumber": "135NUM000A1"
                    },
                    {
                        "order": "DD12345678",
                        "orderItemId": 54879848453,
                        "quantity": 2,
                        "packageNumber": "135NUM000A2",
                        "serials": ["ASD123A1", "ASD123A2"]
                    }
                ]
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


+ Request Buyer shipping mode (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 12345,
                "supplierBranchId": 212,
                "timestamp": "2025-06-01T19:33:43.513",
                "shippingCarrier": {
                    "shippingCarrierCode": "GEISPARCEL",
                    "shippingCarrierDeliveryType": "GEISPOINT"
                },
                "parcelShop": {
                    "parcelShopIdentification": "GEISPOINT",
                    "parcelShopBranchCode": "123"
                },
                "expectedDeliveryDate": "2025-06-02",
                "cashOnDeliveryValue": 250.0,
                "cashOnDeliveryValueCurrency": "CZK",
                "shipmentValue": 300.0,
                "shipmentValueCurrency": "CZK",
                "shipmentWeight": 0.9,
                "shipmentVolume": 750,
                "packages": [
                    {
                        "number": "135NUM000A1",
                        "weight": 0.4,
                        "volume": 200
                    },
                    {
                        "number": "135NUM000A2",
                        "weight": 0.5,
                        "volume": 550
                    }
                ],
                "items": [
                    {
                        "order": "DD12345678",
                        "orderItemId": 54879848461,
                        "quantity": 1,
                        "packageNumber": "135NUM000A1",
                        "serials": ["SDF8774X1"]
                    },
                    {
                        "order": "DD12345678",
                        "orderItemId": 54879848462,
                        "quantity": 3,
                        "packageNumber": "135NUM000A1"
                    },
                    {
                        "order": "DD12345678",
                        "orderItemId": 54879848453,
                        "quantity": 2,
                        "packageNumber": "135NUM000A2",
                        "serials": ["ASD123A1", "ASD123A2"]
                    }
                ]
            }
        ```

+ Response 200 (application/json; charset=utf-8)
    
    + Body

        ```json
            {
                "errorCode": 0,
                "errorMessage": "",
                "shipment": {
                    "departureTime": "2025-06-02T08:00:00.000",
                    "shippingList": {
                        "shippingListId": 1234567,
                        "pdf": "https://test.buyer.cz/Apps/pdfdoc.asp?s=1234567AB&x=27s40308532105133N2D17264251"
                    },
                    "shippingListGroup": {
                        "shippingListGroupId": 12345,
                        "pdf": "https://test.buyer.cz/Apps/pdfdoc.asp?s=12345CD&x=27sN2D1726425140308532105133"
                    }
                }
            }
        ```

+ Request Invalid shipment departure (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 12345,
                "supplierBranchId": 212,
                "timestamp": "2025-06-01T19:33:43.513",
                "shippingCarrier": {
                    "shippingCarrierCode": "GEISPARCEL",
                    "shippingCarrierDeliveryType": "GEISPOINT"
                },
                "parcelShop": {
                    "parcelShopIdentification": "GEISPOINT",
                    "parcelShopBranchCode": "123"
                },
                "expectedDeliveryDate": "2025-06-02",
                "cashOnDeliveryValue": 250.0,
                "cashOnDeliveryValueCurrency": "CZK",
                "shipmentValue": 300.0,
                "shipmentValueCurrency": "CZK",
                "shipmentWeight": 0.9,
                "shipmentVolume": 750,
                "packages": [
                    {
                        "number": "135NUM000A1",
                        "weight": 0.4,
                        "volume": 200
                    },
                    {
                        "number": "135NUM000A2",
                        "weight": 0.5,
                        "volume": 550
                    }
                ]
            }
        ```

+ Response 400 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": -2,
                "errorMessage": "Order items missing"
            }
        ```


## Track and Trace {#reference-buyer-api--track-and-trace}

[/api/v1/track?token={token}]

***Conditionally optional method.***

Update shipment Track and Trace information.

Method is required in case of the supplier's own transport contract.

**At least one of the following attributes must be filled, even if they are marked as optional:**

  - order
  - shipment
  - package
  - fullPackageNumber
  
For shipments with `shipmentDeliveryType` ParcelShop sent in *[Confirm order][confirm-order]* is required to send Stored `status` before Delivered `status`.

#### Rules for HTTP response status codes
 - **200** - OK status code. Message successfully processed. `errorCode` must be also `0`.
 - **400** - Bad request status code. Error ocured on application layer. See more in `errorCode` and `errorMessage`.
 - Any other status code is considered invalid and the request must be sent again according to the resend rules.

+ Parameters
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token
    
### Track and Trace request  {#reference-buyer-api--track-and-trace--track-and-trace-request}

[POST]

Request ([TrackAndTraceRequest][ds-track-and-trace-request])  
Response ([GeneralResponse][ds-general-response])


+ Request Delivered to the depot (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 123456,
                "timestamp": "2025-06-01T19:33:43.513",
                "order": "DD12345678",
                "package": "135487AA785BBCCEE",
                "fullPackageNumber": "135487AA785BBCCEEZZZ11133355",
                "status": "Depot",
                "statusTimestamp": "2025-06-01T19:30:00.000"
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

+ Request Final delivery (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 123456,
                "timestamp": "2025-06-01T19:33:43.513",
                "order": "DD12345678",
                "package": "135487AA785BBCCEE",
                "fullPackageNumber": "135487AA785BBCCEEZZZ11133355",
                "status": "Delivery",
                "statusTimestamp": "2025-06-01T19:30:00.000"
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

+ Request Delivered to the end customer or buyer's branch (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 123456,
                "timestamp": "2025-06-01T19:33:43.513",
                "order": "DD12345678",
                "package": "135487AA785BBCCEE",
                "fullPackageNumber": "135487AA785BBCCEEZZZ11133355",
                "status": "Delivered",
                "statusTimestamp": "2025-06-01T19:30:00.000"
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

+ Request Stored at parcel shop (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 123456,
                "timestamp": "2025-06-01T19:33:43.513",
                "order": "DD12345678",
                "package": "135487AA785BBCCEE",
                "fullPackageNumber": "135487AA785BBCCEEZZZ11133355",
                "status": "Stored",
                "statusTimestamp": "2025-06-01T19:30:00.000"
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

+ Request Rejected by the end customer or buyer's branch (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 123456,
                "timestamp": "2025-06-01T19:33:43.513",
                "order": "DD12345678",
                "package": "135487AA785BBCCEE",
                "fullPackageNumber": "135487AA785BBCCEEZZZ11133355",
                "status": "Rejected",
                "statusTimestamp": "2025-06-01T19:30:00.000"
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

+ Request Invalid update (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 123456,
                "timestamp": "2025-06-01T19:33:43.513",
                "order": "DD12345678",
                "package": "135487AA785BBCCEE",
                "fullPackageNumber": "135487AA785BBCCEEZZZ11133355",
                "status": "Delivered",
                "statusTimestamp": "2025-06-01T19:30:00.000"
            }
        ```

+ Response 400 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": -2,
                "errorMessage": "Invalid order number"
            }
        ```


## Delivery result {#reference-buyer-api--delivery-result}

[/api/v1/order/{order}/delivery?token={token}]

***Required method.***

Order delivery final result.

Method is used in case of these situations:

 - issues with shipping, supplier wants to cancel order
 - the package was returned back to supplier's branch as a return shipment
 - supplier uses own carriage and report delivery result

#### Rules for HTTP response status codes
 - **200** - OK status code. Message successfully processed. `errorCode` must be also `0`.
 - **400** - Bad request status code. Error ocured on application layer. See more in `errorCode` and `errorMessage`.
 - Any other status code is considered invalid and the request must be sent again according to the resend rules.

+ Parameters
    + order: DD12345678 ([OrderNumber][ds-order-number], required) - Order Number
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token

### Delivery result request {#reference-buyer-api--delivery-result--delivery-result-request}

[POST]

Request ([DeliveryResultRequest][ds-delivery-result-request])  
Response ([GeneralResponse][ds-general-response])


+ Request Delivery result Delivered (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 123456,
                "timestamp": "2025-06-01T19:33:43.513",
                "status": "Delivered",
                "statusTimestamp": "2025-06-01T19:30:00.000",
                "paymentVS": "123456781"
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

+ Request Delivery result Rejected (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 123456,
                "timestamp": "2025-06-01T19:33:43.513",
                "status": "Rejected",
                "statusTimestamp": "2025-06-01T19:30:00.000",
                "errorReason": "Rejected by the end customer or buyer",
                "paymentVS": "123456781"
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

+ Request Delivery result Canceled (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 123456,
                "timestamp": "2025-06-01T19:33:43.513",
                "status": "Canceled",
                "statusTimestamp": "2025-06-01T19:30:00.000",
                "errorReason": "Damaged during handling",
                "paymentVS": "123456781",
                "errorProducts": [
                    {
                        "code": "AXO001",
                        "quantity": 1
                    }
                ]
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

+ Request Invalid update (application/json; charset=utf-8)

    + Body

        ```json
            {
                "supplierId": 123456,
                "timestamp": "2025-06-01T19:33:43.513",
                "status": "Canceled",
                "statusTimestamp": "2025-06-01T19:30:00.000",
                "errorReason": "Damaged during handling",
                "paymentVS": "123456781",
                "errorProducts": [
                    {
                        "code": "AXO001",
                        "quantity": 1
                    }
                ]
            }
        ```

+ Response 400 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": -2,
                "errorMessage": "Can't cancel delivered order"
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
