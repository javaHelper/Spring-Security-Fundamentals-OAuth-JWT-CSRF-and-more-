#

1) 

````shell
curl --location 'http://localhost:9091/couponapi/coupons/SUPERSALE' \
--header 'Authorization: Basic ZG91Z0BiYWlsZXkuY29tOmRvdWc=' \
--header 'Cookie: JSESSIONID=A92476488B8B3EB433EDE03DBA3B1788'
````

Response:

````
{
    "id": 1,
    "code": "SUPERSALE",
    "discount": 10.000,
    "expDate": "12/12/2022"
}
````