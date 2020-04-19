---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell


includes:
  - errors

search: true
---

# Introduction

Welcome to the Fiwit API! You can use our API to access Fiwit API endpoints, which can get information on assets, tickets, and other elements from the Fiwit application.



# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: API_KEY" \
  -H "Accept: application/json"
```

> Make sure to replace `API_KEY` with your API key.

Fiwit uses API keys to allow access to the API. You can register a new Fiwit API key in [your user settings](https://www.fiwit.io/settings).

Fiwit expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: API_KEY`

<aside class="notice">
You must replace <code>API_KEY</code> with your personal API key.
</aside>

Moreover, in all your requests, you should indicate that you expect to receive JSON 
data using the `Accept: application/json` header. 

# Assets

Assets represent any element constituting your IT : server, database, software, phone, …

## List all assets

To list the assets, just issue a `GET` request to the `/assets` endpoint


```shell
# Request
curl "https://www.fiwit.io/assets" \
  -H "Authorization: API_KEY" \
  -H "Accept: application/json"
  
# Sample response
[
    {
        "id": 127,
        "name": "Laptop BERK42",
        "user_id": 85,
        "created_at": "2020-04-01T05:45:23.469Z",
        "updated_at": "2020-04-01T05:45:33.592Z",
        "assigned_id": null,
        "location_id": null,
        "asset_type_id": 362,
        "team_id": 111,
        "deleted_at": null,
        "ip_address": "12.13.14.15",
        "custom_field_values": [
            {
                "id": 197,
                "entity_type": "Asset",
                "entity_id": 127,
                "custom_field_id": 1002,
                "value": "5",
                "created_at": "2020-04-01T05:45:33.606Z",
                "updated_at": "2020-04-01T05:45:33.606Z",
                "team_id": 111,
                "deleted_at": null
            }
        ]
    }
]
```

## Get a specific asset

To get a specific asset, just issue a `GET` request to the `/assets` endpoint, and specify 
an id (ex: `/assets/127`)


```shell
# Request
curl "https://www.fiwit.io/assets/127" \
  -H "Authorization: API_KEY" \
  -H "Accept: application/json"
  
# Sample response
{
    "id": 127,
    "name": "Laptop BERK42",
    "user_id": 85,
    "created_at": "2020-04-01T05:45:23.469Z",
    "updated_at": "2020-04-01T05:45:33.592Z",
    "assigned_id": null,
    "location_id": null,
    "asset_type_id": 362,
    "team_id": 111,
    "deleted_at": null,
    "ip_address": "12.13.14.15",
    "custom_field_values": [
        {
            "id": 197,
            "entity_type": "Asset",
            "entity_id": 127,
            "custom_field_id": 1002,
            "value": "5",
            "created_at": "2020-04-01T05:45:33.606Z",
            "updated_at": "2020-04-01T05:45:33.606Z",
            "team_id": 111,
            "deleted_at": null
        }
    ]
}
```

## Create an asset

To create an asset, issue a `POST` request to the `/assets`endpoint. 


```shell
# Request
curl "https://www.fiwit.io/assets/" \
  -H "Authorization: API_KEY" \
  -H "Accept: application/json" \
  -H "Content-Type: application/json" \
  --request POST \
  --data '{"name":"Laptop Test"}'

  
# Sample response
{
  "id": 150,
  "name": "Laptop Test",
  "user_id": 85,
  "created_at": "2020-04-19T05:15:37.658Z",
  "updated_at": "2020-04-19T05:15:37.658Z",
  "assigned_id": null,
  "location_id": null,
  "asset_type_id": null,
  "team_id": 111,
  "deleted_at": null,
  "pairing_token": "AcZkKALxvjdR5b4dsbP3Dk85",
  "ip_address": null,
  "custom_field_values": []
}
```

## Update an asset


To update an asset, issue a `PATCH` request to the `/assets` endpoint, specifying an ID. 


