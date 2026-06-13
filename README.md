# SQL Shortcut Scripts

A personal reference library of advanced T-SQL patterns for SQL Server.

![T-SQL](https://img.shields.io/badge/T--SQL-SQL%20Server-blue)

## Overview

This repo is a collection of reusable T-SQL snippets covering advanced SQL Server techniques that come up repeatedly in day-to-day development and DBA work. Each script targets a specific pattern — indexing strategies, constraint management, triggers, utility queries, and more. Intended as a grab-and-adapt reference, not a runnable project.

## Scripts Reference

| Script File | Category | Description |
|---|---|---|
| `Clustered Index.sql` | Indexing | Creates a unique clustered index on a view column; includes `WITH SCHEMABINDING` view pattern and `sp_refreshview` for on-demand refresh |
| `Materialized view__Indexed view.sql` | Views | Demonstrates indexed (materialized) view creation with `SCHEMABINDING`, `COUNT_BIG(*)` for grouped aggregations, and `set statistics io on` for I/O profiling |
| `Constraints_ON_OFF.sql` | Constraints | Uses `sp_msforeachtable` to bulk enable or disable all foreign key / check constraints across every table — useful for bulk data loads |
| `delete all tables in a DB even with constraints.sql` | Utilities | Drops all foreign key constraints via a cursor over `INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS`, then drops all tables with `sp_MSforeachtable` |
| `Create Trigger on LastUpdatedDate.sql` | Triggers | `AFTER INSERT, UPDATE` trigger template that captures row counts and validates fields on the affected table — adaptable to any audit / timestamp pattern |
| `Function output fields logic partially done.sql` | Functions | Parses `INFORMATION_SCHEMA.ROUTINES` to extract the SELECT output columns from a named scalar function using `SUBSTRING`, `CHARINDEX`, and `STRING_SPLIT` |
| `STUFF combine with a comma.sql` | Utilities | Uses `STUFF` + `FOR XML PATH('')` to concatenate multi-row values into a single comma-separated string per group (classic row-to-column pivot pattern) |
| `SearchTableColumnName.sql` | Utilities | Queries `sys.columns` joined to `sys.tables` to find every table containing a column whose name matches a given pattern — handy for schema discovery |
| `Top with ties.sql` | Utilities | Demonstrates `SELECT TOP(n) WITH TIES` — returns all rows that share the same value as the nth row in the `ORDER BY`, preventing arbitrary truncation of tied results |
| `get the smaller and the larger numbers without using MIN and MAX.sql` | Practice | Self-join technique to compare rows within the same table and surface the smaller vs. larger value without using aggregate functions `MIN`/`MAX` |
| `orix_quiz.sql` | Practice | SQL puzzle / quiz schema — creates `species`, `ponds`, and `ducks` tables with constraints and seed data; used for join and filtering practice scenarios |

## Quick Usage

1. Open the target `.sql` file in **SSMS** or **Azure Data Studio**.
2. Switch to the appropriate database context (`USE [YourDatabase]`).
3. Read the inline comments — most scripts reference example table/schema names that need to be swapped for your own.
4. Run in a non-production environment first; scripts like `delete all tables in a DB even with constraints.sql` are destructive by design.

## Prerequisites

- **SQL Server** 2016 or later (some features — `STRING_SPLIT`, indexed views — require 2016+; most patterns work on 2012+)
- **SSMS** 18+ or **Azure Data Studio** — either works for running these scripts
