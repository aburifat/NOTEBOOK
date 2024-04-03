# Aggregation Stages

## $addFields
Adds new fields to documents. $addFields outputs documents that contain all existing fields from the input documents and newly added fields.

#### Syntex
```javascript
{ $addFields: { <newField>: <expression>, ... } }
```

#### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/addFields/

## $count
Passes a document to the next stage that contains a count of the number of documents input to the stage.

#### Syntex
```javascript
{ $count: <string> }
```
```<string>``` is the name of the output field which has the count as its value. ```<string>``` must be a non-empty string, must not start with $ and must not contain the . character.

#### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/count/

## $group
The $group stage separates documents into groups according to a "group key". The output is one document for each unique group key.

A group key is often a field, or group of fields. The group key can also be the result of an expression. Use the _id field in the $group pipeline stage to set the group key. 

#### Syntex
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

#### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/group/

## $limit
Limits the number of documents passed to the next stage in the pipeline.

#### Syntex
```javascript
{ $limit: <positive 64-bit integer> }
```

#### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/limit/

## $lookup
Performs a left outer join to a collection in the same database to filter in documents from the "joined" collection for processing. The ```$lookup``` stage adds a new array field to each input document. The new array field contains the matching documents from the "joined" collection. The ```$lookup``` stage passes these reshaped documents to the next stage.

#### Syntex
```javascript
{
   $lookup:
     {
       from: <collection to join>,
       localField: <field from the input documents>,
       foreignField: <field from the documents of the "from" collection>,
       as: <output array field>
     }
}
```
The ```$lookup``` takes a document with these fields:

|Field|Description|
|---|---|
|from|Specifies the collection in the same database to perform the join with.|
|localField|Specifies the field from the documents input to the ```$lookup``` stage.|
|foreignField|Specifies the field from the documents in the from collection.|
|as|Specifies the name of the new array field to add to the input documents.|

#### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/lookup/

## $match
Filters the documents to pass only the documents that match the specified condition(s) to the next pipeline stage.

#### Syntex
```javascript
{ $match: { <query> } }
```

#### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/match/

## $project
Passes along the documents with the requested fields to the next stage in the pipeline. The specified fields can be existing fields from the input documents or newly computed fields.

#### Syntex
```javascript
{ $project: { <specification(s)> } }
```
The ```$project``` specifications have the following forms:

|Form|Description|
|---|---|
|```<field>: <1 or true>```|Specifies the inclusion of a field. Non-zero integers are also treated as ```true```.|
|```_id: <0 or false>```|Specifies the suppression of the _id field.|
|```<field>: <expression>```|Adds a new field or resets the value of an existing field.|
|```<field>: <0 or false>```|Specifies the exclusion of a field.|

#### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/project/

## $sort
Sorts all input documents and returns them to the pipeline in sorted order.

#### Syntex
```javascript
{ $sort: { <field1>: <sort order>, <field2>: <sort order> ... } }
```
```$sort``` takes a document that specifies the field(s) to sort by and the respective sort order. ```<sort order>``` can have one of the following values:

|Value|Description|
|---|---|
|1|Sort ascending.|
|-1|Sort descending.|

#### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/sort/

## $unwind
Deconstructs an array field from the input documents to output a document for each element. Each output document is the input document with the value of the array field replaced by the element.

#### Syntex
```javascript
{ $unwind: <field path> }
```
When you specify the field path, prefix the field name with a dollar sign $ and enclose in quotes.

#### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/unwind/

