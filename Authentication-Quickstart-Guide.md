# Sign Up and Authentication Quickstart Guide

To gain access to IQM's API and its services, first the user must sign up and log in to obtain the authentication required to send requests.

## Sign Up

Sign up for an account by providing an email address and desired password with the following endpoint:

<span class="badge-post"> POST </span> <span class="code-text">/api/v3/ua/sign-up </span>


---

#### Header Parameters

{% json-schema
  schema={
    "type": "object",
    "title": "Authorization",
    "properties": {
      "Authorization": {
        "type": "string | required | header",
        "description": "API token"
      }
    }
  }
/%}

#### Body 

{% json-schema
  schema={
    "title": "Body",
    "type": "object",
    "properties": {
      "email": {
        "type": "string | required",
        "description": "Email address of user"
      },
      "password": {
        "type": "string | required",
        "description": "Desired password of user"
      },
    }
  }
/%}




```json {% title="Request" %}
{
  "email": "user1@iqm.com",
  "password": "123456"
}
```

```json {% title="Response 200" %}
{
    "success": true,
    "data": {
        "access_token": "d90fa7de-534c-4652-ad8f-c4f6f70461ac",
        "refresh_token": "2e379c6f-959d-498f-8319-ff13ebef6bfe",
        "scope": "read write",
        "token_type": "bearer",
        "expires_in": 35999
    }
}
```

## Log In

Once a user has created an account, they can perform the login. This API will send OAuth compliant response with OW Id which can be used for any further API communications. Use the following endpoint:

<span class="badge-post"> POST </span> <span class="code-text">/api/v3/ua/login </span>

<span class="badge"> POST </span>

---

#### Header Parameters

{% json-schema
  schema={
    "title": "Authorization",
    "type": "object",
    "properties": {
      "Authorization": {
        "type": "string | required",
        "description": "API token"
      },
      "X-IAA-HOST": {
        "type": "string | required",
        "description": "Workspace URL"
      },
    }
  }
/%}

#### Body

{% json-schema
  schema={
    "title": "Body",
    "type": "object",
    "properties": {
      "grantType": {
        "type": "string | required",
        "description": "[OAuth Grant Types](https://oauth.net/2/grant-types/)"
      },
      "email": {
        "type": "string | required",
        "description": "User account email"
      },
        "password": {
        "type": "string | required",
        "description": "User account password"
      },
    }
  }
/%}

```json {% title="Request" %}
{
    "grantType": "password",
    "email": "user1@iqm.com",
    "password": "123456"
}
```

```json {% title="Response 200" %}
{
    "success": true,
    "data": {
        "access_token": "106adb25-37b0-4cab-8381-d682fe7cc3c8",
        "refresh_token": "eac4c1f6-781e-4b04-baff-9c2e415d1f64",
        "scope": "read write",
        "token_type": "bearer",
        "expires_in": 35999,
        "owId": 200001
    }
}
```