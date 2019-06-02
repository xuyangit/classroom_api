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
  <summary>Login Api</summary>

</details>

<details>
  <summary>Login Api</summary>

</details>

<details>
  <summary>Login Api</summary>

</details>
