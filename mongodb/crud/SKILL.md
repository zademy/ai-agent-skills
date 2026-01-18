---
name: crud
description: CRUD operations in MongoDB
---

# MongoDB CRUD Operations

## Create (Insert)

```javascript
// Insert one
db.users.insertOne({
  name: 'John',
  email: 'john@example.com',
  age: 30,
  createdAt: new Date()
});

// Insert many
db.users.insertMany([
  { name: 'Jane', email: 'jane@example.com' },
  { name: 'Bob', email: 'bob@example.com' }
]);
```

## Read (Find)

```javascript
// Find all
db.users.find();

// Find with filter
db.users.find({ age: { $gte: 18 } });
db.users.find({ name: /^J/ });
db.users.find({ email: { $exists: true } });

// Find one
db.users.findOne({ _id: ObjectId('xxx') });

// Projection
db.users.find({}, { name: 1, email: 1, _id: 0 });

// Sort and limit
db.users.find().sort({ createdAt: -1 }).limit(10);
```

## Update

```javascript
// Update one
db.users.updateOne(
  { _id: ObjectId('xxx') },
  { $set: { name: 'John Doe' } }
);

// Update many
db.users.updateMany(
  { status: 'inactive' },
  { $set: { updatedAt: new Date() } }
);

// Array operations
db.users.updateOne(
  { _id: ObjectId('xxx') },
  { $push: { tags: 'premium' } }
);
```

## Delete

```javascript
// Delete one
db.users.deleteOne({ _id: ObjectId('xxx') });

// Delete many
db.users.deleteMany({ status: 'deleted' });
```