```shell
# Request
curl "https://www.fiwit.io/assets/150" \
  -H "Authorization: API_KEY" \
  -H "Accept: application/json" \
  -H "Content-Type: application/json" \
  --request PATCH \
  --data '{"name":"Laptop Test V2"}'

  
# Sample response
{
  "id": 150,
  "team_id": 111,
  "user_id": 85,
  "assigned_id": null,
  "location_id": null,
  "asset_type_id": null,
  "name": "Laptop Test V2",
  "created_at": "2020-04-19T05:15:37.658Z",
  "updated_at": "2020-04-19T05:18:43.850Z",
  "deleted_at": null,
  "pairing_token": "AcZkKALxvjdR5b4dsbP3Dk85",
  "ip_address": null,
  "custom_field_values": []
}
```

## Get custom fields

If you need to specify custom fields, you need to input them in the `custom_field_values` array, 
using their ID. To get the IDs of all custom fields, issue a request to `/asset_fields` 

```shell
# Request
curl "https://www.fiwit.io/asset_fields" \
  -H "Authorization: API_KEY" \
  -H "Accept: application/json"

  
# Sample response
[
  {
    "id": 363,
    "name": "Phone",
    "user_id": 85,
    "created_at": "2020-04-01T05:29:15.710Z",
    "updated_at": "2020-04-01T05:29:15.725Z",
    "team_id": 111,
    "deleted_at": null,
    "is_machine": false
  }
]
```

## Get asset types
Same goes if you would like to specify a given asset type when creating a resource. 
You can list all the available asset types at: `/asset_types`

```shell
# Request
curl "https://www.fiwit.io/asset_types" \
  -H "Authorization: API_KEY" \
  -H "Accept: application/json"

  
# Sample response
[
  {
    "id": 1005,
    "name": "model",
    "description": null,
    "type": "string",
    "value": null,
    "user_id": 85,
    "entity_type_type": "AssetType",
    "entity_type_id": 363,
    "created_at": "2020-04-01T05:29:15.829Z",
    "updated_at": "2020-04-01T05:29:15.829Z",
    "team_id": 111,
    "deleted_at": null,
    "default_value": null
  }
]
```



# Tickets

Tickets represent customer assistance requests, and, they can be retrieved
using the API. 

## List all tickets

To list the tickets, just issue a `GET` request to the `/tickets` endpoint


```shell
# Request
curl "https://www.fiwit.io/tickets" \
  -H "Authorization: API_TOKEN" \
  -H "Accept: application/json"
  
# Sample response
[
   {
      "assigned_id" : null,
      "ticket_type_id" : 196,
      "status_changed_at" : "2020-04-18T05:58:25.021Z",
      "priority" : "medium",
      "team_id" : 111,
      "deleted_at" : null,
      "created_at" : "2020-04-18T05:58:25.021Z",
      "name" : "Intercom ticket #26607347877",
      "user_id" : 85,
      "updated_at" : "2020-04-18T05:58:25.021Z",
      "status" : "new",
      "id" : 52,
      "intercom_url" : "https://app.intercom.com/a/apps/ygjdratr/inbox/inbox/all/conversations/26607347877",
      "custom_field_values" : []
   }
]
```

## Get a specific ticket

To get a specific ticket, just issue a `GET` request to the `/tickets` endpoint, and specify 
an id (ex: `/tickets/52`)


```shell
# Request
curl "https://www.fiwit.io/tickets/52" \
  -H "Authorization: API_TOKEN" \
  -H "Accept: application/json"
  
# Sample response
{
   "status" : "new",
   "created_at" : "2020-04-18T05:58:25.021Z",
   "id" : 52,
   "assigned_id" : null,
   "custom_field_values" : [],
   "ticket_type_id" : 196,
   "deleted_at" : null,
   "team_id" : 111,
   "name" : "Intercom ticket #26607347877",
   "status_changed_at" : "2020-04-18T05:58:25.021Z",
   "updated_at" : "2020-04-18T05:58:25.021Z",
   "user_id" : 85,
   "priority" : "medium",
   "intercom_url" : "https://app.intercom.com/a/apps/ygjdratr/inbox/inbox/all/conversations/26607347877"
}
```

## Create a ticket

To create a ticket, issue a `POST` request to the `/tickets`endpoint. 


