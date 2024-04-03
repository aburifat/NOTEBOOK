# Aggregation Examples

## Data Model (Users)
```javascript
[
    {
      "index": NumberInt(0),
      "name": "Aurelia Gonzales",
      "isActive": false,
      "registered": ISODate("2015-02-11T04:22:39+0000"),
      "age": NumberInt(20),
      "gender": "female",
      "eyeColor": "green",
      "favoriteFruit": "banana",
      "company": {
        "title": "YURTURE",
        "email": "aureliagonzales@yurture.com",
        "phone": "+1 (940) 501-3963",
        "location": {
          "country": "USA",
          "address": "694 Hewes Street"
        }
      },
      "tags": [
        "enim",
        "id",
        "velit",
        "ad",
        "consequat"
      ]
    },
    ...
]
```

### 1. How many users are active?
#### Solution
```javascript
[
    {
        $match: {
            isActive: true
        }
    },
    {
        $count: 'activeUser'
    }
]
```
#### Output
```javascript
{
  "activeUser": 516
}
```

### 2. What is the average age of all users?
#### Solution
```javascript
[
    {
        $group: {
            _id: null,
            averageAge: {
                $avg: "$age"
            }
        }
    }
]
```
#### Output
```javascript
[
    {
        "_id": null,
        "averageAge": 29.835
    }
]
```

### 3. List top 2 most common favourite fruits among users.

#### Solution
```javascript
[
    {
        $group: {
            _id: "$favoriteFruit",
            count: {
                $sum: 1
            }
        }
    },
    {
        $sort: {
            count: -1
        }
    },
    {
        $limit: 2
    }
]
```

#### Output
```javascript
[
    {
        "_id": "banana",
        "count": 339
    },
    {
        "_id": "apple",
        "count": 338
    }
]
```

### 4. Find total number of males and females.

#### Solution
```javascript
[
    {
        $group: {
            _id: "$gender",
            count: {
                $sum: 1
            }
        }
    }
]
```

#### Output
```javascript
[
    {
        "_id": "female",
        "count": 507
    },
    {
        "_id": "male",
        "count": 493
    }
]
```

### 5. Which country has the height number of registered users?

#### Solution
```javascript
[
    {
        $group: {
            _id: "$company.location.country",
            userCountryCount: {
                $sum: 1
            }
        }
    },
    {
        $sort: {
            userCountryCount: -1
        }
    },
    {
        $limit: 1
    }
]
```

#### Output
```javascript
[
    {
        "_id": "Germany",
        "userCountryCount": 261
    }
]
```

### 6. List all the eye colors present in the collection

#### Solution
```javascript
[
    {
        $group: {
            _id: "$eyeColor"
        }
    }
]
```

#### Output
```javascript
[
    {
        "_id": "green"
    },
    {
        "_id": "blue"
    },
    {
        "_id": "brown"
    }
]
```

### 7. What is the average number of tags(Array) per user?

#### Solution 1
```javascript
[
    {
        $unwind: "$tags"
    },
    {
        $group: {
            _id: "$_id",
            numberOfTags: {
                $sum: 1
            }
        }
    },
    {
        $group: {
            _id: null,
            avgNumberOfTags: {
                $avg: "$numberOfTags"
            }
        }
    }
]
```

#### Solution 2
```javascript
[
    {
        $addFields: {
            numberOfTags: {
                $size: {
                    $ifNull: ["$tags", []]
                }
            }
        }
    },
    {
        $group: {
            _id: null,
            avgNumberOfTags: {
                $avg: "$numberOfTags"
            }
        }
    }
]
```

#### Output
```javascript
[
    {
        "_id": null,
        "avgNumberOfTags": 3.556
    }
]
```

## 8. How many users have 'enim' as one of their tags?

#### Solution
```javascript
[
    {
        $match: {
            tags: "enim"
        }
    },
    {
        $count: 'userWithEnimTag'
    }
]
```

#### Output
```javascript
[
    {
        "userWithEnimTag": 62
    }
]
```