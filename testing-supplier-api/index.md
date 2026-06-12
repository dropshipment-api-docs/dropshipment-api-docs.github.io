---
layout: default
nav_order: 5
title: Testing Supplier API
---

# Testing Supplier API {#reference-testing-supplier-api}
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

The Testing Supplier API is consists of endpoints that invokes requests to *[Supplier API][supplier-api]*.
API is implemented on buyer side.

## Insert order {#reference-testing-supplier-api--insert-order}

[/api/v2/order/insert/{test}?token={token}]

A testing endpoint to invoke *[Insert order][insert-order]* request to Supplier API

Also initiate new test and deactivate previous one.

+ Parameters
    + test: T001 ([String30][ds-string-30], required) - Test number 
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token

### Invoke Insert order request {#reference-testing-supplier-api--insert-order--invoke-insert-order-request}

[POST]

Request ([InvokerOrderInsertRequest][ds-invoker-order-insert-request])  
Response ([InvokerOrderInsertResponse][ds-invoker-order-insert-response])  


+ Request Successful reservation (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "codes": [
                    "AXO001",
                    "AXO002"
                ]
            }
        ```

+ Response 200 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": 0,
                "errorMessage": "The test case is still in progress.",
                "responseHTTPStatusCode": 201,
                "responseObject": {
                    "errorCode": 0,
                    "errorMessage": "",
                    "supplierOrder": "A56789123456",
                    "validUntil": "2025-07-01T00:00:00.000"
                }
            }
        ```


+ Request Intended Out of stock (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "codes": [
                    "AXO001",
                    "AXO002"
                ]
            }
        ```

+ Response 200 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": 0,
                "errorMessage": "The test case is completed successfully.",
                "responseHTTPStatusCode": 400,
                "responseObject": {
                    "errorCode": -3,
                    "errorMessage": "Out of stock",
                    "errorProducts": [
                        {
                            "code": "AXO001",
                            "quantity": 1
                        }
                    ]
                }
            }
        ```

+ Request Unintended Out of stock (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "codes": [
                    "AXO001",
                    "AXO002"
                ]
            }
        ```

+ Response 400 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": -6,
                "errorMessage": "The test case failed. Unexpected response errorCode. Expects 0. Receive -3",
                "responseHTTPStatusCode": 400,
                "responseObject": {
                    "errorCode": -3,
                    "errorMessage": "Out of stock",
                    "errorProducts": [
                        {
                            "code": "AXO001",
                            "quantity": 1
                        }
                    ]
                }
            }
        ```

+ Request Invalid Supplier Testing URL (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "customerId": 1,
                "supplierId": 100,
                "supplierBranchId": 123,
                "codes": [
                    "AXO001",
                    "AXO002"
                ]
            }
        ```

+ Response 400 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": -1,
                "errorMessage": "Problem with send request to Dropshipper!"
            }
        ```



## Extend order {#reference-testing-supplier-api--extend-order}

[/api/v2/order/extend/{test}?token={token}]

A testing endpoint to invoke *[Extend order][extend-order]* request to Supplier API

+ Parameters
    + test: T001 ([String30][ds-string-30], required) - Test number
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token

### Invoke Extend order request {#reference-testing-supplier-api--extend-order--invoke-extend-order-request}

[POST]

Request ([InvokerSimpleRequest][ds-invoker-simple-request])  
Response ([InvokerOrderExtendResponse][ds-invoker-order-extend-response])  


+ Request Successful extension of the reservation (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "supplierId": 1
            }
        ```

+ Response 200 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": 0,
                "errorMessage": "The test case is still in progress.",
                "responseHTTPStatusCode": 200,
                "responseObject": {
                    "errorCode": 0,
                    "errorMessage": "",
                    "validUntil": "2025-07-01T00:00:00.000"
                }
            }
        ```

+ Request Intended failed reservation (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "supplierId": 1
            }
        ```

+ Response 200 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": 0,
                "errorMessage": "The test case is completed successfully.",
                "responseHTTPStatusCode": 400,
                "responseObject": {
                    "errorCode": -5,
                    "errorMessage": "Rejected"
                }
            }
        ```

+ Request Unintended failed reservation (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "supplierId": 1
            }
        ```

+ Response 400 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": -6,
                "errorMessage": "The test case failed. Unexpected response errorCode. Expects 0. Receive -5",
                "responseHTTPStatusCode": 400,
                "responseObject": {
                    "errorCode": -5,
                    "errorMessage": "Rejected"
                }
            }
        ```



## Cancel order {#reference-testing-supplier-api--cancel-order}

[/api/v2/order/cancel/{test}?token={token}]

A testing endpoint to invoke *[Cancel order][cancel-order]* request to Supplier API

+ Parameters
    + test: T001 ([String30][ds-string-30], required) - Test number 
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token

### Invoke Cancel order request {#reference-testing-supplier-api--cancel-order--invoke-cancel-order-request}

[POST]

Request ([InvokerSimpleRequest][ds-invoker-simple-request])  
Response ([InvokerOrderCancelResponse][ds-invoker-order-cancel-response])  

+ Request Successful Cancel order (application/json; charset=utf-8)
    
    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "supplierId": 1
            }
        ```

+ Response 200 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": 0,
                "errorMessage": "The test case is completed successfully.",
                "responseHTTPStatusCode": 200,
                "responseObject": {
                    "errorCode": 0,
                    "errorMessage": ""
                }
            }
        ```

+ Request Failed Cancel order (application/json; charset=utf-8)
    
    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "supplierId": 1
            }
        ```

+ Response 200 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": -6,
                "errorMessage": "The test case failed. Unexpected response errorCode. Expects 0. Receive -5",
                "responseHTTPStatusCode": 400,
                "responseObject": {
                    "errorCode": -5,
                    "errorMessage": "Rejected"
                }
            }
        ```



## Confirm order {#reference-testing-supplier-api--confirm-order}

[/api/v2/order/confirm/{test}?token={token}]

Provides ability to invoke *[Confirm order][confirm-order]* request to Supplier API

+ Parameters
    + test: T001 ([String30][ds-string-30], required) - Test number 
    + token: jDGARg+SaXMa8Ib++O92+ZX3ITQ= ([HmacToken][ds-hmac-token], required) - HMAC Authentication token

### Invoke Confirm order request {#reference-testing-supplier-api--confirm-order--invoke-confirm-order-request}

[POST]

Request ([InvokerSimpleRequest][ds-invoker-simple-request])  
Response ([InvokerOrderConfirmResponse][ds-invoker-order-confirm-response])  


+ Request Successful Confirm order (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "supplierId": 1
            }
        ```

+ Response 200 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": 0,
                "errorMessage": "The test case is still in progress.",
                "responseHTTPStatusCode": 200,
                "responseObject": {
                    "errorCode": 0,
                    "errorMessage": ""
                }
            }
        ```

+ Request Failed Confirm order (application/json; charset=utf-8)

    + Body

        ```json
            {
                "timestamp": "2025-06-01T19:33:43.513",
                "supplierId": 1
            }
        ```

+ Response 400 (application/json; charset=utf-8)

    + Body

        ```json
            {
                "errorCode": -6,
                "errorMessage": "The test case failed. Unexpected response errorCode. Expects 0. Receive -5",
                "responseHTTPStatusCode": 400,
                "responseObject": {
                    "errorCode": -5,
                    "errorMessage": "Rejected"
                }
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
