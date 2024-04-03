# Aggregation Stages

## $addFields
Adds new fields to documents. $addFields outputs documents that contain all existing fields from the input documents and newly added fields.

### Syntex
```javascript
{ $addFields: { <newField>: <expression>, ... } }
```

### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/addFields/

## $count
Passes a document to the next stage that contains a count of the number of documents input to the stage.

### Syntex
```javascript
{ $count: <string> }
```
```<string>``` is the name of the output field which has the count as its value. ```<string>``` must be a non-empty string, must not start with $ and must not contain the . character.

### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/count/

## $group
The $group stage separates documents into groups according to a "group key". The output is one document for each unique group key.

A group key is often a field, or group of fields. The group key can also be the result of an expression. Use the _id field in the $group pipeline stage to set the group key. 

### Syntex
```javascript
{
 $group:
   {
     _id: <expression>, // Group key
     <field1>: { <accumulator1> : <expression1> },
     ...
   }
}
```

### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/group/

## $match
Filters the documents to pass only the documents that match the specified condition(s) to the next pipeline stage.

### Syntex
```javascript
{ $match: { <query> } }
```

### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/match/

