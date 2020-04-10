---
title: big data revision
tags: Big Data
categories: Notes
abbrlink: 1984119a
date: 2020-03-22 17:19:29
---
{% cq %}A revision for Big Data System.{% endcq %}
<!-- more -->
# Big Data Definitions
- huge volumes of data
- the challenges, risks, and rewards of storing and extracting meaningful information from this data
- it becomes difficult to process using on-hand data management tools or traditional data processing applications
## Volume
- Sheer size of data in terms of storage and access.
- Many different factors can contribute to the increase in data volume.
## Velocity
- Speed of incoming data and the time it takes to process.
- Data velocity is both the speed at which data streams in, and the timely manner in which data must be dealt with to maintain time based relevance.
## Variety
- Types of files and formats of data as well as sources.
- Data comes in all kinds of formats, but can be grouped into two types: structured and unstructured.
- Structured data is the numeric data in traditional databases. Created from line-of-business and pre-formatted data collected over time.
- Unstructured data is the relational and seemingly unrelated data that comes from unstructured sources (social media, text documents, email, video, audio, etc.)

> Extra Vs have been proposed, these typically describe characteristics rather than being definitional

## Veracity
- How accurate and meaningful is the data?
## Value
- How can value be derived from a big dataset?

# Big Data Examples
- smart healthcare
- wearable devices
- smart retail
- equipment health management
- connected/smart cars
- intelligent transport
- smart grid
- smart cities
- recommender systems
- finance

# HIGH LEVEL ARCHITECTURE
- The challenge of Big Data is how can we possibly deal with data that fits	these characteristics, both individually and collectively.
- The core of the answer lies in using distributed resources.
## Big Data sources
- The	sources	layer	refers to all	of the data available for analysis, coming in from all channels.	The	type of analysis and sources are closely related.
## Data messaging and store layer
- is responsible for acquiring data from data sources.
- If	necessary,	the	layer	will also be responsible	for	converting	the	data	to	a format	that	suits	how	the	data will	be analysed.
- Data acquisition
- Data digest
- Distributed file storage
## Analysis layer
- The	analysis layer reads the data digested by the data massaging	and	store	layer	(in	some	cases, it accesses data directly from the data source).
- Entity indentification
- Analytics engine
- Model management
## CONSUMPTION LAYER
- This	layer	consumes	the	output	provided	by	the	analysis	layer.
## INFORMATION	INTEGRATION	LAYER
- Responsible	for	connecting	to	various	data	sources.
- Requires	quality	connectors &	adapters
## DATA	GOVERNANCE	LAYER
- GDPR:	General	Data	Protection	Regulation
## SYSTEM	MANAGEMENT	layer
## QUALITY OF	SERVICE	(QOS)	LAYER

# MapReduce
- Programming	model	for	expressing	distributed	computation	in massive-scale	systems.
- Open-source	implementation	called	Hadoop.
## MapReduce	process
- Iterate	over a large number of records.
‒ Extract	something	of interest from	each.(Map)
‒ Shuffle	and	sort intermediate	results.
‒ Aggregate	intermediate results into something usable.(Reduce)
‒ Generate final output.(Reduce)
## Distributed	File	System	(DFS)
- move	workers	to	the	data:
  - Not	enough	RAM	to	hold	all	the	data	in	memory
  - Disk access is slow,	but	disk throughput is reasonable
