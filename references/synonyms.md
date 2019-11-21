# Synonyms

## List one synonym

<RouteHighlighter method="GET" route="/indexes/:index/synonyms/:synonym"/>

List one sequence and his synonyms inside an index.

#### Headers

| Header              | Value            |
|---------------------|------------------|
| **X-Meili-API-Key** | `$API_KEY`       |
| **Content-Type**    | application/json |
| **Accept-encoding** | gzip, deflate    |

#### Path Variables

| Variable          | Description           |
|-------------------|-----------------------|
| **index**         | The index UID |
| **synonym**         | Sequence of which the synonyms will be returned |


#### Example
```bash
 curl \
  --location \
  --request GET 'http://localhost:8080/indexes/movies/synonyms/magician' \
  --header 'Content-Type: application/json' \
  --header "X-Meili-API-Key: $API_KEY" \
```

#### Response: `200 OK`


```json
["harry","merlin"]
```
array of synonyms of the given sequence in the path variable. 

## List all synonyms

<RouteHighlighter method="GET" route="/indexes/:index/synonyms"/>

List all sequences and their synonyms inside an index.

#### Headers

| Header              | Value            |
|---------------------|------------------|
| **X-Meili-API-Key** | `$API_KEY`       |
| **Content-Type**    | application/json |
| **Accept-encoding** | gzip, deflate    |

#### Path Variables

| Variable          | Description           |
|-------------------|-----------------------|
| **index**         | The index UID |


#### Example
```bash
 curl \
  --location \
  --request GET 'http://localhost:8080/indexes/movies/synonyms' \
  --header 'Content-Type: application/json' \
  --header "X-Meili-API-Key: $API_KEY" \
```

#### Response: `200 OK`

```json
{
  "potter": [
    "harry"
  ],
  "magician": [
    "harry",
    "merlin"
  ],
  "harry": [
    "potter"
  ]
}
```


## Create synonyms

<RouteHighlighter method="POST" route="/indexes/:index/synonyms"/>

Create synonyms.

#### Headers

| Header              | Value            |
|---------------------|------------------|
| **X-Meili-API-Key** | `$API_KEY`       |
| **Content-Type**    | application/json |
| **Accept-encoding** | gzip, deflate    |

#### Path Variables

| Variable          | Description           |
|-------------------|-----------------------|
| **index**         | The index UID |

#### Body

