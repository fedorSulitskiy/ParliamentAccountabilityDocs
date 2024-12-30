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
- [ ] Land they own on a map

## 28 - Dec - 2024

### Simple MP Data

- [ ] Contact Details for MPs
- [x] Use REGEX to get all £ numbers from each interest.
  - [x] InterestSummary Object implemented

### Complex MP Data

- [ ] `/Biography` mixin to MP object
- [ ] `/Voting` records mixin to MP object

### Constituency Data

- [ ] GeoJSON for constituency boundaries
- [ ] Latest Election results for the constituency
- [ ] Constituency summary

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
