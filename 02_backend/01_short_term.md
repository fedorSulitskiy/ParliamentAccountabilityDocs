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
