# Classroom Api Doc
<details>
  <summary>Login Api</summary>

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


