# ⛹️ Short Term Backend Tasks

- [x] Set up database
- [x] Set up basic API structure
- [x] Deploy the backend (somewhere)

## 27 - Dec - 2024

Cron job to run across all contituencies and get the MP names. Store the names in the database.
Then keep the list of MP names and ids up to date.

When we need specific data we search for first 20(?) MPs in the database and then use their names to get the specific data.

- [x] GET MP data from API
- [x] How much money they make
- [x] Their interests (financial)
- [x] Their contituency
- [x] Their party
- ❗ Land they own on a map

## 28 - Dec - 2024

### Simple MP Data

- [x] Contact Details for MPs
- [x] Use REGEX to get all £ numbers from each interest.
  - [x] InterestSummary Object implemented

### Complex MP Data

- [x] `/Biography` mixin to MP object
- ❗ `/Voting` records mixin to MP object

### Constituency Data

- [x] GeoJSON for constituency boundaries
- [x] Latest Election results for the constituency
- [x] Constituency summary

## 30 - Dec - 2024

_Proposed change to the `InterestSumary` object:_

### `InterestSummary` Object

This would allow for an attachment of all interest summary fields to a single field. So now we won't have to rely on the order of strings and dates in the `InterestSummary` arrays.

```go
type InterestSummary struct {
	Value          *int64     `json:"value"`
	AcceptedDate   *time.Time `json:"acceptedDate"`
	ReceivedDate   *time.Time `json:"receivedDate"`
	RegisteredDate *time.Time `json:"registeredDate"`
}
```

### `Interest` Object

Many `InterestSummary` objects per `Interest` because one interest can have multiple child interests.
Total value is the sum of all value fields in the `InterestSummary` objects.

```go
type Interest struct {
	ID              int               `json:"id"`
	Interest        string            `json:"interest"`
	CreatedWhen     string            `json:"createdWhen"`
	LastAmendedWhen *string           `json:"lastAmendedWhen"`
	DeletedWhen     *string           `json:"deletedWhen"`
	IsCorrection    bool              `json:"isCorrection"`
	ChildInterests  []ChildInterest   `json:"childInterests"`
	Summary         []InterestSummary `json:"summary"`
    TotalValue      int64             `json:"totalValue"`
}
```

### `ChildInterest` Object

One `InterestSummary` per child interest.

```go
type ChildInterest struct {
	ID              int             `json:"id"`
	Interest        string          `json:"interest"`
	CreatedWhen     string          `json:"createdWhen"`
	LastAmendedWhen *string         `json:"lastAmendedWhen"`
	DeletedWhen     *string         `json:"deletedWhen"`
	IsCorrection    bool            `json:"isCorrection"`
	ChildInterests  []ChildInterest `json:"childInterests"`
	Summary         InterestSummary `json:"summary"`
}
```

## 11 - Feb - 2025

### New Tasks:

- [ ] Remove `loguru` dependency on the logger
	- Write custom logger
- [ ] Remove `gin` dependency on the router
	- Write custom router using standard library
- [ ] Run the bakend as binaries instead of using docker
	- [ ] Use `nix` to manage the environment
	- [ ] Use `nix` to manage the deployment
- [ ] Modularise the nix configuration
	- [Reference](https://www.youtube.com/watch?v=vYc6IzKvAJQ&t=31s)
- [ ] Manage secrets on nix using SOPS
	- [Reference](https://www.youtube.com/watch?v=G5f6GC7SnhU)
- [ ] Expose the API to the internet using Cloudflare Zero Trust