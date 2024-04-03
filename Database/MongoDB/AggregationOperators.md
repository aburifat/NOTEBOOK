# Aggregation Operators

## $all
The ```$all``` operator selects the documents where the value of a field is an array that contains all the specified elements.

#### Syntex
```javascript
{ <field>: { $all: [ <value1> , <value2> ... ] } }
```

#### Reference
https://www.mongodb.com/docs/manual/reference/operator/query/all/

## $arrayElemAt
Returns the element at the specified array index.

#### Syntext
```javascript
{ $arrayElemAt: [ <array>, <idx> ] }
```

#### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/arrayElemAt/

## $avg
Returns the average value of the numeric values. 
```$avg```
 ignores non-numeric values.

 #### Syntex
 When used in the ```$bucket```, ```$bucketAuto```, ```$group```, and ```$setWindowFields``` stages, ```$avg``` has this syntax:

 ```javascript
{ $avg: <expression> }
 ```

 #### Reference
 https://www.mongodb.com/docs/manual/reference/operator/aggregation/avg/

 ## $first
 Returns the result of an expression for the first document in a group of documents. Only meaningful when documents are in a defined order.

 #### Syntex
 ```javascript
{ $first: <expression> }
 ```

 #### Reference
 https://www.mongodb.com/docs/manual/reference/operator/aggregation/first/

 ## $ifNull
 The ```$ifNull``` expression evaluates input expressions for null values and returns:
- The first non-null input expression value found.
- A replacement expression value if all input expressions evaluate to null.

```$ifNull``` treats undefined values and missing fields as null.

#### Syntex
```javascript
{
   $ifNull: [
      <input-expression-1>,
      ...
      <input-expression-n>,
      <replacement-expression-if-null>
   ]
}
```

#### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/ifNull/

## $push
```$push``` returns an array of all values that result from applying an expression to documents.

#### Syntex
```javascript
{ $push: <expression> }
```

#### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/push/

 ## $size
 Counts and returns the total number of items in an array.

 #### Syntex
 ```javascript
{ $size: <expression> }
 ```
The argument for ```$size``` can be any expression as long as it resolves to an array.

 #### Reference
https://www.mongodb.com/docs/manual/reference/operator/aggregation/size/

 ## $sum
 Calculates and returns the collective sum of numeric values. 
```$sum```
 ignores non-numeric values.

 #### Syntex
 When used as an accumulator, 
```$sum```
 has this syntax:

 ```javascript
{ $sum: <expression> }
 ```

 #### Reference
 https://www.mongodb.com/docs/manual/reference/operator/aggregation/sum/