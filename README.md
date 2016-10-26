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

