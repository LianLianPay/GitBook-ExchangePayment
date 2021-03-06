## Pre-authorized order status query API

###### Endpoint

```html
https://queryapi.lianlianpay.com/preauthquery.htm
```


###### Request Parameters

|Name|Required|Type|Description|
|:---|:---|:---|:---|
|oid_partner|Required|String(18)|The unique identification assigned to the merchant. E.g. 201304121000001004|
|platform|Optional|String(32)| ```platform``` is used for sharing user info between multiple ```oid_partner```, this requires additional settings from LianLian side|
|sign|Required|String|Signature value|
|sign_type|Required|String(3)|RSA |
|pay_type|Required|String|F, authorization|
|api_version|Required|String|Fixed value, ```1.0```|
|no_order|Required|String(32)|Merchant order No.|
|dt_order|Required|String(14)|Merchant order date. Format: YYYYMMDDHHMMSS, E.g. 20170801225714|
|oid_paybill|Required|String(18)|Unique transaction No. in LianLian system. E.g. 2011030900001098|

###### Sample Request

```curl
curl https://traderapi.lianlianpay.com/preauthquery.htm\
-H "Content-type:application/json;charset=utf-8" \
-d '{   
        "oid_partner":"201103171000000000",
		"pay_type":"F",
		"api_verion":"1.0",
		"dt_order":"2013051500001",
    	"no_order":"2013051500001",
    	"sign_type":"RSA",
    	"sign":"ZPZULntRpJwFmGNIVKwjLEF2Tze7bqs60rxQ22CqT5J1UlvGo575QK9z/+p+7E9cOoRoWzqR6xHZ6WVv3dloyGKDR0btvrdqPgUAoeaX/YOWzTh00vwcQ+HBtXE+vPTfAqjCTxiiSJEOY7ATCF1q7iP3sfQxhS0nDUug1LP3OLk="
    }'
```

***
## Response

###### Parameters

|Name|Required|Type|Description|
|:---|:---|:---|:---|
|ret_code|Required|String(4)|2003 Payment created<br>2006 The transaction has expired.<br>PR07 Pre-authorized application is successful.<br>PR08 Pre-authorized application to be verified. <br>PR09 Pre-authorized application processing. <br>PR10 Pre-authorized application failed.<br>PR11 Capture successfully <br>PR12 Processing capture<br>PR13 Capture failed<br>PR14 Pre authorization revoked successfully <br>PR15 Pre authorization revocation processing <br>PR16 Pre authorization revocation failed <br>|
|ret_msg|Required|String(100)|Return message, description of ```ret_code```, in Chinese |
|oid_partner|Required|String(18)|The unique identification assigned to the merchant. E.g. 201304121000001004|
|sign_type|Required|String(3)|RSA |
|sign|Required|String|Signature value|
|no_order|Optional|String(32)|Merchant order No.|
|dt_order|Optional|String(14)|Merchant order date. Format: YYYYMMDDHHMMSS, E.g. 20170801225714|
|oid_paybill|Optional|String(18)|Unique transaction No. in LianLian system. E.g. 2011030900001098|
|money_order|Optional|String(12)|Merchant order amount, range: 0.01 ~ 100,000,000.00, 2 decimal places are expected, in CNY|

###### Sample Response

```json
{
	"ret_code":"0000",
	"ret_msg":交易成功",
	"oid_partner":"201103171000000000",
	"oid_paybill":"2013051416009982",
	"no_order":"2013051500001",
	"dt_order":"20141231010101",
	"money_order":"210.97",
	"user_id":"20130515094013",
	"sign_type":"RSA",
	"sign":"ZPZULntRpJwFmGNIVKwjLEF2Tze7bqs60rxQ22CqT5J1UlvGo575QK9z/+p+7E9cOoRoWzqR6xHZ6WVv3dloyGKDR0btvrdqPgUAoeaX/YOWzTh00vwcQ+HBtXE+vPTfAqjCTxiiSJEOY7ATCF1q7iP3sfQxhS0nDUug1LP3OLk="
	}
```