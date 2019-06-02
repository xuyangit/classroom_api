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
  <summary>Get assignments</summary>

Used to get assignments for user.

**URL** : `/assignments`

**Method** : `GET`

**Data constraints**

No data needed. Get user information from the token in cookies.



## Success Response
The data field contains a series of assignments. The problem id is used to get problem from the server by /problem?problemId=xxxxx.

```json
{
	"data":
    {
    	"AssignmentNameX":
        {
       		"problemIds": ["10001","20003"],
            "repoFullName":"private-cr-test/firsthw"
        },
        "AssignmentNameY":
        {
        	"problemIds": ["10003"]
            "repoFullName": "xxxx/xxxxx"
        }
    },
    "err": ""
}
```

## Error Response

**Condition** : If no assignments found.

**Content** :

```json
{
    "err": "NotFound"
    "data": {}
}
```
</details>

<details>
  <summary>Get problem content</summary>
	Used to get problem details.

**URL** : `/problem`

**Method** : `GET`

**Data constraints**


| Form key | Data type |
|----------|-----------|
| problemId   | string    |



## Success Response


```json
{
	"data": "problem content based on markdown template",
    "err": ""
}
```
The data field is in the format of markdown.We reuse your solution.
The template is like this:
```text
# {problem name}
## 题目描述
{problem description}
## 输入
{input}
## 输出
{output}
<button>开始答题</button>
```

## Error Response

**Condition** : If problemId is null.

**Content** :

```json
{
    "err": "InvalidArg"
    "data": ""
}
```
</details>

<details>
  <summary>Submit assignment</summary>
	
Used to submit assignment.

**URL** : `/submit`

**Method** : `POST`

**Data constraints**
Repo name is used instead of assignment name. We need the repo name so that we can perform following git operations. As the frontend has requested for the assignments information, don't discard the repo name fields so that you can use them here.
```json
{
	"repoFullName": "private-cr-test/firsthw",
	"code":
	{
		"10001": "import os\nprint('here2')",
		"20003": "import os\nprint('here3')"
	}
}
```



## Success Response
If error is empty, the submit is successfully submitted but need to run for a while. Use the runId to query for the submit's current state.
```json
{
    "err": "",
    "runId": "9c291e19-de52-473e-92b2-7d9d086e791a"
}
```


## Error Response

**Condition** : (1) Last submit is not completed; or (2) Submit too frequently; or (3) No changes compared to last submit.

**Content** :

```json
{
    "err": "NotReady",
    "runId": ""
}
```
</details>
