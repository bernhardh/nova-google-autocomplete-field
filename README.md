## Nova Google AutoComplete Field Package

This field allows you to work with Google Places API to autocomplete on user input and get the full real address with all the metadata (like latitude and longitude).

## Installation

You can install the package in to a Laravel app that uses Nova via composer:

```bash
composer require emilianotisato/nova-google-autocomplete-field
```

Add the below to /resources/views/vendor/nova/layout.blade.php (this you can copy from the nova repository to override the original)
* To get resualts in specific language add `&language=en` to the below script url

```php
<script src="https://maps.googleapis.com/maps/api/js?key={{env('ADDRESS_AUTOCOMPLETE_API_KEY')}}&libraries=places"></script>
             
```

Add the below to your `.env` file

Create an app and enable Places API and create credentials to get your API key
https://console.developers.google.com

```shell
ADDRESS_AUTOCOMPLETE_API_KEY=############################
```

## Usage:
Add the use decalaration to your resource and use the fields:

```php
use EmilianoTisato\GoogleAutocomplete\GoogleAutocomplete;
// ....

GoogleAutocomplete::make('Address'),

//You can add a country or countries to autocomplete or leave empty for all.
          
// Specify a single country
AddressAutocomplete::make('Address')
          ->countries('US'),
                
// Specify multiple countries [array]
AddressAutocomplete::make('Address')
          ->countries(['US','AU]),
```

You can access other parameter like `latitude, longitude, street_number, route, locality, administrative_area_level_1, country, postal_code` and whatever is available by de Places API with the available AddressMetadata field:

```php
use EmilianoTisato\GoogleAutocomplete\AddressMetadata;
use EmilianoTisato\GoogleAutocomplete\GoogleAutocomplete;

// Now this address field will search and store the address as a string, but also made available the values in the withValues array
GoogleAutocomplete::make('Address')->withValues(['latitude', 'longitude']),

// And you can store the values by autocomplete like this
AddressMetadata::make('lat')->fromValue('latitude'),
AddressMetadata::make('long')->fromValue('longitude'),

// You can disable the field so the user can't edit the metadata
AddressMetadata::make('long')->fromValue('longitude')->disabled(),

// Or you can make the field invisible in the form but collect the data anyways
AddressMetadata::make('long')->fromValue('longitude')->invisible(),
```
