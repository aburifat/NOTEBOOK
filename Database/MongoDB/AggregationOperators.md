# Aggregation Operators

## $avg
Returns the average value of the numeric values. 
```$avg```
 ignores non-numeric values.

 ### Syntex
 When used in the ```$bucket```, ```$bucketAuto```, ```$group```, and ```$setWindowFields``` stages, 
```$avg```
 has this syntax:

 ```javasctipt
{ $avg: <expression> }
 ```

 ### Reference
 https://www.mongodb.com/docs/manual/reference/operator/aggregation/avg/