# 📍 Endpoints

This page will have a subset of the endpoints implemented. These are the ones that are used in the frontend.

> [!WARNING]
> ***Unless specified otherwise, all endpoints have root `/api/`.***

> [!TIP]
> Look into the [`models`](https://github.com/fedorSulitskiy/ParliamentAccountabilityBackend/tree/main/lib/models) folder in the backend to have further understanding of the data structure.

## 📌 GET `/mps/`

This endpoint returns a list of MPs, *as saved in our database*. The list is paginated and the default page size is 20.

### Request

```http
GET api/mps/
```

### Response

```json
{
    "status": 200,
    "message": 650, // Total number of MPs in the DB (not the number of MPs in this response)
    "data": [
        {
            "id": 6,
            "papi_id": 4359,
            "name": "Kinnock, Stephen",
            "party": "Labour",
            "constituency": "Aberafan Maesteg",
            "description": "Stephen Kinnock MP",
            "created_at": "2024-12-27T19:07:11.761268Z",
            "updated_at": "2024-12-27T19:07:11.761268Z"
        },
        {
            "id": 7,
            "papi_id": 4357,
            "name": "Blackman, Kirsty",
            "party": "Scottish National Party",
            "constituency": "Aberdeen North",
            "description": "Kirsty Blackman MP",
            "created_at": "2024-12-27T19:07:11.77018Z",
            "updated_at": "2024-12-27T19:07:11.77018Z"
        },
        ...
    ]
}
```

## 📌 GET `/papi/mps/by-name/:name`

This endpoint taps directly into the Parliament's API and returns a more comprehensive data on the MP.

### Request

```http
GET api/papi/mps/by-name/:name
```

### Response

Note the *default* values; since we get data from the P-API directly this kind of data can't be expected.

```json
{
    "status": 200,
    "message": "MP found",
    "data": {
        "id": 0, // default value
        "papi_id": 4514,
        "name": "Starmer, Sir Keir",
        "party": "Labour",
        "constituency": "Holborn and St Pancras",
        "description": "Rt Hon Sir Keir Starmer MP",
        "created_at": "0001-01-01T00:00:00Z", // default value
        "updated_at": "0001-01-01T00:00:00Z" // default value
    }
}
```
