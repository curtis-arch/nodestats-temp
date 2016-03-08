
## Add a record

GET /requests/create
+ user, string, optional
+ project, string, optional
+ eventType, string, optional
+ event, string, optional
+ content, string, optional
+ metadata, string, optional
+ ip, string, optional, defaults from request
+ userAgent, string, optional, defaults from request
+ timestamp, number, optional, unix offset, defaults to now
+ callback, string, optional, jsonp callback parameter

Sample response:
```json
{
    "success": true,
    "data": {
        "deleted": 0,
        "errors": 0,
        "generated_keys": ["6540e7f2-bc73-46d9-a813-dfcb8f24d919"],
        "inserted": 1,
        "replaced": 0,
        "skipped": 0,
        "unchanged": 0
    },
    "error": null
}
```

The API will try to parse out any date. Just be aware it could have some limitations
and you will achieve best results by passing it a preferred format.

## Query for requests

GET /requests
Filters:
+ user, string, optional
+ project, string, optional
+ eventType, string, optional
+ event, string, optional
+ ip, string, optional
+ start, date, required, ISO 8601 format
+ end, date, required, ISO 8601 format
+ limit, number, optional

Sample output:
```json
{
    "success": true,
    "error": null,
    "data": [{
        "content": "content0.9569159653037786",
        "timestamp": 1423285070905,
        "event": "event0.9540031442884356",
        "eventType": "eventType0.7074686523992568",
        "id": "0680c0f8-594b-418d-b237-ee5a3a95d46a",
        "ip": "ip0.42774740792810917",
        "metadata": "metadata0.1415706172119826",
        "project": "project0.23264494352042675",
        "user": "user0.3856971587520093",
        "userAgent": "userAgent0.7797085801139474"
    }, {
        "content": "content0.20633318228647113",
        "timestamp": 1423285070905,
        "event": "event0.8371858799364418",
        "eventType": "eventType0.9380447180010378",
        "id": "09e65f94-53e0-46aa-b5c4-2db54dd51e4b",
        "ip": "ip0.03233872936107218",
        "metadata": "metadata0.2804808602668345",
        "project": "",
        "user": "user0.7853867907542735",
        "userAgent": "userAgent0.06947706546634436"
    }]
}
```

## Query for request daily report

GET /requests/daily
** The filters are the same as /requests

Sample output:
```json
{
    "success": true,
    "error": null,
    "url":"/requests/daily?user=usertest&start=2015-02-22&end=2015-02-22"
    "data": {
        "total": 94,
        "days": {
            "2015-02-22": 90,
        }
    }
}
```

## Query for request hourly report

GET /requests/hourly
** The filters are the same as /requests

Sample output:
```json
{
    "success": true,
    "data": {
        "total": 0,
        "hours": [
            {
                "time": "2015-02-23T00:00:00-07:00",
                "reqs": 0
            }
        ]
    },
    "error": null,
    "url": "/requests/hourly?user=usertest&start=2015-02-23&end=2015-02-23"
}
```
