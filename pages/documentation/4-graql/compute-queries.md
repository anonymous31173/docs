---
title: Compute Queries
keywords: graql, compute, match
last_updated: September 28, 2016
tags: [graql]
summary: "Graql Compute Queries"
sidebar: documentation_sidebar
permalink: /documentation/graql/compute-queries.html
folder: documentation
---

A compute query executes a [Pregel algorithm](https://www.quora.com/What-are-the-main-concepts-behind-Googles-Pregel) to determine information about the graph in parallel. Called within the Graql shell, the general syntax is:

```
compute [algorithm] in [subgraph];
```

* `algorithm` can be any of the [available statistics algorithms](#available-statistics-algorithms).
* `subgraph` is a comma separated list of type IDs to be visited by the Pregel algorithm. 

## Subgraph

The subgraph syntax is provided to control the types that a chosen [algorithm](#available-algorithms) operates upon. By default, the compute algorithms include instances of every type in the calculation. Using the `in` keyword followed by a comma separated list of types will restrict the calculations to instances of those types only.

For example,

```
compute count in person;
```

will return just the number of instances of the concept type person.

## Available Statistics Algorithms

The following algorithms are available to perform simple statistics compuations, and we aim to add to these as demand dictates. Please get
in touch on our [discussion](https://discuss.grakn.ai/) page to request any features that are of particular interest
to you. A summary of the statistics algorithms is given in the table below.

| Algorithm | Description                                   |
| ----------- | --------------------------------------------- |
| [`count`](#count)     | Count the number of instances.                        |
| [`max`](#maximum)    | Compute the maximum value of a resource. |
| [`mean`](#mean)    | Compute the mean value of a resource.                           |
| [`median`](#mean)    | Compute the median value of a resource.                           |
| [`min`](#minimum)    | Compute the minimum value of a resource. |
| [`std`](#standard-deviation)    | Compute the standard deviation of a resource. |
| [`sum`](#sum)    | Compute the sum of a resource. |

For further information see the individual sections below.

### Count

The default behaviour of count is to return a single value that gives the number of instances present in the graph. It
is possible to also count subsets of the instances in the graph using the [subgraph](#subgraph) syntax, as described above.

```
compute count in person;
```

### Mean

Computes the mean value of a given resource type. This algorithm requires the [subgraph](#subgraph) syntax to be used.
For example,

```
compute mean of age in person;
```

would compute the mean of the value persisted in instances of the resource type age. It is also possible to provide a
set of resource types.

```
compute mean of user-rating, expert-rating in movie;
```

which would compute the mean of the union of the instances of the two resource types.

### Median

Computes the median value of a given resource type. This algorithm requires the [subgraph](#subgraph) syntax to be used.
For example,

```
compute median of age in person;
```

would compute the median of the value persisted in instances of the resource type age. 

### Minimum

Computes the minimum value of a given resource type, similar to [mean](#mean).

```
compute min of age in person;
```

### Maximum

Computes the maximum value of a given resource type, similar to [mean](#mean).

```
compute max of age in person;
```

### Standard Deviation

Computes the standard deviation of a given resource type, similar to [mean](#mean).


```
compute std of age in person;
```

### Sum

Computes the sum of a given resource type, similar to [mean](#mean).

## When to Use `aggregate` and When to Use `compute`

[Aggregate queries](./aggregate-queries.html) are computationally light and run single-threaded on a single machine, but are more flexible than the equivalent compute queries described above.

For example, you can use an aggregate query to filter results by resource. The following  aggregate query, allows you to match the number of people of a particular name:

```
match $x has name 'Bob'; aggregate count;
```

Compute queries are computationally intensive and run in parallel on a cluster (so are good for big data).

```
compute count of person; 
```

Compute queries can be used to calculate the number of people in the graph very fast, but you can't filter the results to determine the number of people with a certain name.


{% include links.html %}