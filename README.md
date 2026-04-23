# Distribusion QA Practice

## Overview
A QA test suite built using the Deutsche Bahn public transport API 
(https://v6.db.transport.rest) as part of interview preparation for 
a QA Analyst role at Distribusion Technologies.

Distribusion is a B2B travel marketplace connecting transport operators 
like Deutsche Bahn with retailers like Google Maps and Booking.com. 
This project simulates the kind of API testing a QA Analyst would 
perform on their platform.

## API Tested
**Deutsche Bahn REST API** — https://v6.db.transport.rest  
A public transport API providing real train departure and location data.

## Test Coverage

### 1. Location Search
| Test | URL | Type |
|------|-----|------|
| Valid city search | /locations?query=Berlin | Happy path |
| Invalid city search | /locations?query=zzzzzzz | Negative |
| Empty query string | /locations?query= | Negative |
| Special characters | /locations?query=!@#$%^ | Edge case |
| Unicode characters | /locations?query=Berlín | Edge case |

### 2. Departures
| Test | URL | Type |
|------|-----|------|
| Valid station ID | /stops/8011160/departures | Happy path |
| Invalid station ID | /stops/9999999/departures | Negative |
| Past date | /stops/8011160/departures?when=2020-01-01 | Edge case |
| Future date | /stops/8011160/departures?when=2026-12-01 | Edge case |

## Key QA Concepts Demonstrated
- Happy path testing
- Negative testing
- Edge case testing
- Data validation — checking for null values, correct data types, required fields
- Formal bug reporting with severity ratings
- End to end thinking about how transport data flows through an API platform

## How to Use This Collection
1. Download and install Postman (postman.com/downloads)
2. In Postman click **Import**
3. Select the `.json` file from this repository
4. The full collection appears in your Postman sidebar
5. Run requests folder by folder
