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
        "id": 0,
        "papi_id": 185,
        "name": "Corbyn, Jeremy",
        "party": "Independent",
        "constituency": "Islington North",
        "description": "Rt Hon Jeremy Corbyn MP",
        "synopsis": {
            "value": "The Rt Hon Jeremy Corbyn is the Independent MP for <a href='/constituency/4120/overview'>Islington North</a>, and has been an MP continually since 9 June 1983.",
            "links": [
                {
                    "rel": "self",
                    "href": "/Members/185/Synopsis",
                    "method": "GET"
                }
                ...
            ]
        },
        "interests": [
            {
                "id": 3,
                "name": "2. (a) Support linked to an MP but received by a local party organisation or indirectly via a central party organisation",
                "sortOrder": 0,
                "interests": [
                    {
                        "id": 5980,
                        "interest": "Name of donor: We Deserve Better\r\nAddress of donor: Pelican House, 144 Cambridge Heath Rd, London E1 5QJ\r\nAmount of donation or nature and value if donation in kind: £10,000 for political Activities. This was repaid on 7 June 2024\r\nDonor status: unincorporated association\r\n(Registered 9 July 2024; updated 5 July 2024)",
                        "createdWhen": "2024-10-02T15:01:29.8166667",
                        "lastAmendedWhen": "2024-08-16T15:03:06.43",
                        "deletedWhen": null,
                        "isCorrection": false,
                        "childInterests": []
                    },
                    ...
                ]
            },
            ...
        ],
        "created_at": "0001-01-01T00:00:00Z",
        "updated_at": "0001-01-01T00:00:00Z"
    }
}
```
