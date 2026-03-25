# Spline File Format


## Spline File Structure


A spline file is an `.spl` text file, based on the [json](http://www.json.org/) format. This file contains all necessary information to define a [spline graph](../../api/library/worlds/class.splinegraph_cpp.md#intro) consisting of points in 3D space, connected by cubic Bezier spline segments. Spline graphs can be adjusted by manually editing an `.spl` file in a text editor or via [API](../../api/library/worlds/class.splinegraph_cpp.md).


![](spline.png)


There are **2** basic sections in the `.spl` file:

- **[Points](#points).** This section contains the list of all points of the spline graph represented by their coordinates (X, Y, Z).
- **[Segments](#segments).** This section contains the list of spline segments connecting different points.


In general the syntax of the `.spl` file is as follows:

```java
{
	"points": [
		[
			-1335.1749267578125,
			78.811111450195313,
			4.7690000534057617
		],

		...

	],
	"segments": [
		{
			"start_index": 0,
			"start_tangent": [
				-4.7529296875,
				4.06640625,
				-2.1245796233415604e-009
			],
			"start_up": [
				0,
				0,
				1
			],
			"end_index": 1,
			"end_tangent": [
				2.8794116973876953,
				-1.2208551168441772,
				8.9795076929632955e-010
			],
			"end_up": [
				0,
				0,
				1
			]
		},

		...

	]
}

```


## Points Data


The first section of the `.spl` file contains the array of [spline points](../../api/library/worlds/class.splinegraph_cpp.md#intro). Each point is represented as an array of 3 coordinates (X, Y, Z). The number of points is not limited. Vertex indices come in the order of appearance starting from **0**.


```java
	"points": [
		[
			-1335.1749267578125,
			78.811111450195313,
			4.7690000534057617
		],
		[
			-1404.5445556640625,
			150.18548583984375,
			3.8284587860107422
		],
		[
			-1427.984130859375,
			153.21903991699219,
			3.1477432250976562
		],
		[
			40.473739624023438,
			563.27911376953125,
			2.1209244728088379
		],

		...
	]

```


## Segments Data


The second section of the `.spl` file contains the list of [spline segments](../../api/library/worlds/class.splinegraph_cpp.md#intro) connecting the points described above. The number of segments is not limited and does not depend on the number of points.


Each of the segments is represented by the following elements:

|  |  |
|---|---|
| **start_index** | Index of the spline segment's starting point in the [list of points](#points). |
| **start_tangent** | Tangent coordinates at the starting point of the spline segment. Tangent coordinates define the form of the segment. |
| **start_up** | ["Up" vector coordinates](../../api/library/worlds/class.splinegraph_cpp.md#up) at the starting point of the spline segment. |
| **end_index** | Index of the spline segment's ending point in the [list of points](#points). |
| **end_tangent** | Tangent coordinates at the ending point of the spline segment. Tangent coordinates define the form of the segment. |
| **end_up** | ["Up" vector coordinates](../../api/library/worlds/class.splinegraph_cpp.md#up) at the ending point of the spline segment. |


```java
	"segments": [
		{
			"start_index": 0,
			"start_tangent": [
				-4.7529296875,
				4.06640625,
				-2.1245796233415604e-009
			],
			"start_up": [
				0,
				0,
				1
			],
			"end_index": 1,
			"end_tangent": [
				2.8794116973876953,
				-1.2208551168441772,
				8.9795076929632955e-010
			],
			"end_up": [
				0,
				0,
				1
			]
		},

		...
	]

```
