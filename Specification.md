# Specification
This document explains the SwissSharedMobility data exchange standard.

## Introduction
The SwissSharedMobility standard is an open data standard for Shared Mobility. The data standard aims to describe real-time data for all kind of Shared Mobilities such as bike sharing, car sharing or scooter sharing.
The suggested data standard is based on the ["General Bikeshare Feed Specification"](https://github.com/NABSA/gbfs/blob/master/README.md) which was designed by the "North American Bikeshar Association".

The SwissSharedMobility standard is constructed modularly. Therefore operators can introduce the data standard in stages. The following modules are available:

Mandatory
 * [SwissSharedMobilityPushSystem](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushsystem)
 * [SwissSharedMobilityPushStation](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushstation)
 * [SwissSharedMobilityPushStatus](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushstatus)

Optional
* SwissSharedMobilityPushHours
* SwissSharedMobilityPushCalendar
* SwissSharedMobilityPushRegions
* SwissSharedMobilityPushPricing
* SwissSharedMobilityPushAlerts

### SwissSharedMobilityPushSystem
Describes the system and the metainformation of the system.

| Field Name  | Required | Defines|
| ------------- | ------------- | --- |
| system_id  | yes |  ID field - identifier for this bike share system. This should be globally unique (even between different systems) and it is currently up to the publisher of the feed to guarantee uniqueness. In addition, this value is intended to remain the same over the life of the system. | 
| language |  yes | An IETF language tag indicating the language that will be used throughout the rest of the files. This is a string that defines a single language tag only. | 
| name  | yes  |  	Full name of the system to be displayed to customers. | 
| operator |  optional | Name of the operator of the system. |
| url | optional | The URL of the bike share system. The value must be a fully qualified URL that includes http:// or https://, and any special characters in the URL must be correctly escaped. |
| email | optional | A single contact email address for customers o address questions about the system. |

**Attributes not used from GBFS-Standard**
 * short_name
 * purchase_url
 * start_date
 * phone_number
 * timezone
 * license_url


### SwissSharedMobilityPushStation
Describes the "station" where a vehicle can be rented.


| Field Name  | Required | Defines|
| ------------- | ------------- | --- |
| stations | yes | Array that contains one object per station in the system as defined below. |
| -station_id | yes | Unique identifier of a station. |
| -name | optional | Public name of the station. |
| -latitude | yes | The latitude of station. The field value must be a valid WGS 84 latitude in decimal degrees format. |
| -longitude | yes | The longitude of station. The field value must be a valid WGS 84 longitude in decimal degrees format. |
| -address | yes | Valid street number and name where station is located. |
| -post_code | yes | Postal code where station is located. |
| -station_status | yes | Indicates the status of the station. station_status will be derived from [SwissSharedMobilityPushStatus](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushstatus). The following characteristics are possible: open, closed, out of service, unknown |
| - vehicle_number | yes | Amount of available vehicles. |



**Attributes not used from GBFS-Standard**
 * short_name
 * cross_street
 * region_id
 * rental_methods
 * capacity
 
 **Open questions:**
 * Shall url for direct booking of vehicle be on station level or vehicle level?
 * How can the available vehicle number be displayed for stations with more than one vehicle type?
 
 
 ### SwissSharedMobilityPushStatus
Describes the "station" where a vehicle can be rented.
 
 
 

