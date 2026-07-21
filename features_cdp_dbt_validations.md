# Supported Validations for DBT Segments | Data 360 Connect REST API

**Source:** https://developer.salesforce.com/docs/data/connectapi/guide/features_cdp_dbt_validations.html

---

To create a segment, use the POST /ssot/segments endpoint. To update a segment, use the PATCH /ssot/segments/{segmentApiName} endpoint.

When creating or updating a segment, the sql property is subject to these validations.

Only the primary key of the SegmentOn DMO is allowed in the select statement. The first table in the join clause must be a profile table.

No aggregation (min, max, avg, count) is allowed at the top-level select.

No select all (*) expression is allowed in the top-level select.

Only the primary key of the segment on table (the first table in the from clause of the sql statement) can be selected.

Multiple columns can’t be selected even if one of them is the primary key of the table.

No case statements are allowed in the primary select.

If the primary key of the segmentOn object has key qualifiers, you must project the key qualifiers, as well, in the primary select. First project the primary key and then the qualifier. Group bys must also include the key qualifiers.

If the primary key of the segmentOn object has key qualifiers, you can provide an additional condition in the join on condition.

All columns must be fully qualified by table name in the query and subselect queries.

Subqueries are supported only in a where clause and must emit only one column.

Compare columns of the same data type. To compare columns of different data types, cast one or both of the operands so that they have the same type.

limit and offset are supported.

Any SQL statement other than the select statement isn’t allowed.

Aliases are not supported.

To join two DMOs, there must be a relationship between the DMOs, and you must use one of their related join keys in the join on condition. The join on condition can contain only an equality comparison between the joining keys and an optional additional condition for comparing FQK fields.
