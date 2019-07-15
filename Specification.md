# Specification
This document explains the SwissSharedMobility data exchange standard.

## Introduction
The SwissSharedMobility standard is an open data standard for Shared Mobility. The data standard aims to describe real-time data for all kind of Shared Mobilities such as bike sharing, car sharing or scooter sharing.
The suggested data standard is based on the ["General Bikeshare Feed Specification"](https://github.com/NABSA/gbfs/blob/master/README.md) which was designed by the "North American Bikeshar Association".

The SwissSharedMobility standard is constructed modularly. Therefore operators can introduce the data standard in stages. The following modules are available:

Mandatory
 * SwissSharedMobilityPushSystem
 * SwissSharedMobilityPushStation
 * SwissSharedMobilityPushStatus

Optional
* SwissSharedMobilityPushHours
* SwissSharedMobilityPushCalendar
* SwissSharedMobilityPushRegions
* SwissSharedMobilityPushPricing
* SwissSharedMobilityPushAlerts

### SwissSharedMobilityPushSystem
Describes the system

| Field Name  | Required | Defines|
| ------------- | ------------- | --- |
| system_id  | yes |  ID field - identifier for this bike share system. This should be globally unique (even between different systems) and it is currently up to the publisher of the feed to guarantee uniqueness. In addition, this value is intended to remain the same over the life of the system. | 
| name  | yes  |




