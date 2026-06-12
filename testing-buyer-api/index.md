---
layout: default
nav_order: 4
title: Testing Buyer API
---

# Testing Buyer API {#reference-testing-buyer-api}
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

The Testing Buyer API has the same structure as *[production Buyer API][buyer-api]* but `test` variable is added to the URL. 
API is implemented on buyer side.

## Availability {#reference-testing-buyer-api--availability}

[/api/v2/availability?token={token}&test={test}]

A testing endpoint for buyer *[Availability][availability]* method. See *[Availability][availability]* for more details.

A testing endpoint accepts a maximum of 100 products.

+ Parameters
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token
    + test: T001 ([String30][ds-string-30], required) - Test number 

### Test Availability request {#reference-testing-buyer-api--availability--test-availability-request}

[POST]

Request ([AvailabilityRequest][ds-availability-request])  
Response ([GeneralResponse][ds-general-response])  


+ Request PartialFull import for Supplier product pricing  (application/json; charset=utf-8)

    + Attributes ()

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


+ Request Invalid request (application/json; charset=utf-8)

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
                        "ean": "Product-EAN",
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


## Create shipment {#reference-testing-buyer-api--create-shipment}

[/api/v2/shipment?token={token}&test={test}]

A testing endpoint for buyer *[Create shipment][create-shipment]* method. See *[Create shipment][create-shipment]* for more details.

+ Parameters
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token
    + test: T001 ([String30][ds-string-30], required) - Test number 

### Test Create shipment request {#reference-testing-buyer-api--create-shipment--test-create-shipment-request}

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
                "shipmentValue": 199.0,
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

+ Response 200 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": 0,
                "errorMessage": "The test case is still in progress.",
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
                "shipmentValue": 199.0,
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
                "errorMessage": "The test case failed. Missing packageId in packages!"
            }
        ```



## Delete shipment {#reference-testing-buyer-api--delete-shipment}

[/api/v2/shipment/{shipment}?token={token}&test={test}]

A testing endpoint for buyer *[Delete shipment][delete-shipment]* method. See *[Delete shipment][delete-shipment]* for more details.

+ Parameters
    + shipment: SHIP12345678 ([String50][ds-string-50], required) - Shipment Number to delete
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token
    + test: T001 ([String30][ds-string-30], required) - Test number 

### Test Delete shipment request [DELETE] {#reference-testing-buyer-api--delete-shipment--test-delete-shipment-request-delete}

Request ([ShipmentDeleteRequest][ds-shipment-delete-request])  
Response ([GeneralResponse][ds-general-response]) 

 
+ Request Successful Delete shipment (application/json; charset=utf-8)

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
                "errorMessage": "The test case is completed successfully."
            }
        ```

+ Request Failed Delete shipment (application/json; charset=utf-8)

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
                "errorMessage": "The test case failed. Unknown shipment!"
            }
        ```


## Shipment departure {#reference-testing-buyer-api--shipment-departure}

[/api/v2/shipment/{shipment}/departure?token={token}&test={test}]

A testing endpoint for buyer *[Shipment departure][shipment-departure]* method. 
See *[Shipment departure][shipment-departure]* for more details.

+ Parameters
    + shipment: SHIP12345678 ([String50][ds-string-50], required) - Shipment Number 
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token
    + test: T001 ([String30][ds-string-30], required) - Test number 

### Test Shipment departure request {#reference-testing-buyer-api--shipment-departure--test-shipment-departure-request}

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
                "shipmentValue": 199.0,
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
                "errorMessage": "The test case is still in progress."
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
                "shipmentValue": 199.0,
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
                "errorMessage": "The test case is still in progress.",
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
                "shipmentValue": 199.0,
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
                "errorMessage": "The test case failed. Order items missing"
            }
        ```



## Track and Trace {#reference-testing-buyer-api--track-and-trace}

[/api/v2/track?token={token}&test={test}]

A testing endpoint for buyer *[Track and Trace][track-and-trace]* method. 
See *[Track and Trace][track-and-trace]* for more details.

+ Parameters
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token
    + test: T001 ([String30][ds-string-30], required) - Test number 

### Test Track and Trace request {#reference-testing-buyer-api--track-and-trace--test-track-and-trace-request}

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
                 "errorMessage": "The test case is still in progress."
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
                 "errorMessage": "The test case is still in progress."
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
                 "errorMessage": "The test case is still in progress."
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
                 "errorMessage": "The test case is still in progress."
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
                 "errorMessage": "The test case is still in progress."
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
                "errorMessage": "The test case failed. Invalid order number"
            }
        ```


## Delivery result {#reference-testing-buyer-api--delivery-result}

[/api/v2/order/{order}/delivery?token={token}&test={test}]

A testing endpoint for buyer *[Delivery result][delivery-result]* method. 
See *[Delivery result][delivery-result]* for more details.

+ Parameters
    + order: DD12345678 ([OrderNumber][ds-order-number], required) - Order Number
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token
    + test: T001 ([String30][ds-string-30], required) - Test number 

### Test Delivery result request {#reference-testing-buyer-api--delivery-result--test-delivery-result-request}

[POST]

Request ([DeliveryResultRequest][ds-delivery-result-request])  
Response ([GeneralResponse][ds-general-response])  

+ Request Delivered (application/json; charset=utf-8)

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
                "errorMessage": "The test case is completed successfully."
            }
        ```

+ Request Rejected (application/json; charset=utf-8)

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
                "errorMessage": "The test case is completed successfully."
            }
        ```

+ Request Canceled (application/json; charset=utf-8)

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
                "errorMessage": "The test case is completed successfully."
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
                "errorMessage": "The test case failed. Can't cancel delivered order"
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
