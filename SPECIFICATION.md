# Amadeus SDK Specification Document

[Table of Content](#table-of-content) | [Templates](./templates)

![Status](https://img.shields.io/badge/version-1.0-brightgreen.svg)

## Overview

The goal of this document is to set a shared standard for implementation and development of all Amadeus SDKs. For the sake of this document, there is no differentiation between SDKs and API client SDKs.

This document is a work in progress, and should be changed and updated as changes are made to the APIs or developer needs are discovered.

### Requirement Prioritization

The following document follows the [MoSCoW](https://en.wikipedia.org/wiki/MoSCoW_method) method of prioritising rules. Please follow the following guidelines when evaluating rules.

* `MUST` - Rules labeled as __must__ are requirements that should not be deviated from at any cost
* `SHOULD` - Rules labeled as __should__ are requirements that could be deviated from if needed, though this will have to be documented and cleared with all stakeholders before it can be disregarded.
* `COULD` - Rules labeled as __could__ are requirements that are desirable but not necessary and therefore would be nice to have where time and resources permit.

We do not use the fourth __`won't`__ level in this specification.

## Limitations

Currently this specification is limited due to various reasons. This means that currently:

* This specification mostly focusses on read-only API methods
* This specification assumes a language that has objects, or object-like features
* This specification does not assume the SDK is automatically generated

## Table of Contents

* Maintenance Requirements
    * [1. Source Control](#1-source-control)
    * [2. Releases & Versioning](#2-releases--versioning)
    * [3. CI Server](#3-ci-server)
* Additional Content Requirements
    * [4. Documentation](#4-documentation)
    * [5. Testing](#5-testing)
    * [6. Linting](#6-linting)
* Dependencies & Infrastructure Requirements
    * [7. Dependencies](#7-dependencies)
    * [8. HTTP Client](#8-http-client)
    * [9. Logging](#9-logging)
    * [10. Reporting](#10-reporting)
* Initialization & Interaction Requirements
    * [11. Initialization](#11-initalization)
    * [12. Namespacing](#12-namespacing)
    * [13. Method Syntax](#13-method-syntax)
    * [14. Error Handling](#14-error-handling)
* API Mapping Requirements
    * [15. API Calls](#15-api-calls)
    * [16. Entities](#16-entities)
* Specific Language Requirements
    * [17. Ruby](#17-ruby)
    * [18. Node / Javascript](#18-node--javascript)
    * [19. Python](#19-python)
    * [20. Java](#20-java)

## Maintenance Requirements

### 1. Source Control

- [ ] __1.1__ The source code for the SDK __must__ be maintained within Git version control
- [ ] __1.2__ Development of new features __should__ happen on feature branches
- [ ] __1.3__ Feature branches __should__ pass all tests and linting before they can be merged into the `master` branch
- [ ] __1.4__ Source control __should__ contain tags for each release of the SDK
- [ ] __1.5__ The `master` branch __should__ be kept in a condition that allows for direct use through checkout
- [ ] __1.6__ The source code __must__ be hosted publicly
- [ ] __1.7__ The source code __should__ use GitHub for public hosting
- [ ] __1.8__ The source code __should__ not include build packages, compiled assets, or any other intermediary files used to package the source code into a release

### 2. Releases & Versioning

- [ ] __2.1__ The SDK __must__ use [Semantic Versioning](http://semver.org/) to increment the version number as changes are made
- [ ] __2.2__ The version number of the SDK __could__ be incremented when the SDK has gathered enough changes to warrant a new release
- [ ] __2.3__ For every release a tag __must__ created within Git
- [ ] __2.4__ New releases __should__ be deployed automatically to the package manager using the CI server
- [ ] __2.5__ For every new release the `CHANGELOG` file __must__ to be updated with the `Major`, `Minor` and `Patch` changes
- [ ] __2.6__ Releases __must__ be pushed to package managers as an __Amadeus__ user not exclusively under any personal accounts
- [ ] __2.7__ The version number of the SDK __should__ be independent of the API version
- [ ] __2.8__ A release package __should__ not include unnecessary source code files or intermediarry files for the SDK.
- [ ] __2.9__ A release package __must__ include the documentation `README` file
- [ ] __2.10__ A release package __must__ include the `LICENSE` file
- [ ] __2.11__ A release package __should__ include the `CHANGELOG` file
- [ ] __2.12__ The name of the SDK __should__ follow language best practices, and be one of `amadeus`, `Amadeus`, or `amadeus/amadeus`.
- [ ] __2.13__ If the preferred name of the SDK is not available, it __could__ be one of `amadeus-sdk`, `AmadeusSDK`, or `amadeusdev/amadeus`.
- [ ] __2.14__ The name of the SDK __must__ exclude the programming language (e.g. __not__ `amadeus-php`) or a reference to this being an SDK client library (e.g. __not__ `amadeus-sdk`)
practices, and be one of `amadeus`, `Amadeus`, or `amadeus/amadeus`.
- [ ] __2.15__ As soon as the first public version of the library has been signed off, the version __should__ be bumped to `1.0.0`


### 3. CI Server

- [ ] __3.1__ A Continuous Integration (CI) server __must__ be used to automatically test any branch of the Git repository
- [ ] __3.2__ The CI server __should__ be [Travis CI](https://travis-ci.org/).
- [ ] __3.3__ The CI server __must__ test against all current LTS language versions
- [ ] __3.4__ The CI server __could__ test against popular non-LTS versions
- [ ] __3.5__ The CI server __could__ test on different platforms, including Windows, Linux, and macOS.
- [ ] __3.6__ The CI server __should__ test new Git tags, and build and push the package to the package manager

## Additional Content Requirements

### 4. Documentation

- [ ] __4.1__ The SDKs __must__ include a `README` file
    - [ ] __4.1.1__ The `README` file __should__ include a version badge
    - [ ] __4.1.2__ The `README` file __should__ include a test status badge
    - [ ] __4.1.3__ The `README` file __must__ link to the `LICENSE` file
    - [ ] __4.1.4__ The `README` file __should__ be written in Markdown
    - [ ] __4.1.5__ The `README` file __must__ have instructions on how to install the SDK using a package manager
    - [ ] __4.1.6__ The `README` file __could__ have instructions on how to install the SDK from version control
    - [ ] __4.1.7__ The `README` file __must__ have instructions on how to initialise the SDK with the API credentials
        - [ ] __4.1.7.1__ Where possible, the initialised client variable __should__ be named `amadeus`. For example, `amadeus = new Amadeus::Client()`
    - [ ] __4.1.8__ The `README` file __should__ document all the different ways the SDK can be initialized
    - [ ] __4.1.9__ The `README` file __must__ include a basic sample on how to make a first API call
    - [ ] __4.1.10__ The `README` file __must__ link to the developer portal
    - [ ] __4.1.11__ The `README` file __should__ link to documentation on the developer portal
    - [ ] __4.1.12__ The `README` file __must__ document any installation requirements and prerequisites
    - [ ] __4.1.13__ The `README` file __should__ to official support channels
    - [ ] __4.1.14__ The `README` file __must__ document where a developer can find their API credentials
- [ ] __4.2__ The SDKs __should__ have its public methods documented in a way that allows for autogenerated method documentation. For example, for Ruby this would be [yard](https://yardoc.org/) and for Java this would be using Javadoc.
- [ ] __4.3__ The SDKs __could__ use the CI server or any other build tool to autogenerate the method documentation on deploy
- [ ] __4.4__ The GitHub repository __should__ have a title in the format "Ruby library for the Amadeus travel APIs"
- [ ] __4.5__ The GitHub repository __should__ have the following tags: `amadeus`, `travel`, `flights`, `hotels`, `sdk`, `library`
- [ ] __4.6__ The SDKs __must__ include a `CHANGELOG` file
- [ ] __4.7__ The SDKs __must__ include a `CODE_OF_CONDUCT` file
- [ ] __4.8__ The SDKs __must__ include a `CONTRIBUTING` file
    - [ ] __4.8.1__ The Contribution Guidelines __should__ include instructions on how to run the SDK in development/testing mode.
- [ ] __4.9__ The SDKs __must__ include a `ISSUE_TEMPLATE` file
- [ ] __4.10__ The SDKs __must__ include a `PULL_REQUEST_TEMPLATE` file
- [ ] __4.11__ The SDKs __must__ include a `SUPPORT` file

> Templates for a lot of these files have been provided in the [templates](./templates) folder

### 5. Testing

- [ ] __5.1__ The SDKs __must__ be thoroughly tested
- [ ] __5.2__ The tests __should__ have integration tests to make the API calls
- [ ] __5.3__ The tests __should__ test response objects
- [ ] __5.4__ The tests __must__ not actually make any HTTP calls to the API in testing and instead use some kind of VCR method
- [ ] __5.5__ The tests __must__ not include actual API credentials

### 6. Linting

- [ ] __6.1__ The SDKs __must__ have their files linted
- [ ] __6.2__ The linting __must__ ensure that tabs/spaces are consistently used
- [ ] __6.3__ The linting __should__ ensure no trailing whitespace is left in the code
- [ ] __6.4__ The linting __should__ ensure quotes and brackets are consistently applied
- [ ] __6.5__ The linting __could__ ensure semicolons are present when needed
- [ ] __6.6__ The linting __could__ ensure comments are present on public methods

## Dependencies & Infrastructure Requirements

### 7. Dependencies

- [ ] __7.1__ The SDK __must__ limit its runtime dependencies
- [ ] __7.2__ The SDK __should__ have no runtime dependencies
- [ ] __7.3__ The SDK __could__ use any amount of development and test dependencies

### 8. HTTP Client

- [ ] __8.1__ The SDK __must__ use a well supported HTTP client
- [ ] __8.2__ A HTTP client from the standard libraries __should__ be used
- [ ] __8.3__ The HTTP __should__ support proxies
- [ ] __8.4__ The SDK __could__ allow a developer to provide an alternative HTTP client

### 9. Logging

- [ ] __9.1__ The SDK __must__ be able to log activities to a logger
- [ ] __9.2__ The logger __should__ use the default runtime log
- [ ] __9.3__ The logger __must__ allow being turned on/off per SDK client
- [ ] __9.4__ The logger __could__ allow for different verbosity levels per SDK client
- [ ] __9.5__ The logger __should__ allow a developer to provide an alternative logger

### 10. Reporting

- [ ] __10.1__ The SDK __must__ identify requests to the API as originating from the SDK
- [ ] __10.2__ The SDK __must__ report the SDK version number to the API
- [ ] __10.3__ The SDK __should__ report the language version number to the API
- [ ] __10.4__ The HTTP client __should__ use the following format user agent to identify the library:
    - Specification: `library_name/library_version language_name/language_version`
    - Example with known language version: `amadeus-ruby/1.0.0 ruby/2.4.2`
    - Example with unknwon language version: `amadeus-ruby/1.0.0 -`
- [ ] __10.5__ The SDK __should__ allow a developer to provide an additional __custom app id__ and __custom app version__ to be passed along in the user agent.
    - Specification: `library_name/library_version language_name/language_version app_name/app_version`
    - Example: `amadeus-ruby/1.0.0 ruby/2.4.2 test_ios_app/1.0.0`

## Initialization & Interaction Requirements

### 11. Initialization

- [ ] __11.1__ The SDK __could__ be included or imported when needed, and where applicable __must__ use the `amadeus`, `com.amadeus.developer`, or `Amadeus` package name
- [ ] __11.2__ The SDK __should__ reside in its own namespace and avoid polluting the global namespace
- [ ] __11.3__ The actual client object for the SDK __should__ exist as a subclass within the Amadeus namespace where the language allows. For for example `Amadeus::Client` in Ruby, or `Amadeus\Client` in PHP
- [ ] __11.4__ The SDK client __must__ allow for the creation of multiple clients per runtime environment, allowing the creation of multiple clients with different credentials
- [ ] __11.5__ The SDK client __must__ be able to accept SDK credentials as method parameters
- [ ] __11.6__ The SDK client __should__ accept the SDK credentials implicitly as environment variables `AMADEUS_CLIENT_ID` and `AMADEUS_CLIENT_SECRET`
- [ ] __11.7__ The SDK client __must__ accept a parameter to turn set the logger level
- [ ] __11.8__ The SDK client __should__ be able to implicitly accept the debug level as environment variable `AMADEUS_LOG_LEVEL`
- [ ] __11.9__ The SDK client __should__ be able to accept an alternative logger object
- [ ] __11.10__ The SDK client __could__ accept an alternative HTTP client
- [ ] __11.11__ The SDK client __must__ allow selection of the base URL by name (`test` and `production`)
- [ ] __11.12__ The SDK client __must__ allow for setting a custom base URL directly

### 12. Namespacing

- [ ] __12.1__ The SDK __should__ use namespaced methods to create a match between the API and the SDK
    - `GET /v1/flights` : `amadeus.flights.get`
    - `GET /v2/hotels/offers`: `amadeus.hotels.offers.get`
- [ ] __12.2__ The SDK __could__ use resource IDs as parameters to the namespace, or as a name or unnamed parameter to the call used to execute the API call
    - `GET /v1/hotels/123` : `amadeus.hotels(123)`
    - `GET /v1/hotels/123` : `amadeus.hotels.get(123)`
    - `GET /v1/hotels/123` : `amadeus.hotels.get(id: 123)`
- [ ] __12.3__ The SDK __should__ limit API calls when selecting sub resources. All of these should make 1 API call only
    - `GET /v1/hotels/123/hotel-offers` : `amadeus.hotels(123).offers`
    - `GET /v1/hotels/123/hotel-offers` : `amadeus.hotels.get(123).offers`
    - `GET /v1/hotels/123/hotel-offers` : `amadeus.hotels.get(id: 123).offers`
- [ ] __12.4__ The SDK __could__ drop the HTTP verb methods where lazy loading is possible
    - `GET /v1/flights/123/legs` : `amadeus.flights(123).legs()` (should make 1 API call only)
    - `GET /v1/flights/123/legs/345` : `amadeus.flights(123).legs(345)` (should make 1 API call only)
- [ ] __12.5-__ The SDK __could__ convert the API namespace (e.g. `reference-data`) to a more idiomatic format (e.g. `reference_data` or `ReferenceData`)

### 13. Method Syntax

- [ ] __13.1__ The SDK API calls __should__ allow for a method to fetch all records for a resource with or without any parameters
    - Example: `amadeus.flights().get()` : `GET /v1/flights`
    - Example: `amadeus.flights().get({ foo: 123 }` : `GET /v1/flights?foo=123`
- [ ] __13.2__ The SDK API calls __should__ allow for a method to take a record ID to fetch a specific resource
    - Example: `amadeus.flights(123).get()` : `GET /v1/flights/123`
- [ ] __13.3__ When making a POST or PUT request, the SDK API calls __should__ accept a key/value data structure for the data to be submitted
    - Example: `amadeus.flights().post({ from: "LHR", to: "LAX" })`
- [ ] __13.4__ In asynchronous programming languages, the SDK API calls __should__ allow for a callback method as a final parameter
    - Example `amadeus.flights().get(params, callback_function)`
- [ ] __13.5__ The SDK API calls __should__ return objects or other structured data
    - [ ] __13.5.1__ The SDK __must__ parse the JSON returned from the API
    - [ ] __13.5.2__ The SDK __should__ raise an exception if the JSON could not be parsed
    - [ ] __13.5.3__ The SDK __should__ raise an exception if the parsed object is an error object

### 14. Error Handling

- [ ] __14.1__ The SDK __should__ raise an exception for any request that did not result a HTTP 200 or 201 response code
- [ ] __14.2__ The SDK __should__ differentiate between different errors
    - [ ] __14.2.1__ The SDK __should__ raise a specific exception when a transport error occurs (e.g. if the API could not be reached, or unexpected data was returned from the API)
    - [ ] __14.2.2__ The SDK __should__ raise a specific exception when a client error occurs (e.g. bad credentials were used, or incorrect data was sent to the API, basically any 400 error)
    - [ ] __14.2.3__ The SDK __should__ raise a specific exception if a server error occurred
- [ ] __14.3__ The SDK __should__ prefer using native exceptions and errors over returning error objects
- [ ] __14.4__ The SDK __should__ not validate submitted data within the SDK, instead leaving this task to the API and raising exceptions on receiving an error response from the API
- [ ] __14.5__ The SDK __should__ allow the inspection of request and response objects on exception

## API Mapping Requirements

### 15. API Calls

- [ ] __15.1__ The SDK __should__ define the `reference-data` namespace
    - [ ] __15.1.1__ The SDK __must__ implement the [`GET /v2/reference_data/urls/checkin-links`](https://mobile-services.amadeus.com/catalogue/31#learn) endpoint
        - Example: `amadeus.reference_data.urls.checkin_links.get({ airline: 'BA' })`
    - [ ] __15.1.2__ The SDK __must__ implement the [`GET /v2/reference_data/locations`](https://mobile-services.amadeus.com/catalogue/32#learn) endpoint
        - Example: `amadeus.reference_data.locations.get({ keyword: 'LON' })`
    - [ ] __15.1.3__ The SDK __must__ implement the [`GET /v2/reference_data/locations/airports`](https://mobile-services.amadeus.com/catalogue/33#learn) endpoint
        - Example: `amadeus.reference_data.locations.airports.get({ latitude: '0.0', longitude: '0.0' })`
- [ ] __15.2__ The SDK __should__ define the `shopping` namespace
    - [ ] __15.2.1__ The SDK __must__ implement the [`GET /v1/shopping/flight-destinations`](https://mobile-services.amadeus.com/catalogue/35#learn) endpoint
        - Example: `amadeus.shopping.flight_destinations.get({ origin: 'LAX' })`
    - [ ] __15.2.2__ The SDK __must__ implement the [`GET /v1/shopping/flight-offers`](https://mobile-services.amadeus.com/catalogue/36#learn) endpoint
        - Example: `amadeus.shopping.flight_offers.get({ origin: 'LAX', destination: 'LHR', departureDate: '2020-12-01' })`
    - [ ] __15.2.3__ The SDK __must__ implement the [`GET /v1/shopping/flight-dates`](https://mobile-services.amadeus.com/catalogue/37#learn) endpoint
        - Example: `amadeus.shopping.flight_dates.get({ origin: 'LAX', destination: 'LHR' })`
- [ ] __15.3__ The SDK __should__ define the `travel/analytics` namespace
    - [ ] __15.3.1__ The SDK __must__ implement the [`GET /v1/travel/analytics/fare-searches`](https://mobile-services.amadeus.com/catalogue/30#learn) endpoint
        - Example: `amadeus.travel.analytics.fare_searches.get({ origin: 'LAX', sourceCountry: 'US', period: 2015 })`
    - [ ] __15.3.2__ The SDK __must__ implement the [`GET /v1/travel/analytics/air-traffics`](#) endpoint
        - Example: `amadeus.travel.analytics.air_traffics.get({ origin: 'LAX', period: '2015-07' })`
- [ ] __15.4__ The SDK __should__ define the `shopping/hotels` namespace
    - [ ] __15.4.1__ The SDK __must__ implement the [`GET /v1/shopping/hotel-offers`](#) endpoint
        - Example: `amadeus.shopping.hotel_offers.get({ cityCode: 'LAX' }`
    - [ ] __15.4.2__ The SDK __must__ implement the [`GET /v1/shopping/hotels/:hotel_id/hotel-offers`](#) endpoint
        - Example: `amadeus.shopping.hotels.get(123).hotel_offers.get({ checkInDate: '2018-12-01', checkOutDate: '2018-12-03' })`
    - [ ] __15.4.3__ The SDK __must__ implement the [`GET /v1/shopping/hotels/:hotel_id/offers/:offer_id`](#) endpoint
        - Example: `amadeus.shopping.hotels.get(123).hotel_offers.get(345)`

### 16. Responses

- [ ] __16.1__ The SDK __should__ return a response object where possible, instead of the JSON data directly
- [ ] __16.2__ The SDK __should__ include a method to access the raw JSON data
    - Example:  `amadeus.reference_data.urls.checkin_links.get({ airline: '1X' }).json` returns `{ meta: ..., data: [...] }`
- [ ] __16.3__ The SDK __could__ include a method to access the `data` attribute from the returned JSON, if there is any
  - Example:  `amadeus.reference_data.urls.checkin_links.get({ airline: '1X' }).data` returns `[...]`
- [ ] __16.3__ The response objects __should__ allow for easy pagination where needed
    - Example: `response = amadeus.foo.bar(); next_response = result.next();`
- [ ] __16.4__ The response object __could__ allow for access of the returned data as methods on the object
    - Example: `flight_offer = amadeus.get_flight_offers(); first_leg = flight_offer.flight.airline.name;`
- [ ] __16.6__ The response object __should__ be able to deal with any new parameters returned from the API without needing an SDK update. In other words, the class definition of response objects should not define the attributes of the object statically

## Specific Language Requirements

### 17. Ruby

- [ ] __17.1__ The SDK __must__ support Ruby 2.2+
- [ ] __17.2__ The SDK __should__ support JRuby

### 18. Node / Javascript

- [ ] __18.1__ The SDK __should__ promises
- [ ] __18.2__ The SDK __could__ support ES7's `async/await`
- [ ] __18.3__ The SDK __should__ be written in ES6+
- [ ] __18.4__ The SDK __should__ work in an ES5 environment
- [ ] __18.5__ The SDK __should__ support ES6 modules

### 19. Python

- [ ] __19.1__ The SDK __should__ support Python 2 and 3

### 20. Java

- [ ] __20.1__ The SDK __should__ support both the regular JRE, and the Android runtime
