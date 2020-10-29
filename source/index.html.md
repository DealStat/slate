---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - python
  - shell

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>


search: true
---

# Introduction

DealStat API for Real Estate data extraction


# PDFs

## Send document (POST)


```python
import requests

FILE_LOC = '/your/path/<YOUR_FILE_LOC>.pdf'
file_content = open(FILE_LOC, 'rb')

files = {'file': file_content}
headers = {'Authorization': 'Bearer YOUR-API-KEY'}

result = requests.post('http://DEALSTAT-API-URL.com/<file_type>', files=files, headers=headers)

print(result)

```

```shell
curl -i -X 'POST' 'http://DEALSTAT-API-URL.com/<file_type>'
  -H "Authorization: Bearer Your-API-KEY"
  -F file=@"/your/path/<YOUR_FILE_LOC>.pdf"
```

> The above command returns JSON structured like this:

```json
{
  "success": true,
  "file_id": "krzmuujooydnmjnpjgepzhifn",
}

```

This endpoint sends document to DealStat for processing

### HTTP Request

<aside class="notice"> Make sure to replace DEALSTAT-API-URL with provided URL </aside>

`POST http://DEALSTAT-API-URL.com/<file_type>`


### URL Parameters

Parameter | Description
--------- | -----------
file_type | title_deed for property deed, om for offering memorandum


### HEADER Parameters

Parameter | Description
--------- | -----------
Authorization | Bearer YOUR-API-KEY

<aside class="notice"> Make sure to replace YOUR-API-KEY with provided API KEY </aside>



### FILE Parameters

Parameter | Description
--------- | -----------
file | File content of PDF

## Retrieve information (GET)

```python
import requests

headers = {'Authorization': 'Bearer YOUR-API-KEY'}

result = requests.get('http://DEALSTAT-API-URL.com/<file_type>?file_id=<FILE-ID>', headers=headers)

print(result)

```

```shell
curl -i -X 'GET' 'http://DEALSTAT-API-URL.com/title_deed?file_id=<FILE-ID>'
  -H "Authorization: Bearer Your-API-KEY"
```

> Property deeds return JSON structured like this:

```json
{
  "file_id": "krzmuujooydnmjnpjgepzhifn",
  "status": "complete",
  "results": {
  			 "bp": ["2412", "1504"],
 			 "instrument": "101070856",
 			 "executed_date":"2017-06-05",
 			 "recorded_date": "2017-06-05",
 			 "grantor": "Breaux Alexander Murphy",
 			 "grantee": "Breaux Alexander Murphy, Trustee of the Breaux Alexander Murphy Trust dated June 5, 2017",
 			 "consideration": 10,
 			 "legal_description": "UNIT 1B, BUILDING II, SILVER TOWN CONDOMINIUMS, A UTAH\nCONDOMINIUM PROJECT, TOGETHER WITH ITS APPURTENANT\nUNDIVIDED OWNERSHIP INTEREST IN THE COMMON AREAS TO THE\nABOVE MENTIONED UNIT OF SAID SILVER TOWN CONDOMINIUUMS,\nWHICH INTEREST IS ESTABLISHED AND IDENTIFIED IN THE\nCONDOMINIUM DECLARATION, RECORDED AS ENTRY NO. 137917\nAND SURVEY MAP FILED FOR RECORD AS ENTRY NO. 13267 AND AS\nMAY BE AMENDED BY THE FIRST SUPPLEMENTAL RECORD OF\nSURVEY RECORDED AS ENTRY NO. 289073.",
 			 "document_type": "GRANT DEED",
 			 "accept": true
 		}
}

```

> Offering memorandums return JSON structured like this:

```json
{
  "file_id": "krzmuujooydnmjnpjgepzhifn",
  "status": "complete",
  "results": {
			"accept": true,
			 "confidence": "HIGH",
			 "cap_rate": 0.0562,
			 "acquisition_price": 3950000.0,
			 "property_location": {"address": "320 Macon Street",
			  "neighborhood": "Bedford-stuyvesant",
			  "city": "Brooklyn",
			  "state": "NY",
			  "lat": 40.6822488,
			  "lng": -73.938079,
			  "zip": "11216"},
			 "property_type": "multifamily",
			 "broker_email": "dj.johnston@cushwake.com",
			 "net_operating_income": 222080.0,
			 "total_square_feet": 6040,
			 "total_units": 7,
			 "total_expenses": 32836.0,
			 "effective_gross_revenue": 254916.0,
			 "portfolio_type": "no"
 		}
}

```

This endpoint retrieves data extracted from the PDF

### HTTP Request

<aside class="notice"> Make sure to replace DEALSTAT-API-URL with provided URL </aside>

`GET http://DEALSTAT-API-URL.com/<file_type>/file_id=<file_id>`

### URL Parameters

Parameter | Description
--------- | -----------
file_type | title_deed for property deed, om for offering memorandum

### Query Parameters

Parameter | Description
--------- | -----------
file_id | File ID returned in preceding POST request


