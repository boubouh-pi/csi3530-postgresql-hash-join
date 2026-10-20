# Symmetric Hash Join in PostgreSQL

Implementation of the symmetric hash join algorithm in the PostgreSQL query executor, built for the CSI3530 database course at the University of Ottawa.

## Overview

A standard hash join first builds a hash table on one relation, then probes it with the other. A **symmetric hash join** builds hash tables on both relations at the same time: each incoming tuple is inserted into its own relation's hash table and immediately probed against the other one. Results are produced as soon as matches are found, which makes the join pipelined.

## Modified PostgreSQL source files

| File | Change |
|---|---|
| `execnodes.h` | `HashJoinState` extended with an inner and an outer hash table |
| `nodeHashjoin.c` | Join logic rewritten for the symmetric hash join |
| `nodeHash.c` | Hash node switched to pipelined execution: each tuple is inserted into the hash table and immediately passed on |
| `createplan.c` | Planner changes to use hash nodes on both inputs |

`OUTPUT-QUERY-SCHEMA.txt` contains the test schema and data (`dept`, `emp`, `manages`) used to check the results.

## Tech

C, PostgreSQL source code (executor and planner).
