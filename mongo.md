### Mongo some information

1) Egnore some properties in the model
```
var usr = User.find().select("--password --anyPeropertyName");
```

### Mongo query
1) Find all documents that have a category of "news".
```
Find all documents that have a category of "news".
```

### aggregate
Aggregate use multiple stage .
Stage is {} ,{}
``` 
  const channel = await User.aggregate([
        {
            $match: {
                username: username?.toLowerCase()
            }
        },
        {
            $lookup: {
                from: "subscriptions",
                localField: "_id",
                foreignField: "channel",
                as: "subscribers"
            }
        },
        {
            $lookup: {
                from: "subscriptions",
                localField: "_id",
                foreignField: "subscriber",
                as: "subscribedTo"
            }
        },
        {
            $addFields: {
                subscribersCount: {
                    $size: "$subscribers"
                },
                channelsSubscribedToCount: {
                    $size: "$subscribedTo"
                },
                isSubscribed: {
                    $cond: {
                        if: {$in: [req.user?._id, "$subscribers.subscriber"]},
                        then: true,
                        else: false
                    }
                }
            }
        },
        {
            $project: {//This is work in IF show filed that  value is One , else 
                fullName: 1,
                username: 1,
                subscribersCount: 1,
                channelsSubscribedToCount: 1,
                isSubscribed: 1,
                avatar: 1,
                coverImage: 1,
                email: 1

            }
        }
    ])
```

**####`group`####**
Group is basically work like Group By in SQl

 
Use group  when we want to get a value in a group like get deparment wise student count
```json
[
 {
   $group: {
     _id: expression,
     fieldN: {
       accumulatorN: expressionN
     }
   }
 }
]
[
 {
   $group: {
     _id: $deparment,
     fieldN: {
       $sum : 1
     }
   }
 }
]

```
This query use for count Number in studnet count 

**####`Limit`####**

Limit is use when  we want to get limit of data one time
```java
db.users.find().limit(1)
```

**####`project`####**
Project is use when only  some field are get
use 1 for show get filed an use 0 not shaow filed
```java
db.restaurants.aggregate([
  {
    $project: {
      "name": 1,
      "cuisine": 1,
      "address": 1
    }
  },
  {
    $limit: 5
  }
])
```
```java
{
  _id: ObjectId('66b7e4ef9fc55996b756f89f'),
  name: 'Ayush',
  state: 'Guj'
}
```

Output is 
```json

{
  _id: ObjectId('66b7e4ef9fc55996b756f89f'),
  name: 'Ayush',
  state: 'Guj'
}
```



**####`sort`####**
Sort is use sort value in some property
```java
db.users.find().sort({"acre" : 1})
```
```json
db.listingsAndReviews.aggregate([ 
  { 
    $sort: { "accommodates": -1 } 
  },
  
])
```

**####`match`###**
Match are use for Match property value If match then get data
```
db.listingsAndReviews.aggregate([ 
  { $match : { property_type : "House" } },
s])
```

**###`$addFields`###**
AddField is use for add some value  filed in array property.
For example add comment to post when we want to add comment id to post table while using addfields
```json
await Post.updateOne(
      { _id: postId },
      { $addToSet: { comment: addComment._id } }
    );

```

**###`$Count`###**
Count is use for count totla  document 
```json
db.user.find().count()
```


**###`$lookup`###**
lookup is wrok like left outer join
If we are want to join other data in current collction when use lookup

1. Customer table
```json
[
  {"_id" :1, "name" : "paresh" },
  {"_id" :2, "name" : "Raju" },
]
```
2. Order table
```json
[
  {"id" : 11 , "OrderName" : "abc" , "Customer_id" : 1},
  {"id" : 12 , "OrderName" : "abc" , "Customer_id" : 2},
]
```

You wnat to get all data in customer like {_id , name , Ordername }

```java
db.customer.aggregate(
[
  {
    $lookup : {
      from : "Order",//Which table are join wnat you table name (collection name)
      localfield : "_id",//Find collection in primary key
      foreignField : "Customer_id",//join collection table ForeginKey
      as : "Order_details" // show other details property name
    }
  }
]
)
```

**###`Output`###**
```json
[
  {"_id" :1, "name" : "paresh" , "Order_details" : {"id" : 11 ,"OrderName" : "abc" , "Customer_id" : 1}},
  {"_id" :2, "name" : "Raju" , "Order_details" : {"id" : 12 ,"OrderName" : "abc" , "Customer_id" : 2}},
]
```














