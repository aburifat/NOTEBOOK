# Aggregation Examples

## Data Model (Users)
```json
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
Solution
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
Output
```json
{
  "activeUser": 516
}
```

### 2. What is the average age of all users?
Solution
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
Output
```json
{
  "_id": null,
  "averageAge": 29.835
}
```