| key          | Value description           |
|-------------------|-----------------------|
| **input**         | the [one-way string](/advanced_guides/synonyms.md#the-one-way-association) that is gonna be associated with the synonyms array |
| **synonyms**         | array of words to associate together in [a multi-way](/advances_guides/synonymss.md##the-multi-way-association) |

An object with either multi-way string associations or one-way string association. 

#### One-way Example
```bash
 curl \
  --location \
  --request POST 'http://localhost:8080/indexes/movies/synonyms' \
  --header 'Content-Type: application/json' \
  --header "X-Meili-API-Key: $API_KEY" \
  --data '{ "input": "magician", "synonyms": ["harry potter", "merlin"]}'
```

#### Multi-way Example
```bash
 curl \
  --location \
  --request POST 'http://localhost:8080/indexes/movies/synonyms' \
  --header 'Content-Type: application/json' \
  --header "X-Meili-API-Key: $API_KEY" \
  --data '{ "synonyms": ["harry potter", "hp"]}'
```

#### Response: `202 Accepted`

```json
{
  "updateId" : 1
}
```
This [update id allows you to track](/references/updates) the current action.

## Update a synonym

<RouteHighlighter method="PUT" route="/indexes/:index/synonyms/:synonym"/>

Update a synonym.

#### Headers

| Header              | Value            |
|---------------------|------------------|
| **X-Meili-API-Key** | `$API_KEY`       |
| **Content-Type**    | application/json |
| **Accept-encoding** | gzip, deflate    |

#### Path Variables

| Variable          | Description           |
|-------------------|-----------------------|
| **index**         | The index UID |
| **synonym**         | Sequence of which the synonyms will be updated |

#### Body

An array of string containing all synonyms of the given sequence.

::: warning
This will **override** the previous synonyms of the given sequence. Don't forget to add them if you dont want to lose them.
:::

#### Example
```bash
 curl \
  --location \
  --request PUT 'http://localhost:8080/indexes/movies/synonyms/magician' \
  --header 'Content-Type: application/json' \
  --header "X-Meili-API-Key: $API_KEY" \
  --data '["harry potter", "merlin", "Illusionist"]'
```

#### Response: `200 Ok`

```json
{
  "updateId" : 1
}
```
This [update id allows you to track](/references/updates) the current action.

## Delete a synonym

<RouteHighlighter method="DELETE" route="/indexes/:index/synonyms/:synonym"/>

Delete a synonym.

#### Headers

| Header              | Value            |
|---------------------|------------------|
| **X-Meili-API-Key** | `$API_KEY`       |
| **Content-Type**    | application/json |
| **Accept-encoding** | gzip, deflate    |

#### Path Variables

| Variable          | Description           |
|-------------------|-----------------------|
| **index**         | The index UID |
| **synonym**         | Sequence of which the synonyms will be deleted |


#### Example
```bash
 curl \
  --location \
  --request DELETE 'http://localhost:8080/indexes/movies/synonyms/magician' \
  --header 'Content-Type: application/json' \
  --header "X-Meili-API-Key: $API_KEY" \
```

#### Response: `200 Ok`

```json
{
  "updateId" : 1
}
```
This [update id allows you to track](/references/updates) the current action.

## Batch write synonyms

<RouteHighlighter method="POST" route="/indexes/:index/synonyms/batch"/>

Batch write synonyms.

#### Headers

| Header              | Value            |
|---------------------|------------------|
| **X-Meili-API-Key** | `$API_KEY`       |
| **Content-Type**    | application/json |
| **Accept-encoding** | gzip, deflate    |

#### Path Variables

| Variable          | Description           |
|-------------------|-----------------------|
| **index**         | The index UID |

#### Body

| key          | Value description           |
|-------------------|-----------------------|
| **input**         | the [one-way string](/advanced_guides/synonymss.md#the-one-way-association) that is gonna be associated with the synonyms array |
| **synonyms**         | array of words to associate together in [a multi-way](/advances_guides/synonymss.md##the-multi-way-association) |

An object with either multi-way string associations or one-way string association. 

#### Example
```bash
 curl \
  --location \
  --request POST 'http://localhost:8080/indexes/movies/synonyms/batch' \
  --header 'Content-Type: application/json' \
  --header "X-Meili-API-Key: $API_KEY" \
  --data '[
    { 
      "input": "magician", 
      "synonyms": ["harry potter", "merlin", "illusionist"]
    }, 
    {  
      "synonyms" : ["mickey", "mouse"]
    }
  ]'
```

#### Response: `202 Accepted`

```json
{
  "updateId" : 1
}
```
This [update id allows you to track](/references/updates) the current action.


## Clear synonyms

<RouteHighlighter method="DELETE" route="/indexes/:index/synonyms"/>

Delete all synonyms

#### Headers

| Header              | Value            |
|---------------------|------------------|
| **X-Meili-API-Key** | `$API_KEY`       |
| **Content-Type**    | application/json |
| **Accept-encoding** | gzip, deflate    |

#### Path Variables

| Variable          | Description           |
|-------------------|-----------------------|
| **index**         | The index UID |


#### Example
```bash
 curl \
  --location \
  --request DELETE 'http://localhost:8080/indexes/movies/synonyms' \
  --header 'Content-Type: application/json' \
  --header "X-Meili-API-Key: $API_KEY" \
```

#### Response: `202 Accepted`

```json
{
  "updateId" : 1
}
```
This [update id allows you to track](/references/updates) the current action.