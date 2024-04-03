# Aggregation Examples

## Data Model

#### Users

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

#### Books
```javascript
[
    {
        "_id":1,
        "title":"The Great Gatsby",
        "author_id":100,
        "genre":"Classic"
    },
    ...
]
```

#### Authors
```javascript
[
    {
        "_id":100,
        "name":"F. Scott Fitzgerald",
        "birth_year":1896
    },
    ...
]
```

## Problems

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

### 8. How many users have 'enim' as one of their tags?

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

### 9. What are the name and age of the users who are inactive and have 'velit' as a tag?

#### Solution
```javascript
[
    {
        $match: {
            isActive: false,
            tags: "velit"
        }
    },
    {
        $project: {
            name: 1,
            age: 1
        }
    }
]
```

#### Output
```javascript
[
    {
        "_id": {
            "$oid": "660be4cee54e0a954da38ae7"
        },
        "name": "Aurelia Gonzales",
        "age": 20
    },
    ...
]
```

### 10. How many users have a phone number strating with "+1 (940)"?

#### Solution
```javascript
[
    {
        $match: {
            "company.phone": /^\+1 \(940\)/
        }
    },
    {
        $count: "userCount"
    }
]
```

#### Output
```javascript
[
    {
        "userCount": 5
    }
]
```

### 11. Name, Registration Time, FavouriteFruit of 4 users who has registered the most recently?

#### Solution
```javascript
[
    {
        $sort: {
            registered: -1
        }
    },
    {
        $limit: 4
    },
    {
        $project: {
            name: 1,
            registered: 1,
            favoriteFruit: 1
        }
    }
]
```

#### Output
```javascript
[
    {
        "_id": {
            "$oid": "660be4cee54e0a954da38da9"
        },
        "name": "Stephenson Griffith",
        "registered": {
            "$date": "2018-04-14T03:16:20.000Z"
        },
        "favoriteFruit": "apple"
    },
    ...
]
```

### 12. Categorized users by their favourite fruit.

#### Solution
```javascript
[
    {
        $group: {
            _id: "$favoriteFruit",
            users: {
                $push: "$$ROOT" // Push entire object
            }
        }
    }
]
```

It's also possible to push name field only by replacing ```$$ROOT``` with ```$name```.

#### Output
```javascript
[
    {
        _id: "apple",
        users: [
            {
                // User Object
            },
            ...
        ]
    },
    ...
]
```

### 13. How many users have 'ad' as the second tag in their list if tags?

#### Solution
```javascript
[
    {
        $match: {
            "tags.1": "ad"
        }
    },
    {
        $count: "userCount"
    }
]
```

#### Output
```javascript
[
    {
        "userCount": 12
    }
]
```

### 14. Find user who have both 'enim' and 'id' as their tags.

#### Solution
```javascript
[
    {
        $match: {
            tags: {
                $all: ['enim', 'id']
            }
        }
    }
]
```

#### Output
```javascript
[
    {
        // User Object having both 'enim' and 'id' in tags
    },
    ...
]
```

### 15. List all the companies located in the USA with their corresponding user count.

#### Solution
```javascript
[
    {
        $match: {
            "company.location.country": "USA"
        }
    },
    {
        $group: {
            _id: "$company.title",
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
        "_id": "HOUSEDOWN",
        "count": 1
    },
    ...
]
```

### 16. Lookup Example (Books, Authors)

#### Solution
```javascript
[
    {
        $lookup: {
            from: "authors",
            localField: "author_id",
            foreignField: "_id",
            as: "author_details"
        }
    },
    {
        $addFields: {
            author_details: {
                $arrayElemAt: ["$author_details", 0]
            }
        }
    }
]
```

```$arrayElemAt: ["$author_details", 0]``` can be replaced with ```$first: "$author_details"```

#### Output
```javascript
[
    {
        "_id": 1,
        "title": "The Great Gatsby",
        "author_id": 100,
        "genre": "Classic",
        "author_details": {
            "birth_year": 1896,
            "_id": 100,
            "name": "F. Scott Fitzgerald"
        }
    },
    ...
]
```