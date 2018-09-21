# Synchronization with VISION

VISION is an external database managed by UNICEF. We use it for fetching basic Partner information using the Vendor Number.

![](../.gitbook/assets/1q2ndt.jpg)

![](../.gitbook/assets/sieu8f.jpg)

By clicking on `add new vendor` and entering Partner Vendor Number, call through the api will be performed. If the record doesn't exist in the database, it will be searched in VISION using the following url:   
[https://devapis.unicef.org/BIService/BIWebService.svc/GetPartnerDetailsInfo\_JSON/&lt;vendor\_number&gt;](https://devapis.unicef.org/BIService/BIWebService.svc/GetPartnerDetailsInfo_JSON/<vendor_number>)  
In case of success, Partner information will be synced with the server database and then periodically refresh the actual data. 

Here is the response example:

```javascript
{
  'ROWSET': {
    'ROW': {
      'CITY': 'AHMEDABAD\\/GUJARAT',
      'COUNTRY': '204',
      'DATE_OF_ASSESSMENT': '01-JAN-16',
      'EMAIL': 'INFO@GRCGUJARAT.ORG',
      'NET_CASH_TRANSFERRED_CY': '0',
      'PARTNER_TYPE': 'GOVT',
      'PARTNER_TYPE_DESC': 'Government',
      'PHONE_NUMBER': '079-26301043',
      'POSTAL_CODE': '380015',
      'REPORTED_CY': '0',
      'RISK_RATING': 'Non-Assessed',
      'SEARCH_TERM1': 'GRC',
      'STREET': 'BLOCK NO.1',
      'TOTAL_CASH_TRANSFERRED_CP': '0',
      'TOTAL_CASH_TRANSFERRED_CY': '0',
      'TOTAL_CASH_TRANSFERRED_YTD': '0',
      'TYPE_OF_ASSESSMENT': 'Micro Assessment',
      'VENDOR_BANK': {
        'VENDOR_BANK_ROW': [
          {
            'BANK_ACCOUNT_NO': '032010100483698',
            'BANK_BRANCH': 'Vastrapur',
            'BANK_COUNTRY_KEY': '204',
            'BANK_KEY': 'UTIB0000032',
            'BANK_NAME': 'AXIS BANK LTD',
            'CITY': 'GUJARAT',
            'STREET': 'SHILALEKH, NEHRU PARK CIRCLE, VASTR',
            'SWIFT_CODE': 'UTIB0000032'
          }
        ]
      },
      'VENDOR_CODE': '2500224187',
      'VENDOR_NAME': 'GENDER RESOURCE CENTRE'
    }
  }
}
```

This response is mapped to Partner objects using the `TPMPartnerSynchronizer`. Fields mapping is presented below:

```text
"vendor_number": "VENDOR_CODE",
"name": "VENDOR_NAME",
"street_address": "STREET",
"city": "CITY",
"postal_code": "POSTAL_CODE",
"country": "COUNTRY",
"email": "EMAIL",
"phone_number": "PHONE_NUMBER",
"blocked": "POSTING_BLOCK",
"deleted_flag": "MARKED_FOR_DELETION",
```

If we synchronize the Partner manually, we also set `hidden` flag to hide the Partner from the base set, but save it into the database. In case of the confirmation of Partner addition, this flag will be changed to false and Partner will appear in the list.

