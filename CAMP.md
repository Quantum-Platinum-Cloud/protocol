# CAMP - Crypto Alias Management Protocol

CAMP is a sub-protocol of OpenCap. CAMP is an optional protocol that allows a server to facilitate the creation, updating, and deletion of a user's alias resources. For a server to be CAMP compliant it must also be CAP compliant by serving aliases, CAMP is essentially a "tier 2" protocol built on top of CAP to add some more features.

The following endpoints are required:

## POST /v1/users

No Authorization (Public method)

Creates a new user.

Body:
```javascript
{
    "username": "john", // the username that will be the first part of the alias
    "domain": "ogdolo.com", // the domain that makes up last part of the alias
    "password": "mysecretpassword"
}
```

Response:
```javascript
Status: 200
{}
```

Note: The "domain" parameter is so that IF this CAMP server is also a CAPP server it can host aliases that use other proxy domains. See the ([CAPP](/CAPP.md)) file for more info.

## POST /v1/auth

Authorization Bearer {jwt}

Authenticates a user to be able to use the JWT for the other endpoints

Body:
```javascript
{
    "username": "lane",
    "password": "su93rS3cret"
}
```

Response:
```javascript
Status: 200
{
    "jwt": "ujahsdbf9dfsf.sdf8ihnsd9fgasdsdfusd8f0adf78f.ud8fs0fbsf"
}
```

## DELETE /v1/users

Authorization Bearer {jwt}

Deletes the authenticated user and all associated addresses.

Response:
```javascript
Status: 200
{
}
```

## PUT /v1/address

Authorization Bearer {jwt}

Adds or updates the address for the authenticated user of the given asset.  

Body:
```javascript
{
    "asset": 0, // 0 = BTC
    "type": "segwit",
    "address": "bc1qvw0ytfntx6zs0lfsruem6xwj0mewng523ktatp"
}
```

Response:
```javascript
Status: 200
{
}
```

## DELETE /v1/address/{asset}

Authorization Bearer {jwt}

Deletes the address for the user of the given asset.  

Response:
```javascript
Status: 200
{
}
```