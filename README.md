# Classroom Api Doc
<details>
  <summary>Login</summary>

Used to login. 

**URL** : `/loginUser`

**Method** : `POST`

**Data constraints**

| Form key | Data type |
|----------|-----------|
| userid   | string    |
| password | string    |



## Success Response
Should redirect to /$(redirect) (e.g., /home here) based on the json result.

```json
{
    "err": "",
    "redirect": "home"
}
```

## Error Response

**Condition** : If 'userid' and 'password' combination is wrong.

**Content** :

```json
{
    "err": "invalid",
    "redirect": ""
}
```
</details>

<details>
  <summary>Register Pre-validation</summary>

Used to prevalidate the register fields. For example, check if the user name has been used and show tips below the input textbox.

**URL** : `/register/validation`

**Method** : `POST`

**Data constraints**

```json
{
    "field": "id",
    "data": "the input user id"
}
```



## Success Response
Error field is empty.

```json
{
    "err": ""
}
```

## Error Response

**Condition** : If user name has been used.

**Content** :

```json
{
    "err": "USERNAME_ALREADY_EXIST"
}
```

</details>

<details>
  <summary>Register</summary>
  Used to register new user.

**URL** : `/register`

**Method** : `POST` or `GET` (`GET` request will return the static html for registration.)

**Data constraints**

| Form key | Data type |
|----------|-----------|
| userid   | string    |
| password | string    |
| name | string |



## Success Response
Error field is empty. Should redirect to the /$(redirect) page.

```json
{
    "err": "",
    "redirect": "login"
}
```

## Error Response

**Condition** : If user name has been used.

**Content** :

```json
{
    "err": "USERNAME_ALREADY_EXIST"
    "redirect": ""
}
```

</details>

<details>
  <summary>Logout</summary>
Used to logout.

**URL** : `/logout`

**Method** : `POST`

**Data constraints**

No data needed. Get user information from the token in cookies.



## Success Response


```json
{
    "logout": True,
    "redirect": "login"
}
```
</details>

<details>
  <summary>Login Api</summary>

</details>
