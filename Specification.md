# Swiss Shared Mobility Data Specification (SSMDS)
This document explains the Swiss Shared Mobility Data Specification (SSMDS).

* [Introduction](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#introduction)
* [Overview](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#overview)
* [Services](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#services)
	* [SwissSharedMobilityPushSystem](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swissSharedMobilityPushSystem)
	* [SwissSharedMobilityPushStations](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swissSharedMobilityPushStations)
	* [SwissSharedMobilityPushVehicles](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swissSharedMobilityPushVehicles)
* [Messages](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#messages)
	* [SwissSharedMobilityAcknowledgement](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#SwissSharedMobilityAcknowledgement)
* [Data types](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#data-types)
	* [acknowledgementType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#acknowledgementType)
	* [actionType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#actiontype)
	* [addressType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#addressType)
	* [station](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#station)
	* [statusType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#statusType)
	* [systemType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#systemType)
	* [vehicle](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#vehicle)
	* [vehicleType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#vehicleType)
* [Best practice](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#best-practice)
* [Open questions](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#openquestions)


## Introduction
The SSMDS is a generic data exchange standard for all kinds of shared mobility assets such as bikes, cars or scooters as well as sharing-systems and aims to describe static and real-time data (such as availability or position).

SSMDS is inspired by the following sources:

| Source  | Scope | Ongoing development |
| --------------------- | ------------- |------------- |
|[General Transit Feed Specification (GTFS)](https://developers.google.com/transit/gtfs/reference/)| Public transportation schedules and associated geographic information. | |
|[General Bikeshare Feed Specification (GBFS)](https://github.com/NABSA/gbfs/blob/master/README.md)| Standardized data feed for bike share system availability. | [Allow vehicle type definitions / generalize to other modes](https://github.com/NABSA/gbfs/pull/136) & [Improvements to GBFS](https://github.com/NABSA/gbfs/issues/137) |
|[Mobility Data Specification (MDS)](https://github.com/CityOfLosAngeles/mobility-data-specification)| Data specifications focused on dockless e-scooters and bicycles. | [Update MDS / MDS-Provider to support multiple modes](https://github.com/CityOfLosAngeles/mobility-data-specification/pull/255) |

Unfortunately, for the time being GBFS and MDS have limited scopes: GBFS only supports bikesharing and MDS only supports dockless e-scooters and bikes. Therefore, we decided to establish a new standard, which is generic and able to support all kinds of shared mobility assets as well as systems.

## Overview

A sharing **system** provides transportation to its customers by means of shared assets (for example bicycles or cars) on an as-needed basis. A sharing system is identified by a unique systemId and described by information about the operator.

A **station** is a physical place containing assets (vehicles) of a specific sharing system. A station is described by coordinates. Every station belongs to a sharing system.

A **vehicle** is a shared mobility asset such as a bike. When its not used it belongs to a station. Every vehicle belongs to a station.


![alt text](https://github.com/SFOE/SwissSharedMobility/blob/master/SSMDS_UML.png)


## Services

To address the data exchange based on the defined entities, the following services are established:

Mandatory:
 * [SwissSharedMobilityPushSystem](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushsystem)
 * [SwissSharedMobilityPushStations](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushstations)
 * [SwissSharedMobilityPushVehicles](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushvehicles)

Optional:
* SwissSharedMobilityPushHours (not yet available)
* SwissSharedMobilityPushCalendar (not yet available)
* SwissSharedMobilityPushRegions (not yet available)
* SwissSharedMobilityPushPricing (not yet available)
* SwissSharedMobilityPushAlerts (not yet available)
* to be extended

### SwissSharedMobilityPushSystem

SwissSharedMobilityPushSystem is a message that is sent in order to upload system data.

| Name  | Data Type | M/O | Description |
| ------------- | ------------- | ------------- |--- |
| actionType | [actionType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#actiontype) | M | The action that has to be performed with the provided data. |
| systemId  | String | M |  Identifier for the sharing system. This should be globally unique (even between different systems) and it is currently up to the operator to guarantee uniqueness. In addition, this value is intended to remain the same over the life of the system. | 
| systemType | [systemType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#systemtype) | M | Type of the system. |
| language | String | M | An IETF language tag indicating the language that will be used throughout the rest of the files. This is a string that defines a single language tag only. | 
| name  | String | M  |  	Full name of the system to be displayed to customers. | 
| operator | String | O | Name of the operator of the system. |
| url | URI | O | The URL of the sharing system. The value must be a fully qualified URL that includes http:// or https://, and any special characters in the URL must be correctly escaped. |
| email | String | O | A single contact email address for customers to address questions about the system. |
| hotline | String | M | Hotline Phone Number. |

 **Example in JSON**
 
 ```json
{
		"actionType" : "fullLoad",
		"systemId" : "nextbike_ch",
		"systemType" : "BikesDocks",
		"language" : "de",
		"name" : "nextbike Switzerland",
		"operator" : "nextbike GmbH, Erich-Zeigner Allee 69-73, 04229 Leipzig, German",
		"url" : "https://www.nextbike.ch/xx/sursee/",
		"email" : "info@nextbike.ch"
}
```
  
 
  
### SwissSharedMobilityPushStations

SwissSharedMobilityPushStations is a message that is sent in order to upload data about the stations.

| Name  | Data Type | M/O | Description |
| ------------- | ------------- | ------------- | --- |
| actionType | [actionType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#actiontype) | M | The action that has to be performed with the provided data. |
| foreignKeySystem | String | M | Foreign key of the sharing system as defined in [SwissSharedMobilityPushSystem](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushsystem).
| stations | List ([station](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#station)) | M | List of stations. Array of Objects. See below for definition of data type station. |

 
**Example in JSON**
  
 ```json
{
	"actionType" : "fullLoad",
	"foreignKeySystem" : "nextbike_ch",
	"stations" : [{
		"stationId" : "46",
		"name" : "BE346633",
		"latitude" : "46.960044",
		"longitude" : "7.458879",
		"address" : {
			"street": "Schärerstrasse",
			"houseNumber": "23",
			"city": "Bern"
		},
		"stationStatus" : "Available"
	},{
		"stationId" : "47",
		"name" : "BE346635",
		"latitude" : "46.85564",
		"longitude" : "7.490025",
		"address" : {
			"street": "Bahnhofstrasse",
			"city": "Bern"
		},
		"stationStatus" : "Available"
	}]
}
```
 
 
 
 ### SwissSharedMobilityPushVehicles
 
 SwissSharedMobilityPushVehicles is a message that is sent in order to upload data about the vehicles.
 
 | Name  | Data Type | M/O | Description |
| ------------- | ------------- | ------------- | --- |
| actionType | [actionType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#actiontype) | M | The action that has to be performed with the provided data. |
| vehicles | List ([vehicle](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#vehicle)) | M | List of vehicles. Array of Objects. See below for definition of data type vehicle. |


**Example in JSON (fullLoad)**
 
  ```json
{
	"actionType" : "fullLoad",
	"vehicles" : [{
		"stationId" : "395",
		"foreignKeyStation" : "46",
		"vehicleId" : "615",
		"vehicleStatus" : "Available",
		"vehicleType" : "Bike"
	},{
		"stationId" : "395",
		"foreignKeyStation" : "46",		
		"vehicleId" : "616",
		"vehicleStatus" : "Available",
		"vehicleType" : "Bike"
	}]
}
```
 
**Example in JSON (update)**
 
  ```json
{
	"actionType" : "update",
	"vehicles" : [{
		"stationId" : "395",
		"foreignKeyStation" : "46",
		"vehicleId" : "615",
		"vehicleStatus" : "Occupied",
		"vehicleType" : "Bike"
	}]
}
``` 

## Messages

### SwissSharedMobilityAcknowledgement

| Name  | Data Type | M/O | Description |
| ------------- | ------------- | ------------- | --- |
| result | [acknowledgementType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#acknowledgementType) | M |  |

## Data types

### acknowledgementType

| Option | Description |
| ------------- | ------------- |
| 000 | Success |
| 901 | Data not compliant with standard |

### actionType

| Option | Description |
| ------------- | ------------- |
| fullLoad | The complete dataset is transmitted. All data will be replaced by the newly transmitted data. |
| update | Only changed entries are transmitted. The changed entries will be updated. |
| insert | Only new entries are transmitted. The new entries will be added to the data. |
| delete | Only to be deleted entries are transmitted. Those entries will be deleted in the data. |

### addressType

| Name  | Data Type | M/O | Description |
| ------------- | ------------- | ------------- | --- |
| city | String | M |  |
| street | String | M |  |
| postalCode | String | O |  |
| houseNumber | String | O |  |

### requirement

| Option | Description |
| ------------- | ------------- |
| No requirements |  |
| Driving licence category A1 |  |
| Helmtragepflicht |  |

### station

| Name  | Data Type | M/O | Description |
| ------------- | ------------- | ------------- | --- |
| stationId | String | M | Unique identifier of a station. |
| name | String | O | Public name of the station. |
| latitude | Float | M | The latitude of station. The field value must be a valid WGS 84 latitude in decimal degrees format. For example: 46.94648 |
| longitude | Float | M | The longitude of station. The field value must be a valid WGS 84 longitude in decimal degrees format. For example: 7.44426 |
| address | [addressType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#addressType) | O | Valid street and street number where station is located. |
| stationStatus | [statusType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#statusType) | M | Indicates the status of the station. |
| availableVehicles | Integer | M | Amount of available vehicles. |
| accessDescription | String | O |  |
| openingHours | String | O |  |


### statusType

| Option | Description |
| ------------- | ------------- |
| Available |  |
| Reserved |  |
| Occupied |  |
| OutOfService |  |
| NotFound |  |
| Unknown |  |

### systemType

| Option | Description |
| ------------- | ------------- |
| BikesDocks |  |
| BikesDockless |  |
| EBikesDocks |  |
| EBikesDockless |  |

### vehicle

| Name  | Data Type | M/O | Description |
| ------------- | ------------- | ------------- | --- |
| vehicleId | String | M | Unique vehicle id. Is defined by the provider |
| foreignKeyStation | String | M | Foreign key of the station as defined in [SwissSharedMobilityPushSystem](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#swisssharedmobilitypushsystem). |
| vehicleStatus | [statusType](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#statusType) | M | Indicates the state of a vehicle. |
| vehicleType | String | M | Indicates the vehicle type. Vehicle types are predefined in a catalogue. |
| vehicleBooking | String | O | Deeplink to the providers booking system. |
| requirements | List ([requirement](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#requirement))  | M | List of requirements. Array of Objects. See below for definition of data type. |
| chargingStatus | String | O | e-vehicles have to indicate the charging status of the battery. |
| travelTo | List ([station](https://github.com/SFOE/SwissSharedMobility/blob/master/Specification.md#station)) | M | List of stations. Array of Objects. See below for definition of data type station. |

### vehicleType

| Option | Description |
| ------------- | ------------- |
| Bike |  |
| E-Bike 25 km/h |  |
| E-Bike 40 km/h |  |

## Best practice

### Free-floating: (E)-Bikes, (E)-Cars, (E)-Scooters...
Generate a station per vehicle. The dynamic part of the data is the location of the station/vehicle (latitude, longitude).

## Open questions
Please refer to [Issues](https://github.com/SFOE/SwissSharedMobility/issues) for ongoing discussions and open questions.
