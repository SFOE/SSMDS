# Specification
This document explains the SwissSharedMobility data exchange standard.

* [Introduction](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#introduction)
* [Overview](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#overview)
* [Services](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#services)
	* [SwissSharedMobilityPushSystem](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swissSharedMobilityPushSystem)
	* [SwissSharedMobilityPushStations](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swissSharedMobilityPushStations)
	* [SwissSharedMobilityPushVehicles](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swissSharedMobilityPushVehicles)
* [Messages](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#messaged)
	* [SwissSharedMobilityAcknowledgement](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#SwissSharedMobilityAcknowledgement)
* [Data types](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#datatypes)
	* [actionType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#actiontype)
	* [station](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#station)
	* [status](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#status)
	* [vehicle](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#vehicle)
* [Open questions](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#openquestions)


## Introduction
The SwissSharedMobility standard is a data exchange standard for shared mobility assets and aims to describe static and real-time data (such as availability or position) for all kinds of shared mobilities such as bikes, cars or scooters. It consists of different individual services. Therefore operators can introduce the data exchange standard in stages. The SwissSharedMobility standard is based on the ["General Bikeshare Feed Specification (GBFS)"](https://github.com/NABSA/gbfs/blob/master/README.md) which was designed by the "North American Bikeshare Association".

## Overview

A sharing **system** is identified by a unique system_id and described with information about the operator.

A **station** is a place described by coordinates where vehicles are positioned. Every station belongs to a sharing system.

A **vehicle** is a shared mobility asset such as a bike. When its not used it belongs to a station. Every vehicle belongs to a station.


![alt text](https://github.com/SFOE/SwissSharedMobility/blob/master/images/swisssharedmobility_overview.png)

To address the data exchange based on the defined entities, the following services are established:

Mandatory:
 * [SwissSharedMobilityPushSystem](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushsystem)
 * [SwissSharedMobilityPushStations](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushstation)
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

SwissSharedMobilityPushSystem is a message that is sent in order to upload system data.

| Name  | Data Type | M/O | Description |
| ------------- | ------------- | ------------- |--- |
| actionType | [actionType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#actiontype) | M | The action that has to be performed with the provided data. |
| system_id  | String | M |  ID field - identifier for this sharing system. This should be globally unique (even between different systems) and it is currently up to the operator to guarantee uniqueness. In addition, this value is intended to remain the same over the life of the system. | 
| language | String | M | An IETF language tag indicating the language that will be used throughout the rest of the files. This is a string that defines a single language tag only. | 
| name  | String | M  |  	Full name of the system to be displayed to customers. | 
| operator | String | O | Name of the operator of the system. |
| url | URI | O | The URL of the sharing system. The value must be a fully qualified URL that includes http:// or https://, and any special characters in the URL must be correctly escaped. |
| email | String | O | A single contact email address for customers to address questions about the system. |

 **Example in JSON**
 
 ```json
{
		"actionType" : "fullLoad",
		"system_id" : "nextbike_ch",
		"language" : "de",
		"name" : "nextbike Switzerland",
		"operator" : "nextbike GmbH, Erich-Zeigner Allee 69-73, 04229 Leipzig, German",
		"url" : "https://www.nextbike.ch/xx/sursee/",
		"email" : "info@nextbike.ch"
}
```
  
 You will find an example in geoJSON [here](https://github.com/SFOE/SwissSharedMobility/blob/master/Json/SwissSharedMobilityPushSystem.json).
  
 
  
### SwissSharedMobilityPushStations

SwissSharedMobilityPushStations is a message that is sent in order to upload data about the stations.

| Name  | Data Type | M/O | Description |
| ------------- | ------------- | ------------- | --- |
| actionType | [actionType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#actiontype) | M | The action that has to be performed with the provided data. |
| fk_system_id | String | M | Foreign key of the sharing system as defined in [SwissSharedMobilityPushSystem](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushsystem).
| stations | [station](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#station) | M | Array that contains one object per station. See below for definition of data type station. |

 
**Example in JSON**
  
 ```json
{
	"actionType" : "fullLoad",
	"fk_system_id" : "nextbike_ch",
	"stations" : {
		"station_id" : "46",
		"name" : "BE346633",
		"latitude" : "46.960044",
		"longitude" : "7.458879",
		"adress" : "Schärerstrasse 23",
		"place" : "Bern",
		"postcode" : "3014",
		"station_status" : "open"
	}
}
```
 
 You will find an example in geoJSON [here](https://github.com/SFOE/SwissSharedMobility/blob/master/Json/SwissSharedMobilityPushStation.json).
 

 
 
 ### SwissSharedMobilityPushVehicles
 
 SwissSharedMobilityPushVehicles is a message that is sent in order to upload data about the vehicles.
 
 | Name  | Data Type | M/O | Description |
| ------------- | ------------- | ------------- | --- |
| actionType | [actionType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#actiontype) | M | The action that has to be performed with the provided data. |
| fk_station_id | String | M | Foreign key of the station as defined in [SwissSharedMobilityPushSystem](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushsystem).
| vehicles | [vehicle](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#vehicle) | M | Array that contains one object per station. See below for definition of data type station. |


**Example in JSON**
 
  ```json
{
	"actionType" : "fullLoad",
	"fk_station_id" : "nextbike_ch",
	"vehicles" : {
		"station_id" : "395",
		"vehicle_id" : "615",
		"vehicle_type" : "Bike",
		"charging_status" : ""
	}
}
```
 
 You will find an example [here](
https://github.com/SFOE/SwissSharedMobility/blob/master/Json/SwissSharedMobilityPushVehicles.json).

## Messages

### SwissSharedMobilityAcknowledgement

| Name  | Data Type | M/O | Description |
| ------------- | ------------- | ------------- | --- |
| result | Boolean | M | True if the message was received and processed successfully. False if not. |

## Data types

### actionType

| Option | Description |
| ------------- | ------------- |
| fullLoad |  |
| update |  |
| insert |  |
| delete |  |

### station

| Name  | Data Type | M/O | Description |
| ------------- | ------------- | ------------- | --- |
| station_id | String | M | Unique identifier of a station. |
| name | String | O | Public name of the station. |
| latitude | Float | M | The latitude of station. The field value must be a valid WGS 84 latitude in decimal degrees format. For example: 46.94648 |
| longitude | Float | M | The longitude of station. The field value must be a valid WGS 84 longitude in decimal degrees format. For example: 7.44426 |
| address | String | M | Valid street and street number where station is located. |
| place | String | M | Name of the village/town where station is located. |
| postcode | Integer | M | Postal code where station is located. |
| station_status | [status](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#status) | M | Indicates the status of the station. |
| vehicle_number | Integer | M | Amount of available vehicles. |

### status

| Option | Description |
| ------------- | ------------- |
| Available |  |
| Reserved |  |
| Occupied |  |
| OutOfService |  |
| NotFound |  |
| Unknown |  |


### vehicle

| Name  | Data Type | M/O | Description |
| ------------- | ------------- | ------------- | --- |
| vehicle_id | String | M | Unique vehicle id. Is defined by the provider|
| vehicle_status | [status](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#status) | M | Indicates the state of a vehicle. |
| vehicle_type | String | M | Indicates the vehicle type. Vehicle types are predefined in a catalogue. |
| charging_status | String | O | e-vehicles have to indicate the charging status of the battery. |

## Open questions
Please refer to [Issues](https://github.com/SFOE/SwissSharedMobility/issues) for ongoing discussions and open questions.
