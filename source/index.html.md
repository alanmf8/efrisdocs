---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:

search: true

code_clipboard: true
---

# Introduction

The system interface uses JSON format to transfer data. The payload is divided into three parts: `{ data, globalInfo, returnStateInfo }`.

```json
{
  "data": {},
  "globalInfo": {},
  "returnStateInfo": {}
}
```

Request/Response protocol attributes |
------------------ |
__data__ `{...}` |
<div>__content__?</div> |
<div>__signature__</div> |
<div>__dataDescription__ `{...}`</div> |
<div><div>__codeType__</div></div> |
<div><div>__encryptCode__</div></div> |
<div><div>__zipCode__</div></div> |
__globalInfo__ `{...}` |
<div>__appId__</div> |
<div>__version__</div> |
<div>__dataExchangeId__</div> |
<div>__interfaceCode__</div> |
<div>__requestCode__</div> |
<div>__requestTime__</div> |
<div>__responseCode__</div> |
<div>__userName__</div> |
<div>__deviceMAC__</div> |
<div>__deviceNo__</div> |
<div>__tin__</div> |
<div>__brn__?</div> |
<div>__taxpayerID__</div> |
<div>__longitude__</div> |
<div>__latitude__</div> |
<div>__extendField__? `{...}`</div> |
<div><div>__responseDateFormat__</div></div> |
<div><div>__responseTimeFormat__</div></div> |
<div><div>__referenceNo__</div></div> |
__returnStateInfo__ `{...}` |
<div>__returnCode__</div> |
<div>__returnMessage__?</div> |

# Goods & Services

## `T102` Upload goods/services

Attributes |
---------- |
**operationType**?<br>`"101"` add goods (default), `"102"` modify product |
**goodsName**<br> |
**goodsCode** |
**measureUnit** |
**unitPrice** |
**currency** |
**commodityCategory** |
**haveExciseTax** |
**exciseDutyCode**? |
**description**? |
**stockPrewarning** |
**havePieceUnit** |
**pieceMeasureUnit**? |
**pieceUnitPrice**? |
**packageScaledValue**? |
**pieceScaledValue**? |
**haveOtherUnit**?<br/>if `havePieceUnit: 102` `haveOtherUnit` must be `102` |
**returnCode**?<br/>response only |
**returnMessage**?<br/>response only |



## Get all goods/services

```shell
curl "http://example.com/api/kittens" \
  -H "Authorization: meowmeowmeow"
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

This endpoint retrieves all kittens.

### Request attributes

Parameter | Default | Description
--------- | ------- | -----------
include_cats false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

# Invoices & Notes

## Upload invoice

Attributes |
---------- |
**sellerDetails** `{...}` |
&emsp;**tin**<br/>&emsp;sellers TIN, must be the same with `globalInfo.tin` |
&emsp;**ninBrn**?<br/>&emsp;sellers NIN if individual or BRN if business |
&emsp;**legalName** |
&emsp;**emailAddress** |
&emsp;**businessName**? |
&emsp;**address**?<br/>&emsp;seller address |
&emsp;**mobilePhone**? |
&emsp;**linePhone**? |
&emsp;**placeOfBusiness**? |
&emsp;**referenceNo**<br/>&emsp;seller's transaction reference. if `invoiceIndustryCode = 104` this can't be empty |
&emsp;**isCheckReferenceNo**?<br/>&emsp;`0` No (default) or `1` Yes |
&emsp;**branchId**? |
&emsp;**branchName**<br/>&emsp;return `sellerDetails.branchName` for response |
&emsp;**branchCode**?<br/>&emsp;return `sellerDetails.branchCode` for response |
**basicInformation** `{...}` |
&emsp;**invoiceNo**?<br/>&emsp;FDN from URA, should be blank in request |
&emsp;**antifakeCode**?<br/>&emsp;verification code, should be blank in request |
&emsp;**deviceNo** |
&emsp;**issueDate**<br/>&emsp;yyyy-MM-dd HH24:mm:ss |
&emsp;**operator**<br/>&emsp;the person sercing the customer |
&emsp;**currency** |
&emsp;**oriInvoiceId**?<br/>&emsp;for debit notes the `invoiceId` returned when raising original invoice/receipt |
&emsp;**invoiceType**<br/>&emsp;`"1"` Invoice/Receipt, `"5"` Credit memo/rebate, `"4"` Debit note |
&emsp;**invoiceKind**<br/>&emsp;`"1"` invoice, `"2"` receipt |
&emsp;**dataSource**<br/>&emsp;`"101"` EFD, `"103"` WebService API, `"106"` offline mode |
&emsp;**invoiceIndustryCode**?<br/>&emsp;`"101"` General industry .etc |
&emsp;**isBatch**?<br/>&emsp;`"0"` not a batch summary invoice (default), `"1"` batch summary invoice |
&emsp;**currencyRate**? |
**buyerDetails** `{...}` |
&emsp;__buyerTin__?<br/>&emsp;TIN of the buyer, mandatory if `buyerType` is B2B or B2G |
&emsp;__buyerNinBrn__? |
&emsp;__buyerPassportNum__? |
&emsp;__buyerLegalName__? |
&emsp;__buyerBusinessName__? |
&emsp;__buyerAddress__? |
&emsp;__buyerEmail__? |
&emsp;__buyerMobilePhone__? |
&emsp;__buyerLinePhone__? |
&emsp;__buyerPlaceOfBusi__? |
&emsp;__buyerType__<br/>&emsp;`"0"` B2B or B2G, `"1"` B2C, `"2"` B2Foreigner |
&emsp;__buyerCitzenship__? |
&emsp;__buyerSector__? |
&emsp;__buyerReferenceNo__?<br/>&emsp;buyer reference or identifier |
**buyerExtend** `{...}` |
**goodsDetail** `[{...}]` |
<div>__item__<br/>if `discountFlag: "0"` the name of the discount line is `{name of line} (discount)`</div> |
<div>__itemCode__</div> |
<div>__qty__?</div> |
<div>__unitOfMeasure__?</div> |
<div>__unitPrice__?</div> |
<div>__total__<br/>must be +ve when `discountFlag = "1" or "2"` and -ve when `discountFlag = "0"`</div> |
<div>__taxRate__<br>instead of 18% put 0.18, must be +ve</div> |
<div>__tax__<br>must be +ve when `discountFlag = "1" or "2"` and -ve when `discountFlag = "0"`</div> |
<div>__discountFlag__<br>`"0"` discount on amount, `"1"` discount on entire item, `"2"` non-discount item</div> |
<div>__discountTotal__?</div> |
<div>__discountTaxRate__?</div> |
<div>__deemedFlag__<br>`"1"` deemed, `"2"` not deemed</div> |
<div>__orderNumber__<br>`+1` each time starting at `"0"`</div> |
<div>__categoryId__?</div> |
<div>__categoryName__?</div> |
<div>__goodsCategoryId__<br>VAT commodity classification</div> |
<div>__goodsCategoryName__?</div> |
<div>__exciseFlag__<br>`"1"` excise, `"2"` not excise</div> |
<div>__exciseRate__?</div> |
<div>__exciseTax__?</div> |
<div>__pack__?</div> |
<div>__stick__?</div> |
<div>__exciseUnit__?</div> |
<div>__exciseCurrency__?</div> |
<div>__exciseRateName__?</div> |

