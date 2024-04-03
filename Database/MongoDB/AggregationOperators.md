# Aggregation Operators

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