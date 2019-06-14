

# Template API


Description of functionality

## Specification

### resource
* GET [resource](#get-resources)
* GET [resource/{id}](#get-resource)

## Requirements

**API Prefix:** `/resource` 

|Query parameter|Type|Description|
|--|--|--|
|[id](dataformats.md#id)|string|Resource id|


## Endpoints

<h3 id="get-resources">GET /resource</h3>

|Header|Description|
|--|--|
|If-Modified-Since|Filter by resources modified after timestamp|

|Query string|Type|Description|
|--|--|--|
|filter|string|Filter by value|


Fetch resources

Get all:
```http
GET /api/2.4/resource
```

Request resources modified after date:
```http
GET /api/2.4/resource 
If-Modified-Since: Tue, 05 Feb 2019 14:03:15 GMT
```

Request resources with filter:
```http
GET /api/2.4/resource?key=val 
```


List of users response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "param": "example",
  }
]
```

|Parameter|Type|Description|
|--|--|--|
|param|string|Example param description|

<h3 id="get-resource">GET /resource/{id}</h3>

Request specific resource
```http
GET /api/2.4/resource/{id} 
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "param": "example"
}
```

|Parameter|Type|Description|
|--|--|--|
|param|string|Example param description|