```shell
# Request
curl "https://www.fiwit.io/tickets/" \
  -H "Authorization: API_TOKEN" \
  -H "Accept: application/json" \
  -H "Content-Type: application/json" \
  --request POST \
  --data '{"priority":"medium"}'

  
# Sample response
{
   "ticket_type_id" : null,
   "team_id" : 111,
   "updated_at" : "2020-04-19T05:28:39.517Z",
   "status_changed_at" : "2020-04-19T05:28:39.517Z",
   "id" : 55,
   "status" : "new",
   "user_id" : 85,
   "priority" : "medium",
   "intercom_url" : null,
   "assigned_id" : null,
   "name" : "T-4",
   "created_at" : "2020-04-19T05:28:39.517Z",
   "deleted_at" : null,
   "custom_field_values" : []
}
```

## Update a ticket


To update a ticket, issue a `PATCH` request to the `/tickets` endpoint, specifying an ID. 


```shell
# Request
curl "https://www.fiwit.io/tickets/55" \
  -H "Authorization: API_TOKEN" \
  -H "Accept: application/json" \
  -H "Content-Type: application/json" \
  --request PATCH \
  --data '{"priority":"low"}'

  
# Sample response
{
   "created_at" : "2020-04-19T05:28:39.517Z",
   "deleted_at" : null,
   "ticket_type_id" : null,
   "updated_at" : "2020-04-19T05:29:00.682Z",
   "intercom_url" : null,
   "custom_field_values" : [],
   "name" : "T-4",
   "status" : "new",
   "team_id" : 111,
   "id" : 55,
   "user_id" : 85,
   "priority" : "low",
   "assigned_id" : null,
   "status_changed_at" : "2020-04-19T05:28:39.517Z"
}
```

## Get custom fields

If you need to specify custom fields, you need to input them in the `custom_field_values` array, 
using their ID. To get the IDs of all custom fields, issue a request to `/ticket_fields` 

```shell
# Request
curl "https://www.fiwit.io/ticket_fields" \
  -H "Authorization: API_TOKEN" \
  -H "Accept: application/json"

  
# Sample response
[
   {
      "deleted_at" : null,
      "name" : "Asset impacted",
      "team_id" : 111,
      "description" : "",
      "id" : 1780,
      "created_at" : "2020-04-18T06:33:56.645Z",
      "user_id" : 85,
      "type" : "string",
      "updated_at" : "2020-04-18T06:33:56.645Z",
      "entity_type_id" : 196,
      "entity_type_type" : "TicketType",
      "value" : null,
      "default_value" : null
   }
]
```

## Get ticket types
Same goes if you would like to specify a given ticket type when creating a resource. 
You can list all the available ticket types at: `/ticket_types`

```shell
# Request
curl "https://www.fiwit.io/ticket_types" \
  -H "Authorization: API_TOKEN" \
  -H "Accept: application/json"

  
# Sample response
[
   {
      "created_at" : "2020-04-01T05:29:16.373Z",
      "name" : "Support request",
      "updated_at" : "2020-04-01T05:29:16.391Z",
      "deleted_at" : null,
      "team_id" : 111,
      "id" : 197,
      "user_id" : 85
   }
]
```


# Locations

Locations represent places where you can store assets. 

## List all locations

To list the locations, just issue a `GET` request to the `/locations` endpoint


```shell
# Request
curl "https://www.fiwit.io/locations" \
  -H "Authorization: API_TOKEN" \
  -H "Accept: application/json"

# Sample response
[
   {
      "name" : "Main headquarter",
      "created_at" : "2020-04-17T04:46:15.131Z",
      "id" : 16,
      "updated_at" : "2020-04-17T04:46:15.131Z",
      "location" : "AAZ",
      "deleted_at" : null,
      "user_id" : 85,
      "team_id" : 111
   }
]
```


# Users

Users are all your colleagues in the Fiwit platform. 

## List all users
 
To list the locations, just issue a `GET` request to the `/users` endpoint


```shell
# Request
curl "https://www.fiwit.io/teams" \
  -H "Authorization: API_TOKEN" \
  -H "Accept: application/json"

# Sample response
[{"id"=>1024, "email"=>"alexis@fiwit.io", "role"=>"platform_user", "first_name"=>"Alexis", "last_name"=>"Clarembeau"}]
```
