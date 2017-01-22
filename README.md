# charlie_checker
Correlate routes with GPS updates for MBTA buses in Greater Boston

# Overview

This will be a web app written in Python and Neo4J that collects and analyzes MBTA vehicle route schedules
and actual vehicle performance.

## Key Functionality Items

* Use Python 3.5 and asyncio
* Use Neo4j (current version)
* Use MBTA schedule download to establish system timetables
* Load graph database with nodes of stops, edges of vehicle and on-foot connections between stops
* Sample vehicle performance API at MBTA for however many routes we can do for however long

## Queries we would want to support

* Fastest nominal route between two points, variability over course of day
* Most and least variable aspects of route or complete commute path
* For example, by giving stop ID, identify most consistent route between Arlington Center and Park Street leaving between 9 and 10 AM
* Larger analysis rating routes by reliability, best case, worst case
* Identify anomalies in schedule e.g. unannounced route changes

## Aspects to Think About

* Size of graph database
* Geofencing to locate nearby stop nodes, use MBTA function or build a temporary MongoDB?

# Implementation Parts

## Collect Schedule Feed

The MBTA schedule is published as a GTFS feed. The feed data comes in the form of a zipfile which needs to be
transferred, unpacked, cleaned, and verified. The "gtfstk" Python module, currently at version 6.0.0 does
this and produces a Feed object which comprises all the data from the feed's zipfile organized into
DataFrames. DataFrames are structures defined in and manipulated by the Pandas Python module. The Pandas
module includes useful aggregation and statistical code, and the related GeoPandas provides geolocation
functionality that we will want, so we'll use:

* Google's transitfeed code for validation of static schedule https://github.com/google/transitfeed
* Google's protocol-buffers code for realtime feed (via Pypi as "protobuf")
* Google's language bindings for the GTFS-realtime feed in Protocol Buffers https://github.com/google/gtfs-realtime-bindings
* gtfstk for parsing static and realtime feeds https://github.com/araichev/gtfstk
* pandas
* geopandas

gtfstk also pulls in a lot of dependencies which might be required for Jupyter integration that we won't use, we'll
need to sort through that further.

On startup, our code should check if we have a schedule loaded and if not, go get one.

Probably save the cleaned version for reload if there is no new schedule when we start up.

## Graph Database Load

* traverse DataFrames in Feed object
* establish edges for vehicles
* establish which stops are near other stop for transfers with a short walk

## Collect Realtime Metrics


