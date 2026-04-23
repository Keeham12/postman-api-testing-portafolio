# Bug Reports
## Distribusion QA Practice — Deutsche Bahn API

---

## BUG-001
- **Title:** Empty query string returns error instead of descriptive message
- **Steps to reproduce:** Send GET https://v6.db.transport.rest/locations?query=
- **Expected:** 400 Bad Request with clear error message explaining query cannot be empty
- **Actual:** Error returned but message is not descriptive enough for a retailer to handle gracefully
- **Severity:** Medium
- **Impact:** Retailers like Google Maps calling this API with an accidental empty query would receive an unhelpful error — making it harder to debug integration issues

---

## BUG-002
- **Title:** Nonsense string query returns closest city match instead of empty results
- **Steps to reproduce:** Send GET https://v6.db.transport.rest/locations?query=zzzzzzz
- **Expected:** 200 OK with empty results array — nonsense string should match no real locations
- **Actual:** 200 OK — API returned closest city match instead of empty array
- **Severity:** Medium
- **Impact:** Retailers displaying search results could show irrelevant locations to travellers — a user searching for a nonsense string should see no results, not a random city. Fuzzy matching behaviour needs clarification from the team on whether this is intended

---

## BUG-003
- **Title:** Special characters in query return closest match instead of empty results
- **Steps to reproduce:** Send GET https://v6.db.transport.rest/locations?query=!@#$%^
- **Expected:** 400 Bad Request or 200 OK with empty results array — special characters should not match real locations
- **Actual:** 200 OK — API returned a closest city match for a special character query
- **Severity:** Medium
- **Impact:** Special character inputs should be handled gracefully. Returning a real location for !@#$%^ could cause incorrect results to be displayed to travellers on retailer platforms like Booking.com

---

## BUG-004
- **Title:** Unicode city name returns correct match
- **Steps to reproduce:** Send GET https://v6.db.transport.rest/locations?query=Berlín
- **Expected:** 200 OK with Berlin returned — API should handle unicode characters gracefully
- **Actual:** 200 OK — Berlin match returned correctly
- **Severity:** N/A
- **Impact:** No bug — this is correct behaviour. The API handles unicode input well which is important for international travellers searching in their native language. Marked as passed.

---

## BUG-005
- **Title:** Invalid station ID returns error without clear message
- **Steps to reproduce:** Send GET https://v6.db.transport.rest/stops/9999999/departures
- **Expected:** 404 Not Found with clear message explaining station does not exist
- **Actual:** Error returned but response does not clearly communicate that the station ID is invalid
- **Severity:** High
- **Impact:** If a transport operator sends an incorrect station ID, the error response needs to be clear enough for developers to debug quickly. An unclear error on a departure endpoint could delay fixing integration issues and affect real traveller journeys

---

## BUG-006
- **Title:** Past date query returns incorrect error response
- **Steps to reproduce:** Send GET https://v6.db.transport.rest/stops/8011160/departures?when=2020-01-01
- **Expected:** 400 Bad Request with clear message explaining past dates are not valid for departure queries
- **Actual:** Error returned but message does not clearly explain that past dates are invalid
- **Severity:** High
- **Impact:** Retailers querying departures with an accidental past date should receive a clear actionable error. An unclear response makes it harder to build reliable integrations — a booking platform could silently fail to show results without understanding why

---

## Summary

| Bug ID | Title | Severity | Status |
|--------|-------|----------|--------|
| BUG-001 | Empty query returns unhelpful error | Medium | Open |
| BUG-002 | Nonsense string returns city match | Medium | Open |
| BUG-003 | Special characters return city match | Medium | Open |
| BUG-004 | Unicode query returns correct match | N/A | Passed |
| BUG-005 | Invalid station ID unclear error | High | Open |
| BUG-006 | Past date returns unclear error | High | Open |
