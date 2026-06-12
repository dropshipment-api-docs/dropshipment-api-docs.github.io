---
layout: default
nav_order: 6
title: Data Structures
---


# Data Structures {#data-structures}
{: .no_toc }

### Timestamp (string) {#data-structures--timestamp}
Date + time format in [CET (Central European Time)](https://time.is/cs/CET) (`YYYY-MM-DDThh:mm:ss.nnn`).

Example: `2025-06-01T19:33:43.513`

### TimestampUtc (string) {#data-structures--timestamputc}
Date + time format in [UTC (Coordinated Universal Time)](https://time.is/cs/UTC) (`YYYY-MM-DDThh:mm:ss.nnn`).

Example: `2025-06-01T18:33:43.513`

### Date (string) {#data-structures--date}
Simple date format (`YYYY-MM-DD`).

Example: `2025-06-01`

### Int16 (number) {#data-structures--int-16}
16-bit signed integer number.

Example: `1234`

### Int32 (number) {#data-structures--int-32}
32-bit signed integer number.

Example: `-123456` `123456`

### Int64 (number) {#data-structures--int-64}
64-bit signed integer number.

Example: `12345678901`

### Float (number) {#data-structures--float}
Approximate floating-point numeric

Example: `1.123456`

### String10 (string) {#data-structures--string-10}
A string with a maximum length of 10 characters.

### String20 (string) {#data-structures--string-20}
A string with a maximum length of 20 characters.

### String30 (string) {#data-structures--string-30}
A string with a maximum length of 30 characters.

### String50 (string) {#data-structures--string-50}
A string with a maximum length of 50 characters.

### String100 (string) {#data-structures--string-100}
A string with a maximum length of 100 characters.

### String500 (string) {#data-structures--string-500}
A string with a maximum length of 500 characters.

### CustomerId ([Int32][ds-int-32]) {#data-structures--customer-id}
32-bit signed integer number.

It can be set for each branch of the supplier separately or it can be the same for all branches.

### OrderNumber ([String30][ds-string-30]) {#data-structures--order-number}
A string with a maximum length of 30 characters. 
Currently, two formats are possible.
The old one has about 10 digits.
And the new one with the prefix DD and about 8 digits.
The format may change in the future.

Old format example: `5478519223`

New format example: `DD14298199`

### GUID (string) {#data-structures--guid}
Globally Unique IDentifier in 4-dashed lowercase format [RFC 4122](https://datatracker.ietf.org/doc/html/rfc4122)

Example: `a20dc9c1-e0d6-4c17-97bc-3d87438307db`

### GLN (string) {#data-structures--gln}
Global Location Number. A string with a length of 13 characters according to **ISO 6523**.

Example: `9506000140445`

### SupplierProductCode ([String50][ds-string-50]) {#data-structures--supplier-product-code}
A case insensitive string with a maximum length of 50.

A character ruleset:
• Allows alphanumeric characters and diacritics.
• Allows special characters: `_` `-` `:` `/` `.` `#` `,` `(` `)` `+` `*` 
• Whitespace at the beginning and end of the string is ignored.

### Weight ([Float][ds-float]) {#data-structures--weight}
Decimal numeric with precision 9 and scale 4.

Min value: `0.0` Max value: `99999.9999`

Example: `5.2468`

### Volume ([Float][ds-float]) {#data-structures--volume}
Decimal numeric with precision 15 and scale 4.

Min value: `0.0` Max value: `9999999999.9999`

Example: `100000`

### Money ([Float][ds-float]) {#data-structures--money}
Decimal numeric with precision 15 and scale 2.

Min value: `0.0` Max value: `9999999999.99`

Example: `149.99`

### VAT ([Float][ds-float]) {#data-structures--vat}
Decimal numeric with precision 9 and scale 2.

Min value: `0.0` Max value: `99.99`

Example: `15.55`

### Number ([Int32][ds-int-32]) {#data-structures--number}
32-bit signed integer number.

Min value: `0` Max value: `2147483647`

Example: `15`

### Id ([Int32][ds-int-32]) {#data-structures--id}
32-bit signed integer number.

Min value: `1` Max value: `2147483647`

Example: `15`

### Id64 ([Int64][ds-int-64]) {#data-structures--id-64}
64-bit signed integer number.

Min value: `1` Max value: `9223372036854775807`

Example: `372036854775807`

### HmacToken (string) {#data-structures--hmac-token}
HMAC Authentication token

Example: `jDGARg+SaXMa8Ib++O92+ZX3ITQ=`


### Country (enum[string]) {#data-structures--country}
2 letter country code according to **ISO 3166-1 Alpha-2**. 
See *[Wiki][wiki-country-code]* or *[ISO][iso-country-code]* for more information.

Examples
+ `CZ`
+ `SK`
+ `DE`

### Currency (enum[string]) {#data-structures--currency}
3 letter currency code code according to **ISO 4217**. 
See *[Wiki][wiki-currency-code]* or *[ISO][iso-currency-code]* for more information.

Examples
+ `CZK`
+ `EUR`
+ `USD`

### ErrorCode (enum[number]) {#data-structures--error-code}
+  `0` - Success.
+ `-1` - Generic error (more info in `errorMessage`). 
+ `-2` - Invalid input data.                          
+ `-3` - Out of stock.                                
+ `-4` - Invalid price.                               
+ `-5` - Operation rejected.                           
+ `-6` - Bad response.   

### SuccessErrorCode (enum[number]) {#data-structures--success-error-code}
+  `0` - Success (No error / Warning message).  

### FailErrorCode (enum[number]) {#data-structures--fail-error-code}
+ `-1` - Generic error(more info in `errorMessage`). 
+ `-2` - Invalid input data.                          
+ `-3` - Out of stock.                                
+ `-4` - Invalid price.                               
+ `-5` - Operation rejected.                            
+ `-6` - Bad response.  

### ImportType (enum[string]) {#data-structures--import-type}
+ `PartialFull` - Update only provided items. Used for nightly batch import.
+ `Update` - Update only provided items
+ `Full` - Missing items in Full import are considered as unavailable. **Deprecated**

### TrackAndTraceStatus (enum[string]) {#data-structures--track-and-trace-status}
+ `Depot` - The shipment was delivered to carrier depot.
+ `Delivery` - The shipment is being delivered to the recipient from depot.
+ `Stored` - The shipment was stored at parcel shop for pickup by the end customer.
+ `Delivered` - The shipment was delivered to the end customer or buyer branch.
+ `Rejected` - The shipment was rejected.

### DeliveryResultStatus (enum[string]) {#data-structures--delivery-result-status}
+ `Canceled` - Canceled by supplier (issues with goods)
+ `Delivered` - Sucessfully delivered to the end customer or buyer branch
+ `Rejected` - Rejected by the end customer or buyer, returned back to supplier

### ShipmentDeliveryType (enum[string]) {#data-structures--shipment-delivery-type}
+ `B2C` - End customer client (carrier will contact customer)
+ `B2B` - Business client
+ `Branch` - Delivery to branch
+ `ParcelShop` - Delivery to parcel shop

### ShipmentShippingMode (enum[string]) {#data-structures--shipment-shipping-mode}
+ `Buyer` - Buyer handles *shipment number*, *package numbers*, *shipping list*, *shipping sticker* and *carrier data*
+ `Supplier` - Supplier handles *shipment number*, *package numbers*, *shipping list*, *shipping sticker* and *carrier data*

### ShippingCarrierCode (enum[string]) {#data-structures--shipping-carrier-code}
+ `ALZA` - Alza
+ `CZPOST` - Czech Post
+ `DHL` - DHL
+ `DPD` - DPD Czechia
+ `DPDSK` - DPD Slovakia
+ `DPDHU` - DPD Hungary
+ `FOFR` - RSC Logistics
+ `GebruderWeiss` - Gebruder Weiss
+ `GEISPARCEL` - Geis Parcel
+ `GEISCARGO` - Geis Cargo
+ `GLS` - GLS
+ `GO` - GO!
+ `HELICAR` - HELICAR
+ `MagyarPOST` - Magyar Posta 
+ `Najbert` - Courier Najbert
+ `PPL` - PPL
+ `RHENUS` - Rhenus HD
+ `SKPOST` - Slovakia Post
+ `SKYNET` - SKYNET
+ `TOPTRANS` - TOPTRANS
+ `UPS` - UPS
+ `WEDO` - WE DO
+ `ZASILKOVNA` - Packeta
+ `ZavolejSiKuryra` - Zavolejsikuryra.cz

### ShippingCarrierDeliveryType (enum[string]) {#data-structures--shipping-carrier-delivery-type}
+ `Supplier`
    For Confirm order message, it means that the supplier is choosing the best delivery type.
    For other messages, it means than the supplier is shipping carrier.
+ `COURIER` 
    Universal courier delivery type. At this time just for Shipping carrier code `Najbert`
+ `ALZABRANCH` - Alza branch delivery for shipping carrier code `ALZA`
+ `ALZABOX` - AlzaBox delivery for shipping carrier code `ALZA`
+ `CZPOSTD` - Address delivery for shipping carrier code `CZPOST`
+ `CZPOSTP` - Post office delivery for shipping carrier code `CZPOST`
+ `CZPOSTB` - BalĂ­kovna delivery for shipping carrier code `CZPOST`
+ `DHL` - For shipping carrier code `DHL`
+ `DPD` - Address delivery for shipping carrier code `DPD`
+ `DPDSK` - Address delivery for shipping carrier code `DPDSK`
+ `DPDHU` - Address delivery for shipping carrier code `DPDHU`
+ `DPDALZABOX` - AlzaBox delivery for shipping carrier code `DPD`
+ `DPDBOX` - DPDBox delivery for shipping carrier code `DPD`
+ `DPDPARCELSHOP` - ParcelShop delivery for shipping carrier code `DPD`
+ `FOFRSTD` - For shipping carrier code `FOFR`
+ `GebruderWeissStandard` - For shipping carrier code `GebruderWeiss`
+ `GEIS` - Address delivery for shipping carrier code `GEISPARCEL`
+ `GEISPOINT` - Geis Point delivery for shipping carrier code  `GEISPARCEL`
+ `GEISCARGO` - For shipping carrier code `GEISCARGO`
+ `GLS` - For shipping carrier code `GLS`
+ `GO` - For shipping carrier code `GO`
+ `HELICARSTD` - Standard delivery for shipping carrier code `HELICAR`
+ `HELICARUP` - Upstairs delivery for shipping carrier code `HELICAR` 
+ `MagyarPOSTHD` - Address delivery for shipping carrier code `MagyarPOST`
+ `MagyarPOSTPO` - Post office delivery for shipping carrier code `MagyarPOST`
+ `MagyarPOSTPP` - Post Point delivery for shipping carrier code `MagyarPOST`
+ `MagyarPOSTPT` - Parcel Terminal delivery for shipping carrier code `MagyarPOST`
+ `PPL` - Address delivery for shipping carrier code `PPL`
+ `PPLPARCELSHOP` - Parcelshop delivery for shipping carrier code `PPL` 
+ `RHENUS` - For shipping carrier code `RHENUS`
+ `SKPOSTD` - Address delivery for shipping carrier code `SKPOST`
+ `SKPOSTP` - Post office delivery for shipping carrier code `SKPOST`
+ `SKYNET` - For shipping carrier code `SKYNET`
+ `TOPTRANS` - For shipping carrier code `TOPTRANS`
+ `UPS` - For shipping carrier code `UPS`
+ `WEDOHD` - Home delivery `WEDO`
+ `ZASILKOVNA` - For shipping carrier code `ZASILKOVNA`
+ `ZavolejSiKuryra` - For shipping carrier code `ZavolejSiKuryra`

### ParcelShopIdentification (enum[string]) {#data-structures--parcel-shop-identification}
+ `ALZABOX` - AlzaBox delivery for shipping carrier code `ALZA`
+ `CZPOSTB` - BalĂ­kovna for shipping carrier code `CZPOST`
+ `CZPOSTP` - Post office delivery for shipping carrier code `CZPOST`
+ `DPDALZABOX` - AlzaBox delivery for shipping carrier code `DPD`
+ `DPDBOX` - DPDBox delivery for shipping carrier code `DPD`
+ `DPDPARCELSHOP` - ParcelShop delivery for shipping carrier code `DPD`
+ `GEISPOINT` - Geis Point delivery for shipping carrier code  `GEISPARCEL`
+ `PPLPARCELSHOP` - Parcelshop delivery for shipping carrier code `PPL` 
+ `ZASILKOVNA` - For shipping carrier code `ZASILKOVNA`

### PackageSortingGroup (enum[string]) {#data-structures--package-sorting-group}
+ `RegularDirect` - Default group
+ `Linehaul` - Linehaul group
+ `CrossLC` - CrossLC group

### ParcelShop (object) {#data-structures--parcel-shop}
+ **parcelShopIdentification** ([ParcelShopIdentification][ds-parcel-shop-identification], required) - Parcel shop identification
+ **parcelShopBranchCode** ([String50][ds-string-50], required) - Parcel shop branch identification

### ShippingCarrierConfirm (object) {#data-structures--shipping-carrier-confirm}
+ **shippingCarrierCode** ([ShippingCarrierCode][ds-shipping-carrier-code], optional) - Shipping carrier code. For `Supplier` delivery type could be attribute empty. 
+ **shippingCarrierDeliveryType** ([ShippingCarrierDeliveryType][ds-shipping-carrier-delivery-type], required) - Shipping carrier delivery type

### ShippingCarrier (object) {#data-structures--shipping-carrier}
+ **shippingCarrierCode** ([ShippingCarrierCode][ds-shipping-carrier-code], optional) - Required same Shipping carrier code as sent in Confirm order.
+ **shippingCarrierDeliveryType** ([ShippingCarrierDeliveryType][ds-shipping-carrier-delivery-type], required) - Shipping carrier delivery type

### ShippingCarrierStrict (object) {#data-structures--shipping-carrier-strict}
+ **shippingCarrierCode** ([ShippingCarrierCode][ds-shipping-carrier-code], required) - Shipping carrier code.
+ **shippingCarrierDeliveryType** ([ShippingCarrierDeliveryType][ds-shipping-carrier-delivery-type], required) - Shipping carrier delivery type

### CountryPrice (object) {#data-structures--country-price}
+ **country** ([Country][ds-country], optional)
    Optional if the country is the same as the branch country. Otherwise required.  
    Target country.
+ **currency** ([Currency][ds-currency], optional)
    Optional if the currency is the same as the import 'currency'. Otherwise required.  
    National currency of the `country`.
+ **vat** ([VAT][ds-vat], required)
    Value added tax in percentage (10, 15, 21, ...).
+ **purchasePriceWithoutFees** ([Money][ds-money], optional)
    Unit purchase price for buyer (excl. VAT, excl. recycling/copyright fee).
    Optional for **Latest price mode**. Required if attribute `sellingPriceWithoutVat` is empty.   
    Incompatible with `sellingPriceWithoutVat`, `price`, `priceWithFee` and `fee`.
+ **sellingPriceWithoutVat** ([Money][ds-money], optional)
    Unit selling price for the end customer (excl. VAT, incl. fees).   
    Optional for **Latest price mode**. Required if attribute `purchasePriceWithoutFees` is empty.
    Incompatible with `purchasePriceWithoutFees`.
+ **fees** ([CountryPriceFees][ds-country-price-fees], optional)
    Recycling and copyright unit fees. If it is not filled in, it means that the fees are 0.

### CountryPriceFees (object) {#data-structures--country-price-fees}
+ **copyright** ([Money][ds-money], optional) 
    Copyright unit fee. If it is not filled in, it means that the fee is 0.
+ **recycling** ([Money][ds-money], optional) 
    Recycling unit fee. If it is not filled in, it means that the fee is 0.

### Product (object) {#data-structures--product}
+ **code** ([SupplierProductCode][ds-supplier-product-code], required) - Supplier product code
+ **name** ([String500][ds-string-500], optional) - Product name
+ **ean** ([String20][ds-string-20], required) - Product EAN code
+ **quantity** ([Number][ds-number], required) - Amount available in stock. 
+ **limited** (boolean, optional)
    Amount in data is limited. We can try send an order that exceeds the reported quantity.   
    Example: Real availability 450, reported 50 ("50+").   
    Default value is `false`.
+ **serialNumbers** (boolean, optional)
    Serial numbers will be provided. If `true` then serial numbers will be expected 
    in `items[].serials` in *Shipment departure* API message.   
    Default value is `false`.  
+ **countryPrices** (array[[CountryPrice][ds-country-price]], optional)
    Required for **Latest price mode**.   
    Forbidden for **Legacy price mode**.   
    Price setting for target countries.
+ **availability** ([String100][ds-string-100], optional)
    Alternative delivery text information (`"7 days"`, `"3 weeks"`) (max 120 chars)
+ **expectedAvailability** ([Date][ds-date], optional)
    Expected availability date.
+ **size1** ([Number][ds-number], optional)
    **Deprecated - will be removed in the future.**
    
    Product size, smallest dimension (in mm).   
+ **size2** ([Number][ds-number], optional)
    **Deprecated - will be removed in the future.**
    
    Product size (in mm).   
+ **size3** ([Number][ds-number], optional)
    **Deprecated - will be removed in the future.**
    
    Product size, largest dimension (in mm).   
+ **weight** ([Weight][ds-weight], optional)
    **Deprecated - will be removed in the future.**
    
    Product weight (in kg).   
+ **price** ([Money][ds-money], optional)
    **Deprecated - replaced by attribute `countryPrices[].purchasePriceWithoutFees`**   
    Required for **Legacy price mode**.  
    Forbidden for **Latest price mode**.   
    Unit purchase price for buyer (excl. VAT, excl. recycling/copyright fee).
+ **priceWithFee** ([Money][ds-money], optional) 
    **Deprecated - without replacement**   
    Optional for **Legacy price mode**.   
    Forbidden for **Latest price mode**.   
    Unit purchase price for buyer (excl. VAT, incl. recycling/copyright fee).
    The fee is 0 if the `fee` and `priceWithFee` fields are not filled.
+ **fee** ([Money][ds-money], optional) 
    **Deprecated - replaced by attribute `countryPrices[].fees`**   
    Optional for **Legacy price mode**.   
    Forbidden for **Latest price mode**.   
    Recycling/copyright fee.   
    The fee is 0 if the `fee` and `priceWithFee` fields are not filled.
+ **vat** ([VAT][ds-vat], optional)
    **Deprecated - replaced by attribute `countryPrices[].vat`**   
    Required for **Legacy price mode**.   
    Forbidden for **Latest price mode**.     
    Value added tax in percentage (10, 15, 21, ...)    

### ErrorProduct (object) {#data-structures--error-product}
+ **code** ([SupplierProductCode][ds-supplier-product-code], required) - Supplier product code
+ **quantity** ([Number][ds-number], optional) - Amount available in stock (default `0`). 
+ **limited** (boolean, optional) - Amount in data is limited (default `false`)
+ **price** ([Money][ds-money], optional) - 
    **Deprecated - It is no longer used. The price correction must be sent via Availability**.
    
    Unit purchase price for buyer (excl. VAT, excl. recycling/copyright fee; default `original price`)

### DeliveryAddress (object) {#data-structures--delivery-address}
+ **companyName** ([String100][ds-string-100], optional) - Company name / Branch name. Required if `addressName` is empty. 
+ **addressName** ([String100][ds-string-100], optional) - Customer name. Required if `companyName` is empty.
+ **streetWithNumber** ([String100][ds-string-100], required) - Street address with number
+ **city** ([String100][ds-string-100], required) - City
+ **country** ([Country][ds-country], required) - Country code
+ **zip** ([String10][ds-string-10], required) - Zip Code (normalized, without spaces)
+ **phone** ([String30][ds-string-30], required) - Phone number
+ **email** ([String100][ds-string-100], required) - Email address
+ **note** ([String500][ds-string-500], optional) - Delivery note

### CompanyAddress (object) {#data-structures--company-address}
+ **companyName** ([String100][ds-string-100], required) - Company name 
+ **streetWithNumber** ([String100][ds-string-100], required) - Street address with number
+ **city** ([String100][ds-string-100], required) - City
+ **country** ([Country][ds-country], required) - Country code
+ **zip** ([String10][ds-string-10], required) - Zip Code (normalized, without spaces)

### ShipmentAddress (object) {#data-structures--shipment-address}
+ **companyName** ([String100][ds-string-100], optional) - Company name / Branch name. Required if `addressName` is empty. 
+ **addressName** ([String100][ds-string-100], optional) - Customer name. Required if `companyName` is empty.
+ **streetWithNumber** ([String100][ds-string-100], required) - Street address with number
+ **city** ([String100][ds-string-100], required) - City
+ **country** ([Country][ds-country], required) - Country code
+ **zip** ([String10][ds-string-10], required) - Zip Code (normalized, without spaces)

### ShipmentDeliveryServices (object) {#data-structures--shipment-delivery-services}
+ **oldApplianceRemoval** (boolean, optional) - Removal of old appliance
+ **carryIn** (boolean, optional) - Delivery to your apartment. Service may vary depending on the carrier.
+ **basicInstallation** (boolean, optional) - Basic installation. Service may vary by carrier.

### GLNList (object) {#data-structures--gln-list}
+ **buyerGln** ([GLN][ds-gln], optional) - GLN of the buying company
+ **orderedByGln** ([GLN][ds-gln], optional) - GLN of the ordering company
+ **invoiceeGln** ([GLN][ds-gln], optional) - GLN of the invoicing company
+ **shipmentDeliveryGln** ([GLN][ds-gln], optional) - GLN of the place where the shipment is delivered by the supplier

### CreatedShipment (object) {#data-structures--created-shipment}
+ **shipmentNumber** ([String50][ds-string-50], required) - Shipment identification
+ **packages** (array[[CreatedPackage][ds-created-package]], required) - List of created packages
+ **pdf** ([String500][ds-string-500], required) - Downloadable PDF with all carrier stickers for whole shipment

### CreatedPackage (object) {#data-structures--created-package}
+ **packageId** ([Id64][ds-id-64], optional) - `packageId` from request if contains
+ **number** ([String100][ds-string-100], required) - Created package number
+ **fullNumber** ([String100][ds-string-100], optional) - Created full package number
+ **pdf** ([String500][ds-string-500], required) - Downloadable PDF with carrier sticker

### ShipmentCreatePackage (object) {#data-structures--shipment-create-package}
+ **packageId** ([Id64][ds-id-64], required) - Identification of the package. Used to identify package in response.
+ **weight** ([Weight][ds-weight], required) - Weight (in kg)
+ **volume** ([Volume][ds-volume], optional) - Volume (in cm3)

### ShipmentCreateItem (object) {#data-structures--shipment-create-item}
+ **order** ([OrderNumber][ds-order-number], required) - Order number.
+ **orderItemId** ([Id64][ds-id-64], optional) - Unique *Order item ID*. **Preferred** item identification. 
  For **Branch delivery** is this attribute required.
+ **code** ([SupplierProductCode][ds-supplier-product-code], optional)
    Supplier product code.   
    Required for cases when you can't supply `orderItemId`.
+ **packageId** ([Id64][ds-id-64], required) - Identification of the package. Used to bond with `packages.packageId`.
+ **quantity** ([Number][ds-number], required) - Quantity.

### DeparturedShipment (object) {#data-structures--departured-shipment}
+ **departureTime** ([Timestamp][ds-timestamp], optional) - Shipment departure time in CET
+ **shippingList** ([ShippingList][ds-shipping-list], required) - Shipping list
+ **shippingListGroup** ([ShippingListGroup][ds-shipping-list-group], optional) - Shipping list group

### ShippingList (object) {#data-structures--shipping-list}
+ **shippingListId** ([Id][ds-id], required) - Shipping list ID
+ **pdf** ([String500][ds-string-500], required) - Downloadable PDF with shipping list

### ShippingListGroup (object) {#data-structures--shipping-list-group}
+ **shippingListGroupId** ([Id][ds-id], required) - Shipping list group ID
+ **pdf** ([String500][ds-string-500], required) - Downloadable PDF with shipping list group

### ShipmentDeparturePackage (object) {#data-structures--shipment-departure-package}
+ **number** ([String100][ds-string-100], required) - Package number (short, internal)
+ **fullNumber** ([String100][ds-string-100], optional) - Full package number (identical to the package sticker. Substring is usually 
  used as tracking number for track and trace)
+ **ttUrl** ([String500][ds-string-500], optional) - Track and Trace URL (prefered way to provide correct Track and Trace)
+ **weight** ([Weight][ds-weight], required) - Weight (in kg)
+ **volume** ([Volume][ds-volume], optional) - Volume (in cm3)
+ **value** ([Money][ds-money], optional) - Package value
+ **valueCurrency** ([Currency][ds-currency], optional) - Package value currency code

### ShipmentDepartureItem (object) {#data-structures--shipment-departure-item}
+ **order** ([OrderNumber][ds-order-number], required) - Order number
+ **orderItemId** ([Id64][ds-id64], optional)
    Unique *Order item ID*. Preferred item identification.   
    For *Branch delivery* is this attribute required.
+ **code** ([SupplierProductCode][ds-supplier-product-code], optional)
    Supplier product code.   
    Required for cases when you can't supply `orderItemId`.
+ **packageNumber** ([String100][ds-string-100], required) - Related package number.
+ **quantity** ([Number][ds-number], required) - Quantity. 
+ **serials** (array[[String50][ds-string-50]], optional) - Serial numbers. Required if `serialNumbersRequired` is `true` in *Order Inser* API message.

### OrderItem (object) {#data-structures--order-item}
+ **orderItemId** ([Id64][ds-id-64], required) - Unique `Order Item ID`. This value is used for items identification
+ **code** ([SupplierProductCode][ds-supplier-product-code], required) - Supplier product code
+ **quantity** ([Number][ds-number], required) - Required quantity
+ **unitPrice** ([Money][ds-money], optional)
    **Deprecated - Replaced by `purchasePriceWithoutFees`**  
    Unit purchase price for buyer (excl. VAT, excl. recycling/copyright fee).  
    This is price from `productList[].price` or `productList[].countryPrices[].purchasePriceWithoutFees` 
    of Availability API message. If the purchase price was not provided from Supplier, it was calculated from the 
    `productList[].countryPrices[].sellingPriceWithoutVat` according to the commission of the product category.
+ **purchasePriceWithoutFees** ([Money][ds-money], required)
    Unit purchase price for buyer (excl. VAT, excl. recycling/copyright fee).  
    This is price from `productList[].price` or `productList[].countryPrices[].purchasePriceWithoutFees` 
    of Availability API message. If the purchase price was not provided from Supplier, it was calculated from the 
    `productList[].countryPrices[].sellingPriceWithoutVat` according to the commission of the product category.
+ **fees** ([CountryPriceFees][ds-country-price-fees], optional)  
    Recycling and copyright unit fees. Filled only for **Latest price mode**.
+ **alzaBarCodes** (array[[String30][ds-string-30]], optional)
    Custom piece identification for **delivery to branch**.  
    Print these *barcodes* (`Code-128BC`) on each piece to identify each individual piece. 
    The barcode count will be equal to the quantity.
    
    Example: `BCX4809077792`
+ **serialNumbersExpected** (boolean, optional)
    If `true` and `serialNumbersRequired` is `false` then serial numbers should be sent in `items[].serials` 
    in *Shipment departure* API message. 
    The case does not strictly require serial numbers, but the lack of serial numbers should be addressed in the future.
    
    Default value is `false`.  
+ **serialNumbersRequired** (boolean, optional)
    If `true` then ignore `serialNumbersExpected` and serial numbers will be required in `items[].serials` 
    in *Shipment departure* API message.
    
    Default value is `false`.   

### GeneralResponse (object) {#data-structures--general-response}
+ **errorCode** ([ErrorCode][ds-error-code], required) - Error Code
+ **errorMessage** ([String500][ds-string-500], optional)
    Required for `errorCode` < 0.  
    Error message for `errorCode` < 0.  
    Warning message for `errorCode` = 0.  

### Route (object) {#data-structures--route}
+ **routeName** ([String100][ds-string-100], optional) - Route name
+ **routeStops** (array[[RouteStop][ds-route-stop]], optional) - Route stops
+ **routeDeliveryOrder** ([Int16][ds-int-16], optional) - Print following number to package sticker for easier delivery.
  For Supplier shipping mode only.

### RouteStop (object) {#data-structures--route-stop}
+ **branchName** ([String30][ds-string-30], optional) - Branch name
+ **ramp** ([String10][ds-string-10], optional) - (un)loading ramp

### PackageSorting (object) {#data-structures--package-sorting}
+ **packageSortingGroup** ([PackageSortingGroup][ds-package-sorting-group], required) - Package sorting group. 
  Packages from different groups should not be physically mixed during shipping.
+ **packageSortingPrint** ([String10][ds-string-10], optional) - Print following text to package sticker for better identification. 
  For Supplier shipping mode only.


### AvailabilityRequest (object) {#data-structures--availability-request}
+ **supplierId** ([Id][ds-id], required) - Supplier Id (provided by the Buyer). Used for authentication token calculation. 
+ **supplierBranchId** ([Id][ds-id], required) - Supplier Branch Id (provided by the Buyer). 
    Suppliers can have multiple Branches with different stock availability. This identification is passed to **Insert order**
+ **timestamp** ([Timestamp][ds-timestamp], required) - Time of action in CET
+ **importType** ([ImportType][ds-import-type], required) - Import type
+ **currency** ([Currency][ds-currency], required) - National currency of the country of the branch.
+ **productList** (array[[Product][ds-product]], required) - Product list

### ShipmentCreateRequest (object) {#data-structures--shipment-create-request}
+ **supplierId** ([Id][ds-id], required) - Supplier ID (provided by the Buyer). Used for authentication token calculation. 
+ **supplierBranchId** ([Id][ds-id], required) - Supplier Branch ID (provided by the Buyer). 
+ **timestamp** ([Timestamp][ds-timestamp], required) - Time of action in CET
+ **shippingCarrier** ([ShippingCarrierStrict][ds-shipping-carrier-strict], required) - Shipping carrier identification.
+ **parcelShop**([ParcelShop][ds-parcel-shop], optional) - Parcel shop detail. Required if `parcelShop` object is contained in Confirm order
+ **cashOnDeliveryValue** ([Money][ds-money], required) - Cash on delivery
+ **cashOnDeliveryValueCurrency** ([Currency][ds-currency], required) - Cash on delivery Currency code
+ **shipmentValue** ([Money][ds-money], optional) - Total shipment value. 
  The attribute is required if `shipmentValue` attribute is sent via `Confirm order`.
+ **shipmentValueCurrency** ([Currency][ds-currency], optional) - Total shipment value Currency code. 
  The attribute is required if `shipmentValue` attribute is filled.
+ **shipmentWeight** ([Weight][ds-weight], required) - Total weight in kg
+ **shipmentVolume** ([Volume][ds-volume], optional) - Total volume in cm3  
+ **packages** (array[[ShipmentCreatePackage][ds-shipment-create-package]], required) - Array of *Packages*
+ **items** (array[[ShipmentCreateItem][ds-shipment-create-item]], required) - Array of *Items*

### ShipmentCreateResponse (object) {#data-structures--shipment-create-response}
+ **errorCode** ([ErrorCode][ds-error-code], required) - Error Code
+ **errorMessage** ([String500][ds-string-500], optional)
    Required for `errorCode` < 0.  
    Error message for `errorCode` < 0.  
    Warning message for `errorCode` = 0.
+ **shipment** ([CreatedShipment][ds-created-shipment], optional)
    Required if `errorCode` = 0.
    Created shipment.

### ShipmentDeleteRequest (object) {#data-structures--shipment-delete-request}
+ **supplierId** ([Id][ds-id], required) - Supplier ID (provided by the Buyer). Used for authentication token calculation. 
+ **supplierBranchId** ([Id][ds-id], required) - Supplier Branch ID (provided by the Buyer). 
+ **timestamp** ([Timestamp][ds-timestamp], required) - Time of action in CET

### ShipmentDepartureRequest (object) {#data-structures--shipment-departure-request}
+ **supplierId** ([Id][ds-id], required) - Supplier ID (provided by the Buyer). Used for authentication token calculation. 
+ **supplierBranchId** ([Id][ds-id], optional) - Supplier Branch ID (provided by the Buyer). Required for multi-branch supplier. 
+ **timestamp** ([Timestamp][ds-timestamp], required) - Time of action in CET
+ **shippingCarrier** ([ShippingCarrier][ds-shipping-carrier], required) - Used Shipping carrier. Required for new Suppliers.
+ **parcelShop**([ParcelShop][ds-parcel-shop], optional) - Parcel shop detail. Required if `parcelShop` object is contained in Confirm order
+ **expectedDeliveryDate** ([Date][ds-date], optional) - Estimated delivery date
+ **cashOnDeliveryValue** ([Money][ds-money], required) - Cash on delivery
+ **cashOnDeliveryValueCurrency** ([Currency][ds-currency], required) - Cash on delivery Currency code
+ **shipmentValue** ([Money][ds-money], optional) - Total shipment value. 
  The attribute is required if `shipmentValue` attribute is sent via `Confirm order`.
+ **shipmentValueCurrency** ([Currency][ds-currency], optional) - Total shipment value Currency code. 
  The attribute is required if `shipmentValue` attribute is filled.
+ **shipmentWeight** ([Weight][ds-weight], required) - Total weight in kg
+ **shipmentVolume** ([Volume][ds-volume], optional) - Total volume in cm3
+ **deliveryAddress** ([DeliveryAddress][ds-delivery-address], optional) - Delivery address where the shipment will be delivered
+ **packages** (array[[ShipmentDeparturePackage][ds-shipment-departure-package]], required) - Array of *Packages*.  
+ **items** (array[[ShipmentDepartureItem][ds-shipment-departure-item]], required) - Array of *Items*.

### ShipmentDepartureResponse (object) {#data-structures--shipment-departure-response}
+ **errorCode** ([ErrorCode][ds-error-code], required)
    Error Code
+ **errorMessage** ([String500][ds-string-500], optional)
    Required for `errorCode` < 0.  
    Error message for `errorCode` < 0.  
    Warning message for `errorCode` = 0.
+ **shipment** ([DeparturedShipment][ds-departured-shipment], optional)
    Required for `errorCode` = 0 and **Buyer shipping mode**.  
    Departured shipment

### TrackAndTraceRequest (object) {#data-structures--track-and-trace-request}
+ **supplierId** ([Id][ds-id], required) - Supplier Id (provided by the Buyer). Used for authentication token calculation. 
+ **order** ([OrderNumber][ds-order-number], optional) - Order number (our indentification). Conditionally required.
+ **shipment** ([String50][ds-string-50], optional) - Shipment number (your identifaction used in *Shipment departure*). Conditionally required.
+ **package** ([String100][ds-string-100], optional) - Package number. Conditionally required.
+ **fullPackageNumber** ([String100][ds-string-100], optional) - Full package number. Conditionally required.
+ **timestamp** ([Timestamp][ds-timestamp], required) - Time of action in CET
+ **status** ([TrackAndTraceStatus][ds-track-and-trace-status], required) - Delivery state
+ **statusTimestamp** ([Timestamp][ds-timestamp], required) - Status time in CET

### DeliveryResultRequest (object) {#data-structures--delivery-result-request}
+ **supplierId** ([Id][ds-id], required) - Supplier Id (provided by the Buyer). Used for authentication token calculation. 
+ **timestamp** ([Timestamp][ds-timestamp], required) - Time of action in CET
+ **status** ([DeliveryResultStatus][ds-delivery-result-status], required) - Delivery information
+ **statusTimestamp** ([Timestamp][ds-timestamp], required) - Status time in CET
+ **errorReason** ([String500][ds-string-500], optional) - Reason for Canceled or Rejected
+ **paymentVS** ([String30][ds-string-30], optional) - Actual Payment Variable Symbol
+ **errorProducts** (array[[ErrorProduct][ds-error-product]], optional) - Optional array of invalid products for Canceled status

### OrderInsertRequest (object) {#data-structures--order-insert-request}
+ **timestamp** ([Timestamp][ds-timestamp], required) - Time of action in CET
+ **customerId** ([CustomerId][ds-customer-id], required) - Buyer ID (provided by the Supplier). Used for authentication token calculation.
+ **supplierId** ([Id][ds-id], required) - Supplier ID (provided by the Buyer). 
+ **regNo** ([String30][ds-string-30], optional) - Buyer Registration Identification Number.
+ **vatNo** ([String30][ds-string-30], optional) - Buyer VAT Identification Number.
+ **supplierBranchId** ([Id][ds-id], required) - Supplier Branch ID (same value as in Availability method). 
+ **itemsPriceCurrency** ([Currency][ds-currency], required) - Item Currency code (from Availability import)
+ **itemsPriceCountry** ([Country][ds-country], optional) - Target country of prices (from Availability import)
+ **orderItems** (array[[OrderItem][ds-order-item]], required)

### OrderInsertResponse (object) {#data-structures--order-insert-response}
+ **errorCode** ([ErrorCode][ds-error-code], required) - Error Code
+ **errorMessage** ([String500][ds-string-500], optional)
    Required for `errorCode` < 0.  
    Error message for `errorCode` < 0.  
    Warning message for `errorCode` = 0.
+ **supplierOrder** ([String30][ds-string-30], optional) - Ignored for `errorCode` < 0. Internal supplier order number.
+ **validUntil** ([Timestamp][ds-timestamp], optional)
    Ignored for `errorCode` < 0.  
    Validity period of a reservation in CET. Default value is `Today` + 30 days. 
    Required value is at least `Today` + 1 day. Optimal value is `Today` + days of minimum guaranteed reservation from contract.
+ **errorProducts** (array[[ErrorProduct][ds-error-product]], optional)
    Ignored for `errorCode` = 0.  
    Array of invalid products for unsuccessful reservation.

### OrderCancelRequest (object) {#data-structures--order-cancel-request}
+ **timestamp** ([Timestamp][ds-timestamp], required) - Time of action in CET
+ **customerId** ([CustomerId][ds-customer-id], required) - Buyer ID (provided by the Supplier). Used for authentication token calculation. 
+ **supplierId** ([Id][ds-id], required) - Supplier ID (provided by the Buyer).
+ **supplierBranchId** ([Id][ds-id], required) - Supplier Branch ID (same value as in Availability method).
+ **regNo** ([String30][ds-string-30], optional) - Buyer Registration Identification Number.
+ **vatNo** ([String30][ds-string-30], optional) - Buyer VAT Identification Number.

### OrderExtendRequest (object) {#data-structures--order-extend-request}
+ **timestamp** ([Timestamp][ds-timestamp], required) - Time of action in CET
+ **customerId** ([CustomerId][ds-customer-id], required) - Buyer ID (provided by the Supplier). Used for authentication token calculation. 
+ **supplierId** ([Id][ds-id], required) - Supplier ID (provided by the Buyer).
+ **supplierBranchId** ([Id][ds-id], required) - Supplier Branch ID (same value as in Availability method).
+ **regNo** ([String30][ds-string-30], optional) - Buyer Registration Identification Number.
+ **vatNo** ([String30][ds-string-30], optional) - Buyer VAT Identification Number.
+ **validUntil** ([Timestamp][ds-timestamp], optional) - Recommanded validUntil in CET

### OrderExtendResponse (object) {#data-structures--order-extend-response}
+ **errorCode** ([ErrorCode][ds-error-code], required) - Error Code
+ **errorMessage** ([String500][ds-string-500], optional)
    Required for `errorCode` < 0.  
    Error message for `errorCode` < 0.  
    Warning message for `errorCode` = 0.
+ **validUntil** ([Timestamp][ds-timestamp], optional)
    Required for `errorCode` = 0.  
    Validity period of a reservation in CET. Required value is at least `Now` + 12 hours.

### OrderConfirmRequest (object) {#data-structures--order-confirm-request}
+ **timestamp** ([Timestamp][ds-timestamp], required) - Time of action in CET
+ **customerId** ([CustomerId][ds-customer-id], required) - Buyer ID (provided by the Supplier). Used for authentication token calculation.
+ **supplierId** ([Id][ds-id], required) - Supplier ID (provided by the Buyer).
+ **supplierBranchId** ([Id][ds-id], required) - Supplier Branch ID (same value as in Availability method).
+ **regNo** ([String30][ds-string-30], optional) - Buyer Registration Identification Number.
+ **vatNo** ([String30][ds-string-30], optional) - Buyer VAT Identification Number.
+ **taxNo** ([String30][ds-string-30], optional) - Byuer Tax Identification Number. **Upcoming feature**
+ **shippingCarrier** ([ShippingCarrierConfirm][ds-shipping-carrier-confirm], required) - Shipping carrier.
+ **parcelShop**([ParcelShop][ds-parcel-shop, optional) - Parcel shop detail. Required with `ParcelShop` value 
    of `shipmentDeliveryType` attribute
+ **route** ([Route][ds-route], optional) - Route information for custom shipping sticker
+ **shipmentDeliveryType** ([ShipmentDeliveryType][ds-shipment-delivery-type], required) - Delivery type. Information is passed to 
    shipment carrier
+ **shipmentShippingMode** ([ShipmentShippingMode][ds-shipment-shipping-mode], required) - Defines who handles *shipment number*, 
    *package numbers*, *shipping list*, *shipping sticker* and *carrier data*
+ **shipmentDeliveryServices** ([ShipmentDeliveryServices][ds-shipment-delivery-services], optional) - Delivery services of shipment by carrier.  **Upcoming feature**
+ **shipmentValue** ([Money][ds-money], optional) - Total shipment value
+ **shipmentValueCurrency** ([Currency][ds-currency], optional) - Total shipment value Currency code
+ **packageSorting** ([PackageSorting][ds-package-sorting], optional) - Package sorting
+ **demandedExpeditionDate** ([Date][ds-date], optional) 
    **Deprecated - Replaced by `shipmentDepartureTime`**. It is necessary remove time part.

    Requested date of dispatch.
+ **shipmentDepartureTime** ([Timestamp][ds-timestamp], required) - Requested shipment departure time in CET.
+ **cashOnDeliveryValue** ([Money][ds-money], required) - Cash on delivery to collect
+ **cashOnDeliveryValueCurrency** ([Currency][ds-currency], required) - Cash on delivery Currency code
+ **paymentVS** ([String30][ds-string-30], required) - Cash on delivery payment Variable Symbol
+ **deliveryBranchId** ([Id][ds-id], optional) - Contains Buyer branch ID if *Branch* delivery type is filled.
+ **shipmentExternalOrderNumber** ([String50][ds-string-50], optional)
    External order number assigned to the shipment, used to identify the order in external systems. Required for label printing.
+ **deliveryAddress** ([DeliveryAddress][ds-delivery-address], required) - The delivery address where the shipment will be finally delivered
+ **glnList** ([GLNList][ds-gln-list], optional) - **Upcoming feature**
+ **buyerAddress** ([CompanyAddress][ds-company-address], optional) - Buyer company address for invoicing. **Upcoming feature**
+ **shipmentDeliveryAddress** ([ShipmentAddress][ds-shipment-address], optional) - The address where the supplier delivers the shipment. May be different from `deliveryAddress`. **Upcoming feature**
 
### InvokerSimpleRequest (object) {#data-structures--invoker-simple-request}
+ **timestamp** ([Timestamp][ds-timestamp], required) - Time of action in CET
+ **supplierId** ([Id][ds-id], required) - Supplier identification (provided by the Buyer). Used for authentication token calculation.

### InvokerOrderInsertRequest {#data-structures--invoker-order-insert-request}
+ **timestamp** ([Timestamp][ds-timestamp], required) - Time of action in CET
+ **customerId** ([CustomerId][ds-customer-id], required) - Buyer ID used for communication with Supplier API. Default is 1.
+ **supplierId** ([Id][ds-id], required) - Supplier ID (provided by the Buyer). Used for authentication token calculation.
+ **supplierBranchId** ([Id][ds-id], required) - Supplier Branch Id (same value as in Availability method). 
+ **codes** (array[[SupplierProductCode][ds-supplier-product-code]], required) - Supplier product codes

### InvokerOrderInsertResponse {#data-structures--invoker-order-insert-response}
+ **errorCode** ([ErrorCode][ds-error-code], required)
    Error Code
+ **errorMessage** ([String500][ds-string-500], optional)
    Required for `errorCode` < 0.  
    Error message for `errorCode` < 0.  
    Warning message for `errorCode` = 0.
+ **responseHTTPStatusCode** ([Int32][ds-int-32], optional)
    HTTP statu code from Supplier API
+ **responseObject** ([OrderInsertResponse][ds-order-insert-response], optional)
    Filled with Supplier API response when it's valid

### InvokerOrderCancelResponse {#data-structures--invoker-order-cancel-response}
+ **errorCode** ([ErrorCode][ds-error-code], required) - Error Code
+ **errorMessage** ([String500][ds-string-500], optional) - Error message. Required for `errorCode` < 0.
+ **responseHTTPStatusCode** ([Int32][ds-int-32], optional) - HTTP statu code from Supplier API
+ **responseObject** ([GeneralResponse][ds-general-response], optional) - Filled with Supplier API response when it's valid

### InvokerOrderExtendResponse {#data-structures--invoker-order-extend-response}
+ **errorCode** ([ErrorCode][ds-error-code], required)
    Error Code
+ **errorMessage** ([String500][ds-string-500], optional)
    Required for `errorCode` < 0.  
    Error message for `errorCode` < 0.  
    Warning message for `errorCode` = 0.
+ **responseHTTPStatusCode** ([Int32][ds-int-32], optional)
    HTTP statu code from Supplier API
+ **responseObject** ([OrderExtendResponse][ds-order-extend-response], optional)
    Filled with Supplier API response when it's valid

### InvokerOrderConfirmResponse {#data-structures--invoker-order-confirm-response}
+ **errorCode** ([ErrorCode][ds-error-code], required) - Error Code
+ **errorMessage** ([String500][ds-string-500], optional) - Error message. Required for `errorCode` < 0.
+ **responseHTTPStatusCode** ([Int32][ds-int-32], optional) - HTTP statu code from Supplier API
+ **responseObject** ([GeneralResponse][ds-general-response], optional) - Filled with Supplier API response when it's valid


[data-structures]:                      #data-structures
[ds-timestamp]:                         #data-structures--timestamp
[ds-timestamputc]:                      #data-structures--timestamputc
[ds-date]:                              #data-structures--date
[ds-int-16]:                            #data-structures--int-16
[ds-int-32]:                            #data-structures--int-32
[ds-int-64]:                            #data-structures--int-64
[ds-float]:                             #data-structures--float
[ds-string-10]:                         #data-structures--string-10
[ds-string-20]:                         #data-structures--string-20
[ds-string-30]:                         #data-structures--string-30
[ds-string-50]:                         #data-structures--string-50
[ds-string-100]:                        #data-structures--string-100
[ds-string-500]:                        #data-structures--string-500
[ds-customer-id]:                       #data-structures--customer-id
[ds-supplier-product-code]:             #data-structures--supplier-product-code
[ds-weight]:                            #data-structures--weight
[ds-volume]:                            #data-structures--volume
[ds-money]:                             #data-structures--money
[ds-vat]:                               #data-structures--vat
[ds-hmac-token]:                        #data-structures--hmac-token
[ds-country]:                           #data-structures--country
[ds-currency]:                          #data-structures--currency
[ds-guid]:                              #data-structures--guid
[ds-gln-list]:                          #data-structures--gln-list
[ds-gln]:                               #data-structures--gln
[ds-number]:                            #data-structures--number
[ds-order-number]:                      #data-structures--order-number
[ds-id]:                                #data-structures--id
[ds-id-64]:                             #data-structures--id-64

[ds-error-code]:                        #data-structures--error-code
[ds-success-error-code]:                #data-structures--success-error-code
[ds-fail-error-code]:                   #data-structures--fail-error-code
[ds-import-type]:                       #data-structures--import-type
[ds-track-and-trace-status]:            #data-structures--track-and-trace-status
[ds-delivery-result-status]:            #data-structures--delivery-result-status
[ds-shipment-delivery-type]:            #data-structures--shipment-delivery-type
[ds-shipment-shipping-mode]:            #data-structures--shipment-shipping-mode
[ds-shipment-delivery-services]:        #data-structures--shipment-delivery-services
[ds-shipping-carrier-code]:             #data-structures--shipping-carrier-code
[ds-shipping-carrier-delivery-type]:    #data-structures--shipping-carrier-delivery-type
[ds-parcel-shop-identification]:        #data-structures--parcel-shop-identification
[ds-route]:                             #data-structures--route
[ds-route-stop]:                        #data-structures--route-stop
[ds-delivery-address]:                  #data-structures--delivery-address
[ds-company-address]:                   #data-structures--company-address
[ds-shipment-address]:                  #data-structures--shipment-address
[ds-package-sorting-group]:             #data-structures--package-sorting-group

[ds-shipping-list]:                     #data-structures--shipping-list
[ds-shipping-list-group]:               #data-structures--shipping-list-group
[ds-departured-shipment]:               #data-structures--departured-shipment
[ds-product]:                           #data-structures--product
[ds-error-product]:                     #data-structures--error-product
[ds-parcel-shop]:                       #data-structures--parcel-shop
[ds-shipping-carrier-confirm]:          #data-structures--shipping-carrier-confirm
[ds-shipping-carrier]:                  #data-structures--shipping-carrier
[ds-shipping-carrier-strict]:           #data-structures--shipping-carrier-strict
[ds-country-price]:                     #data-structures--country-price
[ds-country-price-fees]:                #data-structures--country-price-fees
[ds-created-shipment]:                  #data-structures--created-shipment
[ds-created-package]:                   #data-structures--created-package
[ds-shipment-create-item]:              #data-structures--shipment-create-item
[ds-shipment-create-package]:           #data-structures--shipment-create-package
[ds-shipment-departure-package]:        #data-structures--shipment-departure-package
[ds-shipment-departure-item]:           #data-structures--shipment-departure-item
[ds-order-item]:                        #data-structures--order-item
[ds-package-sorting]:                   #data-structures--package-sorting

[ds-availability-request]:              #data-structures--availability-request
[ds-order-insert-request]:              #data-structures--order-insert-request
[ds-order-insert-response]:             #data-structures--order-insert-response
[ds-order-extend-request]:              #data-structures--order-extend-request
[ds-order-extend-response]:             #data-structures--order-extend-response
[ds-order-cancel-request]:              #data-structures--order-cancel-request
[ds-order-confirm-request]:             #data-structures--order-confirm-request
[ds-shipment-create-request]:           #data-structures--shipment-create-request
[ds-shipment-create-response]:          #data-structures--shipment-create-response
[ds-shipment-delete-request]:           #data-structures--shipment-delete-request
[ds-shipment-departure-request]:        #data-structures--shipment-departure-request
[ds-shipment-departure-response]:       #data-structures--shipment-departure-response
[ds-track-and-trace-request]:           #data-structures--track-and-trace-request
[ds-delivery-result-request]:           #data-structures--delivery-result-request
[ds-general-response]:                  #data-structures--general-response

[ds-invoker-simple-request]:            #data-structures--invoker-simple-request
[ds-invoker-order-insert-request]:      #data-structures--invoker-order-insert-request
[ds-invoker-order-insert-response]:     #data-structures--invoker-order-insert-response
[ds-invoker-order-extend-response]:     #data-structures--invoker-order-extend-response
[ds-invoker-order-confirm-response]:    #data-structures--invoker-order-confirm-response
[ds-invoker-order-cancel-response]:     #data-structures--invoker-order-cancel-response

[hmac]:                                 https://en.wikipedia.org/wiki/Hash-based_message_authentication_code
[base64]:                               https://msdn.microsoft.com/library/system.convert.tobase64string.aspx
[percent-encoding]:                     https://en.wikipedia.org/wiki/Percent-encoding

[wiki-country-code]:                    https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2
[wiki-currency-code]:                   https://en.wikipedia.org/wiki/ISO_4217
[iso-country-code]:                     https://www.iso.org/iso-3166-country-codes.html
[iso-currency-code]:                    https://www.iso.org/iso-4217-currency-codes.html
