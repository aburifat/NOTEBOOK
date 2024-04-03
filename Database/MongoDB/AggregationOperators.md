# Aggregation Operators

## $avg
Returns the average value of the numeric values. 
```$avg```
 ignores non-numeric values.

 ### Syntex
 When used in the ```$bucket```, ```$bucketAuto```, ```$group```, and ```$setWindowFields``` stages, 
```$avg```
 has this syntax:

 ```javascript
{ $avg: <expression> }
 ```

 ### Reference
 https://www.mongodb.com/docs/manual/reference/operator/aggregation/avg/

 ## $sum
 Calculates and returns the collective sum of numeric values. 
```$sum```
 ignores non-numeric values.

 ### Syntex
 When used as an accumulator, 
```$sum```
 has this syntax:

 ```javascript
{ $sum: <expression> }
 ```

 ### Reference
 https://www.mongodb.com/docs/manual/reference/operator/aggregation/sum/