# Specification
This document explains the SwissSharedMobility data exchange standard.

## Introduction
The SwissSharedMobility standard is a data exchange standard for shared mobility assets and aims to describe static and real-time data (such as availability or position) for all kinds of shared mobilities such as bikes, cars or scooters. It consists of different individual services. Therefore operators can introduce the data exchange standard in stages. The SwissSharedMobility standard is based on the ["General Bikeshare Feed Specification (GBFS)"](https://github.com/NABSA/gbfs/blob/master/README.md) which was designed by the "North American Bikeshare Association".

## Overview

A sharing **system** operator is identified by a unique system_id and described by at least a name and a language.

A **station** is a place described by coordinates where vehicles are positioned. Every station belongs to a sharing system.

A **vehicle** is a shared mobility asset such as a bike. When its not used it belongs to a station. Every vehicle belongs to a sharing system.


![alt text](https://github.com/SFOE/SwissSharedMobility/blob/master/images/SwissSharedMobility_overview.png)

To address to data exchange based on the defined entities, the following services are established:

Mandatory:
 * [SwissSharedMobilityPushSystem](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushsystem)
 * [SwissSharedMobilityPushStation](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushstation)
 * [SwissSharedMobilityPushVehicles](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushvehicles)

Optional:
* SwissSharedMobilityPushHours (not available yet)
* SwissSharedMobilityPushCalendar (not available yet)
* SwissSharedMobilityPushRegions (not available yet)
* SwissSharedMobilityPushPricing (not available yet)
* SwissSharedMobilityPushAlerts (not available yet)
* to be extended

## Services

### SwissSharedMobilityPushSystem
Describes the system and the metainformation of the system.

| Field Name  | Required | Defines|
| ------------- | ------------- | --- |
| system_id  | yes |  ID field - identifier for this sharing system. This should be globally unique (even between different systems) and it is currently up to the publisher of the feed to guarantee uniqueness. In addition, this value is intended to remain the same over the life of the system. | 
| language |  yes | An IETF language tag indicating the language that will be used throughout the rest of the files. This is a string that defines a single language tag only. | 
| name  | yes  |  	Full name of the system to be displayed to customers. | 
| operator |  optional | Name of the operator of the system. |
| url | optional | The URL of the sharing system. The value must be a fully qualified URL that includes http:// or https://, and any special characters in the URL must be correctly escaped. |
| email | optional | A single contact email address for customers o address questions about the system. |

**Attributes not used from GBFS-Standard**
 * short_name
 * purchase_url
 * start_date
 * phone_number
 * timezone
 * license_url
 
 **Example**
 
 ```json
{
	"system_id": "SMIDE",
	"station_id": "46",
	"name": "BE346633",
	"latitude": "46.960044",
	"longitude": "7.458879",
	"adress": "Schärerstrasse 23",
	"place": "Bern",
	"postcode": "3014",
	"station_status": "open"
}
```
  
 You will find an example [here](https://github.com/SFOE/SwissSharedMobility/blob/master/Json/SwissSharedMobilityPushSystem.json).
 

 
### SwissSharedMobilityPushStation
Describes the "station" where a vehicle can be rented.


| Field Name  | Required | Defines|
| ------------- | ------------- | --- |
| stations | yes | Array that contains one object per station in the system as defined below. |
| -system_id | yes | Identifier of the sharing system. system_id is defined in [SwissSharedMobilityPushSystem](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushsystem).
| -station_id | yes | Unique identifier of a station. |
| -name | optional | Public name of the station. |
| -latitude | yes | The latitude of station. The field value must be a valid WGS 84 latitude in decimal degrees format. |
| -longitude | yes | The longitude of station. The field value must be a valid WGS 84 longitude in decimal degrees format. |
| -address | yes | Valid street and street number where station is located. |
| -place | yes | Name of the village/town where station is located. |
| -postcode | yes | Postal code where station is located. |
| -station_status | yes | Indicates the status of the station. The following characteristics are possible: open, closed, out of service, unknown |
| - vehicle_number | yes | Amount of available vehicles. |



**Attributes not used from GBFS-Standard**
 * short_name
 * cross_street
 * region_id
 * rental_methods
 * capacity
 
 **Additional attributes**
 * system_id
 * place
 
  
 **Example**
 You will find an example [here](https://github.com/SFOE/SwissSharedMobility/blob/master/Json/SwissSharedMobilityPushStation.json).
 
 
 **Open questions:**
 * Shall url for direct booking of vehicle be on station level or vehicle level?
 * How can the available vehicle number be displayed for stations with more than one vehicle type?
 * Do the attributes "address", "place" and "post_code" need to be mandatory? There is no such information for Nextbike vehicles. Information can be derived using swisstopo-API.
 
 
 ### SwissSharedMobilityPushVehicles
Describes the vehicles that can be rented.
 
| Field Name  | Required | Defines|
| ------------- | ------------- | --- |
| station_id | yes | Identifier of the station where the vehicle is situated. station_id is defined in [SwissSharedMobilityPushStation](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushstation).
| vehicle_id | yes | Unique vehicle id. Is defined by the provider|
| vehicle_status | yes | Indicates the state of a vehicle. The following characteristics are possible: active, inactive, unknown. |
| vehicle_type | yes | Indicates the vehicle type. Vehicle types are predefined in a catalogue. |
| charging_status | optional | e-vehicles have to indicate the charging status of the battery. |


 **Example**
 You will find an example [here](
https://github.com/SFOE/SwissSharedMobility/blob/master/Json/SwissSharedMobilityPushVehicles.json).


**Open questions:**
* FreeFloat-Vehicles change coordinates with every change whereas stations have fix coordinates. station-bases vehicles do not need coordinates whereas freefloat vehicles need coordinates to be defined on "PushVehicles"
* Nextbike does not have information for every single vehicle. A vehicle_id can be derived from the station_id by artifically adding a number at the end:
station_id: 345 --> vehicle_ids: 345-1, 345-2, 345-3... This will cause the problem that vehicles will change the vehicle_id
