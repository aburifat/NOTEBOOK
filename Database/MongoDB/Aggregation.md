# Aggregation

## Stages

### $addFields
Adds new fields to documents. $addFields outputs documents that contain all existing fields from the input documents and newly added fields.

#### Syntex
```
{ $addFields: { <newField>: <expression>, ... } }
```

#### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/addFields/
