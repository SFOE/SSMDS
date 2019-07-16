# Specification
This document explains the SwissSharedMobility data exchange standard.

## Introduction
The SwissSharedMobility standard is an open data standard for Shared Mobility. The data standard aims to describe real-time data for all kind of Shared Mobilities such as bike sharing, car sharing or scooter sharing.
The suggested data standard is based on the ["General Bikeshare Feed Specification"](https://github.com/NABSA/gbfs/blob/master/README.md) which was designed by the "North American Bikeshare Association".

The SwissSharedMobility standard is constructed modularly. Therefore operators can introduce the data standard in stages. The following modules are available:

Mandatory
 * [SwissSharedMobilityPushSystem](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushsystem)
 * [SwissSharedMobilityPushStation](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushstation)
 * [SwissSharedMobilityPushVehicles](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushvehicles)

Optional
* SwissSharedMobilityPushHours (not available yet)
* SwissSharedMobilityPushCalendar (not available yet)
* SwissSharedMobilityPushRegions (not available yet)
* SwissSharedMobilityPushPricing (not available yet)
* SwissSharedMobilityPushAlerts (not available yet)

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
 
 **Example**
 You will find an example [here](https://github.com/SFOE/SwissSharedMobility/blob/master/Json/SwissSharedMobilityPushSystem.json).
 

 
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
| -station_status | yes | Indicates the status of the station. The following characteristics are possible: open, closed, out of service, unknown |
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
 
 
 ### SwissSharedMobilityPushVehicles
Describes the vehicles that can be rented.
 
| Field Name  | Required | Defines|
| ------------- | ------------- | --- |
| vehicle_id | yes | Unique vehicle id. Is defined by the provider|
| vehicle_status | yes | Indicates the state of a vehicle. The following characteristics are possible: active, inactive, unknown. |
| vehicle_type | yes | Indicates the vehicle type. Vehicle types are predefined in a catalogue. |
| charging_status | optional | e-vehicles have to indicate the charging status of the battery. |
