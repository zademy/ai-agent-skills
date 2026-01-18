---
name: aggregation
description: Aggregation pipeline in MongoDB
---

# MongoDB Aggregation Pipeline

## Pipeline Stages

```javascript
db.orders.aggregate([
  // Filter
  { $match: { status: 'completed' } },
  
  // Group
  { $group: {
    _id: '$user_id',
    total: { $sum: '$total' },
    count: { $sum: 1 },
    avgTotal: { $avg: '$total' }
  }},
  
  // Sort
  { $sort: { total: -1 } },
  
  // Limit
  { $limit: 10 }
]);
```

## Lookup (Join)

```javascript
db.orders.aggregate([
  {
    $lookup: {
      from: 'users',
      localField: 'user_id',
      foreignField: '_id',
      as: 'user'
    }
  },
  { $unwind: '$user' },
  {
    $project: {
      order_id: 1,
      user_name: '$user.name',
      total: 1
    }
  }
]);
```

## Accumulators

```javascript
db.products.aggregate([
  { $group: {
    _id: '$category',
    products: { $push: '$name' },
    avgPrice: { $avg: '$price' },
    maxPrice: { $max: '$price' },
    minPrice: { $min: '$price' }
  }}
]);
```
