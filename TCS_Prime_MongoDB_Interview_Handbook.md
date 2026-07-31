# 🍃 TCS Prime MongoDB Interview Handbook

**The Complete MongoDB Revision Guide — Beginner to Advanced, Interview-Ready**

> Built for: TCS Prime · TCS Digital · TCS Ninja · Service-Based Companies · Product-Based Interviews
> Author's context: MERN stack developer (MongoDB, Express, React, Node) — SRM AP, B.Tech CSE

---

## 📑 Table of Contents

1. [MongoDB Fundamentals](#section-1-mongodb-fundamentals)
2. [MongoDB Architecture](#section-2-mongodb-architecture)
3. [Documents & Collections](#section-3-documents--collections)
4. [MongoDB CRUD](#section-4-mongodb-crud)
5. [Query Operators](#section-5-query-operators)
6. [Projection](#section-6-projection)
7. [Sorting, Limiting & Pagination](#section-7-sorting-limiting--pagination)
8. [Indexing](#section-8-indexing)
9. [Query Optimization & explain()](#section-9-query-optimization--explain)
10. [The ESR Rule](#section-10-the-esr-rule)
11. [Aggregation Framework](#section-11-aggregation-framework)
12. [$lookup (Joins)](#section-12-lookup-joins)
13. [Embedding vs Referencing](#section-13-embedding-vs-referencing)
14. [Data Modeling & Schema Design](#section-14-data-modeling--schema-design)
15. [Replication](#section-15-replication)
16. [Sharding](#section-16-sharding)
17. [Transactions](#section-17-transactions)
18. [Atomicity](#section-18-atomicity)
19. [Performance Optimization](#section-19-performance-optimization)
20. [Mongoose](#section-20-mongoose)
21. [MongoDB + Node.js](#section-21-mongodb--nodejs)
22. [Query Practice Bank](#section-22-query-practice-bank)
23. [TCS Prime Rapid-Fire Q&A Bank](#section-23-tcs-prime-rapid-fire-qa-bank)
24. [Scenario-Based Schema Design Questions](#section-24-scenario-based-schema-design-questions)
25. [Tricky Questions](#section-25-tricky-questions)
26. [Common Errors & Fixes](#section-26-common-errors--fixes)
27. [Best Practices](#section-27-best-practices)
28. [One-Page Cheat Sheet](#section-28-one-page-cheat-sheet)
29. [Last-Minute Revision Index](#section-29-last-minute-revision-index)

> 📌 **How to use this handbook:** Read Sections 1–21 top to bottom once (concept mastery). In the 3 days before your interview, drill Sections 22–29 daily. On interview morning, only read Sections 28 and 29.

---

## Section 1: MongoDB Fundamentals

### 1.1 What is MongoDB?

**Definition:** MongoDB is an open-source, **document-oriented NoSQL database** that stores data as flexible, JSON-like documents (BSON internally) instead of rows and columns.

**Why it's needed:** Relational databases enforce a rigid schema and normalize data across tables, which makes them slow to evolve and expensive to query when data is deeply nested or hierarchical (e.g., a product with variable attributes, a social media post with comments). MongoDB stores related data together in one document, matching how modern applications (especially JS-based apps) already model objects.

**Internal working:** MongoDB documents are stored as **BSON** (Binary JSON) on disk, managed by the **WiredTiger** storage engine, which handles compression, caching, and concurrency control via MVCC (Multi-Version Concurrency Control).

**Real-world example:** An e-commerce product with variable specs (a phone has RAM/storage, a shirt has size/color) — in SQL you'd need EAV tables or nullable columns; in MongoDB each product document just has the fields it needs.

```javascript
// A MongoDB document
{
  _id: ObjectId("64f1b2c3..."),
  name: "iPhone 15",
  price: 79900,
  specs: { ram: "6GB", storage: "128GB" },
  tags: ["mobile", "apple", "5G"]
}
```

> 💡 **Interview Tip:** If asked "What is MongoDB?" in one line, say: *"MongoDB is a document-oriented, schema-flexible NoSQL database that stores data in BSON format, built for horizontal scalability and high-velocity application development."*

**Follow-up questions:**
- Is MongoDB schema-less or schema-flexible? → **Schema-flexible** (you *can* enforce schema via validators, but it's not mandatory like SQL).
- Is MongoDB ACID compliant? → Yes, since v4.0 with multi-document transactions; always ACID at the single-document level.

**TCS Interview Perspective:** ⭐⭐⭐⭐⭐ Almost guaranteed opener question. Keep the answer to 3–4 lines, then let the interviewer probe deeper.

---

### 1.2 Why MongoDB? (Advantages)

| Advantage | Explanation |
|---|---|
| Flexible Schema | Documents in the same collection can have different fields |
| Horizontal Scalability | Sharding distributes data across many servers |
| High Performance | Related data embedded together = fewer joins, faster reads |
| Rich Query Language | Supports filtering, aggregation, geospatial, text search |
| High Availability | Replica sets provide automatic failover |
| Developer Friendly | JSON-like documents map naturally to objects in JS/Python/Java |
| Native Aggregation Framework | Powerful in-database analytics without external ETL |

### 1.3 Disadvantages

- No native multi-collection JOIN performance like SQL (uses `$lookup`, which is comparatively costlier).
- Higher memory usage (WiredTiger cache, indexes).
- Data duplication (due to embedding) increases storage and update complexity.
- Transactions across documents/shards, while supported, add performance overhead.
- Not ideal for highly relational data with many-to-many relationships requiring strict consistency (e.g., complex banking ledgers), though this is mitigated via transactions.

### 1.4 NoSQL vs SQL

| Aspect | SQL (RDBMS) | NoSQL (MongoDB) |
|---|---|---|
| Data Model | Tables, rows, columns | Collections, documents |
| Schema | Fixed, predefined | Dynamic, flexible |
| Relationships | Foreign keys, JOINs | Embedding / Referencing |
| Scaling | Vertical (mostly) | Horizontal (sharding) |
| Query Language | SQL | MQL (MongoDB Query Language) |
| Transactions | Native ACID across tables | ACID at document level; multi-doc via sessions |
| Best For | Structured, relational data | Unstructured/semi-structured, high-velocity data |
| Examples | MySQL, PostgreSQL, Oracle | MongoDB, Cassandra, Couchbase |

> ⚠️ **Common Mistake:** Saying "MongoDB doesn't support transactions." It does — since MongoDB 4.0 (replica sets) and 4.2 (sharded clusters).

### 1.5 Types of NoSQL Databases

| Type | Description | Example |
|---|---|---|
| Document Store | Stores JSON/BSON-like documents | MongoDB, CouchDB |
| Key-Value Store | Simple key → value pairs | Redis, DynamoDB |
| Column-Family Store | Data stored in column families | Cassandra, HBase |
| Graph Database | Nodes & edges for relationships | Neo4j |

### 1.6 History (Quick Facts)

- Developed by **10gen** (later renamed **MongoDB Inc.**), first released in **2009**.
- Name derives from "hu**mongo**us" — reflecting its design goal of handling massive datasets.
- Current storage engine (default since 3.2): **WiredTiger**.

### 1.7 JSON vs BSON

| Aspect | JSON | BSON |
|---|---|---|
| Full Form | JavaScript Object Notation | Binary JSON |
| Format | Text-based | Binary |
| Data Types | Limited (string, number, bool, null, array, object) | Rich (Date, ObjectId, Int32, Int64, Decimal128, Binary, etc.) |
| Parsing Speed | Slower (text parsing) | Faster (binary, traversable) |
| Human Readable | Yes | No |
| Size | Compact for humans | Slightly larger but faster to scan |

> 💡 **Interview Tip:** BSON is used internally by MongoDB for storage and network transfer; JSON is what you see when you `find()` in the shell — the driver converts BSON → JSON-like output for you.

### 1.8 Databases, Collections, Documents — The Hierarchy

```
MongoDB Server (mongod)
 └── Database (e.g., "ecommerce")
      └── Collection (e.g., "products")   ≈ SQL Table
           └── Document (e.g., one product) ≈ SQL Row
                └── Field (e.g., "price")   ≈ SQL Column
```

### 1.9 MongoDB Ecosystem

| Tool | Purpose |
|---|---|
| `mongod` | The core database server process |
| `mongosh` | Modern interactive shell |
| `mongos` | Query router for sharded clusters |
| Compass | Official GUI client |
| Atlas | Fully-managed cloud MongoDB (DBaaS) |
| Mongoose | ODM (Object Document Mapper) for Node.js |
| Realm/Device Sync | Mobile & edge sync (legacy) |

### 1.10 Real-World Use Cases

- **E-commerce:** product catalogs (variable attributes), carts, orders.
- **Social Media:** posts, comments, likes (deeply nested, high write volume).
- **IoT:** sensor time-series data (Time Series collections).
- **Content Management:** blogs, CMS with flexible content types.
- **Gaming:** leaderboards, player profiles.


---

## Section 2: MongoDB Architecture

### 2.1 High-Level Architecture Diagram

```
 ┌────────────┐        ┌──────────────┐        ┌─────────────────────┐
 │  Client App │ ─────▶ │ MongoDB Driver│ ─────▶ │   mongod (Server)   │
 │ (Node/Java) │  MQL   │ (e.g. Node.js)│ Wire   │ ┌──────────────────┐│
 └────────────┘        └──────────────┘ Proto   │ │  Query Engine     ││
                                          ──────▶ │ │  (Parser/Planner) ││
                                                   │ └────────┬─────────┘│
                                                   │          ▼          │
                                                   │ ┌──────────────────┐│
                                                   │ │ Storage Engine    ││
                                                   │ │  (WiredTiger)     ││
                                                   │ └────────┬─────────┘│
                                                   │          ▼          │
                                                   │ ┌──────────────────┐│
                                                   │ │  Disk (Data Files)││
                                                   │ └──────────────────┘│
                                                   └─────────────────────┘
```

### 2.2 Components Explained

| Component | Role |
|---|---|
| **Client** | Application code issuing queries |
| **Driver** | Language-specific library (translates app calls → wire protocol) |
| **mongod** | The database server process that stores & serves data |
| **mongos** | Query router in sharded deployments (routes to correct shard) |
| **Storage Engine** | Manages how data is written to/read from disk (default: WiredTiger) |
| **Config Servers** | Store cluster metadata in sharded setups |

### 2.3 WiredTiger Storage Engine

**Definition:** WiredTiger is MongoDB's default storage engine (since v3.2) responsible for how data is stored, compressed, and cached.

**Key features:**
- **Document-level concurrency control** using MVCC (readers don't block writers, writers don't block readers).
- **Compression:** snappy (default), zlib, or zstd — reduces disk footprint significantly.
- **WiredTiger Cache:** an in-memory cache (default ~50% of RAM minus 1GB) that holds frequently accessed data/indexes.
- **Checkpointing:** flushes in-memory changes to disk every 60 seconds (or when the journal reaches a threshold) to ensure durability.
- **Write-Ahead Journal:** logs writes before applying, enabling crash recovery.

### 2.4 Memory Management

```
┌─────────────────────────────────────┐
│           Total RAM                  │
│  ┌───────────────────────────────┐  │
│  │  WiredTiger Cache (~50%-1GB)   │  │  ← hot data & indexes
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  OS Filesystem Cache            │  │  ← compressed data pages
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  Connections / Other processes  │  │
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘
```

### 2.5 Read Path

1. Query arrives at `mongod` via driver.
2. Query planner checks if a usable index exists.
3. If index found → **IXSCAN** (index scan) narrows candidate documents.
4. If no index → **COLLSCAN** (full collection scan).
5. Data fetched from WiredTiger cache (if present) or disk.
6. Results returned to client (BSON → driver converts to native objects).

### 2.6 Write Path

1. Write request hits `mongod`.
2. Applied to an in-memory copy of the document (via WiredTiger).
3. Recorded in the **journal** (write-ahead log) for durability.
4. Acknowledged based on **write concern** (e.g., `w:1` acks after primary write; `w:"majority"` waits for replica acknowledgment).
5. Periodic checkpoint flushes data to disk (~every 60s).
6. If replicated: change is captured in the **oplog** and shipped to secondaries.

> ⚠️ **Common Mistake:** Assuming a write is "lost" if the server crashes 2 seconds after acknowledging with `w:1`. In a replica set, `w:1` only guarantees primary durability, not replication — this is why `w:"majority"` is recommended for critical writes.

**TCS Interview Perspective:** ⭐⭐⭐⭐ Architecture + WiredTiger + read/write path is a common "explain in depth" question in TCS Prime technical rounds. Practice drawing the diagram on a whiteboard/paper.

---

## Section 3: Documents & Collections

### 3.1 Document

**Definition:** The basic unit of data in MongoDB — an ordered set of key-value pairs, stored as BSON. Equivalent to a "row" in SQL, but far more flexible.

```javascript
{
  _id: ObjectId("64f1..."),
  name: "Dhanussh",
  age: 21,
  skills: ["Node.js", "MongoDB", "React"],
  address: { city: "Chennai", pincode: 600001 }
}
```

- Max document size: **16 MB**.
- Max nesting depth: **100 levels**.
- Every document requires a unique `_id` field (auto-generated `ObjectId` if not provided).

### 3.2 Collection

**Definition:** A group of documents, equivalent to a SQL table, but **schema-less** by default — documents inside one collection can have entirely different structures.

```javascript
db.createCollection("students")
db.students.insertOne({ name: "A", age: 20 })
db.students.insertOne({ name: "B", course: "CS", cgpa: 8.7 }) // different shape — totally valid
```

### 3.3 Dynamic Schema

Because MongoDB doesn't enforce a fixed structure, you can:
- Add new fields to some documents without altering others.
- Store nested objects and arrays of varying depth.
- Optionally enforce structure using **JSON Schema Validation** (`$jsonSchema`) at the collection level.

```javascript
db.createCollection("users", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["email"],
      properties: {
        email: { bsonType: "string", description: "must be a string and is required" }
      }
    }
  }
})
```

### 3.4 Nested Documents & Arrays

```javascript
{
  _id: 1,
  name: "Rahul",
  orders: [                          // array of embedded documents
    { product: "Laptop", qty: 1, price: 55000 },
    { product: "Mouse", qty: 2, price: 500 }
  ],
  address: {                          // embedded object
    street: "MG Road",
    city: "Bangalore"
  }
}
```

> 💡 **Interview Tip:** Interviewers often ask you to *write a query* that reaches into a nested array or object — practice dot notation: `"orders.product"`, `"address.city"`.

**Common Mistakes:**
- Forgetting that array fields create a **multikey index** automatically when indexed.
- Confusing embedded document queries — `find({"address.city": "Bangalore"})` works, but `find({address: {city: "Bangalore"}})` requires an *exact* match of the whole embedded object (including field order in some contexts) — always prefer dot notation for partial matches.

**TCS Interview Perspective:** ⭐⭐⭐⭐ "Difference between Document and Collection" and "Explain nested document querying" are frequent starter-to-intermediate questions.


---

## Section 4: MongoDB CRUD

### 4.1 Sample Collection (used throughout this section)

```javascript
db.employees.insertMany([
  { _id: 1, name: "Arjun", dept: "IT", salary: 55000, city: "Chennai" },
  { _id: 2, name: "Priya", dept: "HR", salary: 48000, city: "Mumbai" },
  { _id: 3, name: "Kiran", dept: "IT", salary: 62000, city: "Chennai" }
])
```

### 4.2 CREATE

#### `insertOne()`
```javascript
db.employees.insertOne({ name: "Sara", dept: "Finance", salary: 51000 })
// Returns: { acknowledged: true, insertedId: ObjectId("...") }
```

#### `insertMany()`
```javascript
db.employees.insertMany([{...}, {...}], { ordered: true })
```
- `ordered: true` (default) — stops at first error.
- `ordered: false` — continues inserting remaining documents even if one fails.

> ⚠️ **Common Mistake:** Assuming `insertMany` with `ordered:false` is always faster and safer — it's faster for bulk loads but you lose the "stop-on-first-error" safety net, so failed documents must be tracked separately from the `writeErrors` array.

### 4.3 READ

#### `find()`
```javascript
db.employees.find({ dept: "IT" })                 // filter
db.employees.find({ dept: "IT" }, { name: 1, _id: 0 }) // filter + projection
```

#### `findOne()`
```javascript
db.employees.findOne({ name: "Arjun" })  // returns single document (or null)
```

| `find()` | `findOne()` |
|---|---|
| Returns a **cursor** (iterate to get docs) | Returns a **single document** (or `null`) |
| Use for multiple results | Use when you expect/need exactly one |

### 4.4 UPDATE

#### `updateOne()`
```javascript
db.employees.updateOne(
  { name: "Arjun" },
  { $set: { salary: 60000 } }
)
```

#### `updateMany()`
```javascript
db.employees.updateMany(
  { dept: "IT" },
  { $inc: { salary: 5000 } }
)
```

#### `replaceOne()`
```javascript
db.employees.replaceOne(
  { name: "Arjun" },
  { name: "Arjun", dept: "IT", salary: 60000 }   // ENTIRE document replaced
)
```

| Method | Behavior |
|---|---|
| `updateOne`/`updateMany` | Modifies **only specified fields** (via operators like `$set`) |
| `replaceOne` | **Replaces the whole document** (except `_id`) — omitted fields are deleted |

> ⚠️ **Common Mistake:** Using `updateOne()` without an update operator: `updateOne({name:"A"}, {salary: 5000})` — MongoDB will throw an error because a plain object without `$` operators is treated as a full replacement document, and without `_id` matching rules this often confuses beginners. Always wrap changes in `$set`.

**Useful update options:**
```javascript
db.employees.updateOne({name:"X"}, {$set:{a:1}}, { upsert: true })  // insert if not found
```

### 4.5 DELETE

```javascript
db.employees.deleteOne({ name: "Sara" })    // deletes first match
db.employees.deleteMany({ dept: "HR" })     // deletes all matches
db.employees.drop()                          // deletes ENTIRE collection (incl. indexes)
```

| Method | Scope |
|---|---|
| `deleteOne` | One document |
| `deleteMany` | All matching documents |
| `drop()` | Entire collection + its indexes (irreversible, very fast — metadata-only op) |

**Follow-up Interview Questions:**
- Q: What does `insertOne()` return? → An object with `acknowledged` and `insertedId`.
- Q: Can `updateMany` use `replaceOne`-style full replacement? → No, `replaceMany` doesn't exist; replace is always single-document.
- Q: Is `deleteMany({})` the same as `drop()`? → Functionally similar (empties the collection) but `drop()` also removes indexes and is much faster for large collections since it's metadata-only.

**TCS Interview Perspective:** ⭐⭐⭐⭐⭐ CRUD syntax + differences (`updateOne` vs `replaceOne`, `deleteMany` vs `drop`) are asked in nearly every TCS Prime round — know exact syntax cold.

---

## Section 5: Query Operators

### 5.1 Comparison Operators

| Operator | Meaning | Example |
|---|---|---|
| `$eq` | Equals | `{ age: { $eq: 25 } }` |
| `$ne` | Not equals | `{ age: { $ne: 25 } }` |
| `$gt` | Greater than | `{ salary: { $gt: 50000 } }` |
| `$gte` | Greater or equal | `{ salary: { $gte: 50000 } }` |
| `$lt` | Less than | `{ salary: { $lt: 50000 } }` |
| `$lte` | Less or equal | `{ salary: { $lte: 50000 } }` |
| `$in` | Value in array | `{ dept: { $in: ["IT","HR"] } }` |
| `$nin` | Value not in array | `{ dept: { $nin: ["IT"] } }` |

```javascript
db.employees.find({ salary: { $gte: 50000, $lte: 70000 } })  // range query
```

### 5.2 Logical Operators

| Operator | Meaning | Example |
|---|---|---|
| `$and` | All conditions true | `{ $and: [{dept:"IT"},{salary:{$gt:50000}}] }` |
| `$or` | Any condition true | `{ $or: [{dept:"IT"},{dept:"HR"}] }` |
| `$not` | Negates a condition | `{ salary: { $not: { $gt: 50000 } } }` |
| `$nor` | None of the conditions true | `{ $nor: [{dept:"IT"},{salary:{$lt:30000}}] }` |

> 💡 **Interview Tip:** `{dept:"IT", salary:{$gt:50000}}` is an **implicit `$and`** — you rarely need explicit `$and` unless combining multiple conditions on the *same field* (e.g., two `$or` clauses).

### 5.3 Element Operators

```javascript
db.employees.find({ bonus: { $exists: true } })   // field is present
db.employees.find({ age: { $type: "int" } })       // field matches BSON type
```

### 5.4 Evaluation Operators

```javascript
db.employees.find({ name: { $regex: "^A", $options: "i" } })  // starts with A, case-insensitive
db.employees.find({ $text: { $search: "developer" } })         // requires a text index
db.employees.find({ $expr: { $gt: ["$salary", "$target"] } })  // compare two fields
```

### 5.5 Array Operators

| Operator | Meaning | Example |
|---|---|---|
| `$all` | Array contains all listed values | `{ tags: { $all: ["node","mongo"] } }` |
| `$size` | Array has exact length | `{ tags: { $size: 3 } }` |
| `$elemMatch` | At least one array element matches ALL conditions | `{ scores: { $elemMatch: { subject:"Math", marks:{$gt:80} } } }` |

> ⚠️ **Common Mistake — `$elemMatch` trap:** Without `$elemMatch`, `find({ scores: { subject: "Math", marks: { $gt: 80 } } })` checks conditions **independently across any elements**, which can match a document even if no *single* element satisfies both. `$elemMatch` forces both conditions onto the **same array element**.

### 5.6 Bitwise Operators (less common, but asked in product companies)

```javascript
db.flags.find({ permissions: { $bitsAllSet: [0, 2] } })  // bits 0 and 2 are set
db.flags.find({ permissions: { $bitsAnySet: [1] } })
```

**TCS Interview Perspective:** ⭐⭐⭐⭐⭐ Comparison/logical operators are near-certain; `$elemMatch` is a favorite "gotcha" question for candidates who claim "advanced MongoDB" on their resume.


---

## Section 6: Projection

**Definition:** Projection controls **which fields** are returned in query results — the second argument to `find()`.

```javascript
db.employees.find({}, { name: 1, salary: 1 })          // inclusion — only name, salary (+_id by default)
db.employees.find({}, { name: 1, salary: 1, _id: 0 })  // exclude _id explicitly
db.employees.find({}, { salary: 0 })                    // exclusion — everything EXCEPT salary
```

> ⚠️ **Rule:** You **cannot mix** inclusion (`1`) and exclusion (`0`) in the same projection, **except** for `_id`, which can always be excluded alongside inclusion fields.

### 6.1 Nested Projection
```javascript
db.employees.find({}, { "address.city": 1 })
```

### 6.2 Array Projection

```javascript
db.employees.find({}, { "orders": { $slice: 2 } })        // first 2 array elements
db.employees.find({ "orders.product": "Laptop" },
                   { "orders.$": 1 })                       // only the matched array element
```

### 6.3 Performance Benefits

- Reduces **network bandwidth** (fewer bytes transferred).
- Reduces **memory usage** on client side.
- Can enable a **Covered Query** (see Section 9) if all projected/filtered fields exist in an index — MongoDB never touches the actual document, only the index.

**TCS Interview Perspective:** ⭐⭐⭐ "Can you mix inclusion and exclusion?" is a classic trick question (answer: only with `_id`).

---

## Section 7: Sorting, Limiting & Pagination

```javascript
db.employees.find().sort({ salary: -1 })          // descending
db.employees.find().sort({ dept: 1, salary: -1 }) // multi-field sort
db.employees.find().limit(5)                       // top 5
db.employees.find().skip(10).limit(5)               // pagination: page 3 (5 per page)
```

### 7.1 Pagination Pattern

```javascript
const page = 3, pageSize = 10;
db.employees.find().sort({ _id: 1 }).skip((page - 1) * pageSize).limit(pageSize);
```

> ⚠️ **Performance Warning:** `skip()` is **O(n)** — MongoDB still scans and discards the skipped documents. For large offsets (e.g., `skip(100000)`), this is slow. Prefer **range/cursor-based pagination**:

```javascript
// Cursor-based pagination (efficient for large datasets)
db.employees.find({ _id: { $gt: lastSeenId } }).sort({ _id: 1 }).limit(10)
```

### 7.2 Top-N Queries

```javascript
db.employees.find().sort({ salary: -1 }).limit(3)   // top 3 highest paid
```

### 7.3 Performance Notes

- `sort()` uses an index if available (avoids in-memory sort, which is capped at 100MB by default unless `allowDiskUse` is used in aggregation).
- Always create an index matching your sort field(s) for large collections.

**TCS Interview Perspective:** ⭐⭐⭐⭐ "How would you implement pagination efficiently?" — mention `skip()`'s O(n) cost and the cursor-based alternative; this differentiates strong candidates.

---

## Section 8: Indexing

### 8.1 What is an Index & Why

**Definition:** An index is a special data structure (B-Tree) that stores a small, ordered portion of the collection's data, allowing MongoDB to find documents **without scanning every document** (COLLSCAN).

**Analogy:** Like a book's index — instead of reading every page to find "MongoDB", you jump straight to the page number.

### 8.2 How MongoDB Indexes Work (B-Tree)

```
                [ 50 ]
              /        \
         [20, 35]      [70, 90]
         /   |   \      /   |   \
      [10][25][40] [60][80][95]
```
- MongoDB indexes are implemented as **B-Trees** (technically B+ Trees in WiredTiger).
- Leaf nodes point to the actual document location (or contain the data itself for covered queries).
- Lookups, insertions, range scans all run in **O(log n)**.

### 8.3 Types of Indexes

| Type | Description | Example |
|---|---|---|
| **Single Field** | Index on one field | `db.employees.createIndex({salary:1})` |
| **Compound** | Index on multiple fields | `db.employees.createIndex({dept:1, salary:-1})` |
| **Multikey** | Auto-created when indexing an array field | `db.products.createIndex({tags:1})` |
| **Unique** | Enforces uniqueness | `db.users.createIndex({email:1},{unique:true})` |
| **Sparse** | Only indexes documents where the field exists | `db.users.createIndex({phone:1},{sparse:true})` |
| **TTL** | Auto-deletes documents after a time period | `db.sessions.createIndex({createdAt:1},{expireAfterSeconds:3600})` |
| **Hashed** | Hashes field value — used for sharding | `db.users.createIndex({userId:"hashed"})` |
| **Text** | Enables full-text search | `db.articles.createIndex({content:"text"})` |
| **Wildcard** | Indexes all fields (or subset) dynamically | `db.products.createIndex({"$**":1})` |
| **Hidden** | Index exists but query planner ignores it (for testing removal safely) | `db.employees.hideIndex("salary_1")` |
| **Partial** | Indexes only documents matching a filter | `createIndex({salary:1},{partialFilterExpression:{salary:{$gt:50000}}})` |

### 8.4 Compound Index & Index Prefix

```javascript
db.employees.createIndex({ dept: 1, salary: -1, city: 1 })
```

This single compound index can serve queries on:
- `{dept}` ✅ (leftmost prefix)
- `{dept, salary}` ✅
- `{dept, salary, city}` ✅
- `{salary}` alone ❌ (not a prefix)
- `{city}` alone ❌

> 💡 **Index Prefix Rule:** A compound index can support queries on any **left-to-right prefix** of its fields, not arbitrary subsets.

### 8.5 Cardinality & Selectivity

- **Cardinality:** number of distinct values a field can have (e.g., `gender` = low cardinality, `email` = high cardinality).
- **Selectivity:** how well a query condition narrows down results. High-selectivity fields (like `email`, unique IDs) make excellent index candidates; low-selectivity fields (like `boolean` flags) make poor standalone indexes.

### 8.6 Index Intersection

MongoDB *can* use two separate single-field indexes together (intersecting their results) if no suitable compound index exists — but a well-designed compound index is almost always faster.

### 8.7 Covered Query

**Definition:** A query where **all fields** requested (in filter + projection) are present in the index itself — MongoDB never needs to fetch the actual document from disk.

```javascript
db.employees.createIndex({ dept: 1, salary: 1 })
db.employees.find({ dept: "IT" }, { dept: 1, salary: 1, _id: 0 })  // ✅ COVERED
```
> Requires `_id` to be explicitly excluded (unless `_id` is also part of the index).

**Performance Considerations:**
- Every index **speeds up reads** but **slows down writes** (each insert/update must also update all relevant indexes).
- Indexes consume RAM — too many indexes can push useful data out of the WiredTiger cache.
- Rule of thumb: index fields that are frequently queried, sorted, or used in `$match`/`$lookup`, not every field.

> ⚠️ **Common Mistake:** Creating a separate index for every field "just in case." This bloats write latency and memory. Follow the **ESR Rule** (Section 10) for compound index design instead.

**TCS Interview Perspective:** ⭐⭐⭐⭐⭐ Indexing is one of the **most-asked topics** — expect at least 2–3 questions: types of indexes, compound index prefix rule, and covered queries.


---

## Section 9: Query Optimization & explain()

### 9.1 `explain()`

```javascript
db.employees.find({ dept: "IT" }).explain("executionStats")
```

**Three verbosity modes:**
| Mode | Info Shown |
|---|---|
| `"queryPlanner"` (default) | Chosen plan only, no execution |
| `"executionStats"` | Chosen plan + actual runtime stats (docs examined, time) |
| `"allPlansExecution"` | Stats for **all** candidate plans considered |

### 9.2 Key Output Fields

| Field | Meaning |
|---|---|
| `winningPlan` | The plan MongoDB actually chose |
| `stage` | `COLLSCAN` (full scan) or `IXSCAN` (index scan) or `FETCH` (fetching full doc after index scan) |
| `nReturned` | Documents returned |
| `totalDocsExamined` | Documents scanned |
| `totalKeysExamined` | Index keys scanned |
| `executionTimeMillis` | Time taken |

> 💡 **Golden Ratio to check:** If `totalDocsExamined` ≈ `nReturned`, your query is efficient. If `totalDocsExamined` >> `nReturned`, you're scanning way more than needed — add/fix an index.

### 9.3 COLLSCAN vs IXSCAN

```
COLLSCAN: scans every document in the collection  → O(n), slow on large collections
IXSCAN:   traverses the B-Tree index               → O(log n) + fetch matched docs
```

### 9.4 Covered Query (recap from Section 8)

A covered query shows `"stage": "PROJECTION_COVERED"` in `explain()` output, with **no `FETCH` stage** — meaning MongoDB served the query entirely from the index.

### 9.5 Query Optimization Checklist

1. Run `explain("executionStats")` — check for `COLLSCAN`.
2. Ensure filter fields are indexed (prefer compound indexes over multiple single-field indexes).
3. Use projection to limit returned fields (may enable covered queries).
4. Apply `$match` as early as possible in aggregation pipelines.
5. Avoid `$regex` starting with a wildcard (`/.*abc/`) — it can't use an index prefix efficiently; regex indexes only help with **anchored** patterns (`^abc`).
6. Avoid **negation operators** (`$ne`, `$nin`) on indexed fields where possible — they can't leverage the index as effectively (must scan the range around the excluded value).

> ⚠️ **Common Mistake:** Adding an index and assuming performance is automatically fixed, without verifying with `explain()` that the planner actually **picked** that index (sometimes the query shape doesn't match the index, so it's silently ignored).

**TCS Interview Perspective:** ⭐⭐⭐⭐⭐ "How do you optimize a slow query?" is a **guaranteed** scenario question — always answer with the `explain()` → identify COLLSCAN → add index → re-verify workflow.

---

## Section 10: The ESR Rule

**Definition:** ESR = **Equality, Sort, Range** — the recommended field ordering when designing a compound index for queries that combine equality filters, sorting, and range filters.

```
E → Equality fields first   (exact match, e.g., {dept: "IT"})
S → Sort fields next         (fields used in .sort())
R → Range fields last         (e.g., {salary: {$gt: 50000}})
```

### 10.1 Why This Order?

- **Equality** fields narrow the B-Tree to a small, exact sub-tree instantly.
- **Sort** fields, if placed right after equality fields in the index, let MongoDB return results **already sorted** — no in-memory sort needed.
- **Range** fields go last because a range scan can't narrow down as precisely as equality, and placing it early would break the "already sorted" benefit for later fields.

### 10.2 Example

Query:
```javascript
db.orders.find({ status: "shipped" })
          .sort({ orderDate: -1 })
          .find({ amount: { $gt: 1000 } })
```
Equivalent combined filter:
```javascript
db.orders.find({ status: "shipped", amount: { $gt: 1000 } }).sort({ orderDate: -1 })
```

**Best index (ESR order):**
```javascript
db.orders.createIndex({ status: 1, orderDate: -1, amount: 1 })
//                       ↑ Equality   ↑ Sort         ↑ Range
```

> ⚠️ **Tricky Question:** "Why not put Range before Sort?" — If Range comes before Sort in the index, MongoDB narrows to a range of index entries first, but those entries are **not contiguous in sort order** for the sort field, forcing an expensive in-memory sort. ESR order avoids this.

**Interview Follow-ups:**
- Q: Does ESR order matter for `_id`? → `_id` is a separate default index; ESR applies when *you* design compound indexes.
- Q: What if there's no Sort in the query? → Just use **Equality → Range** order.

**TCS Interview Perspective:** ⭐⭐⭐⭐⭐ ESR Rule is a favorite "advanced" question used to separate junior from strong candidates — memorize the E-S-R acronym and be ready to justify the ordering, not just recite it.


---

## Section 11: Aggregation Framework

### 11.1 What is the Aggregation Pipeline

**Definition:** A framework for processing documents through a sequence of **stages**, each transforming the data and passing it to the next — similar to a Unix pipe (`|`).

```
Collection → [$match] → [$group] → [$sort] → [$project] → Result
```

### 11.2 Sample Collection

```javascript
db.orders.insertMany([
  { _id:1, customer:"A", amount:500, status:"delivered", date: ISODate("2024-01-05") },
  { _id:2, customer:"B", amount:1200, status:"delivered", date: ISODate("2024-01-12") },
  { _id:3, customer:"A", amount:300, status:"cancelled", date: ISODate("2024-02-01") },
  { _id:4, customer:"C", amount:900, status:"delivered", date: ISODate("2024-02-10") }
])
```

### 11.3 Core Stages

#### `$match` — filters documents (like `find()`)
```javascript
{ $match: { status: "delivered" } }
```

#### `$group` — groups documents & computes aggregates
```javascript
{ $group: { _id: "$customer", total: { $sum: "$amount" }, count: { $sum: 1 } } }
```

#### `$project` — reshapes documents
```javascript
{ $project: { customer: 1, amount: 1, year: { $year: "$date" } } }
```

#### `$sort`, `$limit`, `$skip`
```javascript
{ $sort: { total: -1 } }, { $limit: 5 }, { $skip: 10 }
```

#### `$count`
```javascript
{ $count: "totalOrders" }
```

#### `$unwind` — deconstructs an array field into multiple documents
```javascript
// { _id:1, items:["pen","book"] } → becomes 2 documents
{ $unwind: "$items" }
```

#### `$lookup` — join with another collection (see Section 12)

#### `$facet` — runs multiple pipelines in parallel, returns combined results
```javascript
{
  $facet: {
    byStatus: [{ $group: { _id: "$status", count: { $sum: 1 } } }],
    topOrders: [{ $sort: { amount: -1 } }, { $limit: 3 }]
  }
}
```

#### `$bucket` / `$bucketAuto` — groups documents into ranges (histograms)
```javascript
{
  $bucket: {
    groupBy: "$amount",
    boundaries: [0, 500, 1000, 1500],
    default: "Other",
    output: { count: { $sum: 1 } }
  }
}
```

#### `$sample` — random sampling
```javascript
{ $sample: { size: 3 } }
```

#### `$replaceRoot` / `$replaceWith` — promotes an embedded doc to top level
```javascript
{ $replaceRoot: { newRoot: "$address" } }
```

#### `$addFields` — adds computed fields (keeps existing fields)
```javascript
{ $addFields: { totalWithTax: { $multiply: ["$amount", 1.18] } } }
```

#### `$unset` — removes fields (aggregation equivalent of exclusion projection)
```javascript
{ $unset: ["internalNotes", "_v"] }
```

#### `$merge` / `$out` — write pipeline results to a collection
```javascript
{ $merge: { into: "customerTotals", whenMatched: "replace" } }
{ $out: "summaryCollection" }
```
| `$out` | `$merge` |
|---|---|
| Overwrites the entire target collection | Merges/updates specific documents |
| Target collection must be in same DB | Can target a different DB (same cluster) |

### 11.4 Full Example: Total Delivered Amount Per Customer, Sorted

```javascript
db.orders.aggregate([
  { $match: { status: "delivered" } },
  { $group: { _id: "$customer", totalSpent: { $sum: "$amount" }, orders: { $sum: 1 } } },
  { $sort: { totalSpent: -1 } },
  { $project: { _id: 0, customer: "$_id", totalSpent: 1, orders: 1 } }
])
```
**Expected Output:**
```javascript
[
  { customer: "B", totalSpent: 1200, orders: 1 },
  { customer: "C", totalSpent: 900, orders: 1 },
  { customer: "A", totalSpent: 500, orders: 1 }
]
```

### 11.5 Aggregation Pipeline Diagram

```
┌──────────┐   ┌────────┐   ┌────────┐   ┌────────┐   ┌─────────┐
│ orders   │──▶│ $match │──▶│ $group │──▶│ $sort  │──▶│ $project │──▶ Result
│(4 docs)  │   │(filter)│   │(reduce)│   │(order) │   │(reshape) │
└──────────┘   └────────┘   └────────┘   └────────┘   └─────────┘
```

### 11.6 Performance Tips

- Place `$match` (and `$sort` if it can use an index) **as early as possible** — reduces documents flowing through later stages.
- `$match` at the start of a pipeline **can use indexes**; `$match` after `$group`/`$project` cannot.
- Use `$project`/`$unset` early to drop unneeded large fields before expensive stages like `$lookup`.
- Use `allowDiskUse: true` for pipelines exceeding the 100MB in-memory limit per stage.
- Prefer `$group` with `_id: null` only when you truly need a single overall aggregate — grouping unnecessarily is costly.

> ⚠️ **Common Mistake:** Writing `$project` before `$match` when the projected fields aren't needed for filtering — this forces MongoDB to reshape *every* document before discarding most of them. Filter first, reshape later.

**Interview Follow-ups:**
- Q: Difference between `find()` and `aggregate()`? → `find()` retrieves/filters documents; `aggregate()` can filter, transform, group, join, and reshape data in a multi-stage pipeline.
- Q: Can aggregation use indexes? → Yes, primarily in `$match` and `$sort` stages when they're early in the pipeline.

**TCS Interview Perspective:** ⭐⭐⭐⭐⭐ The Aggregation Framework is **the single most tested topic** in mid-to-senior MongoDB rounds. Be ready to write a `$match → $group → $sort` pipeline from scratch on a whiteboard/notepad.


---

## Section 12: $lookup (Joins)

**Definition:** `$lookup` performs a **left outer join** between two collections in the same database — for every document in the input collection, it attaches matching documents from the "foreign" collection.

### 12.1 Basic Syntax (Equality Join)

```javascript
db.orders.aggregate([
  {
    $lookup: {
      from: "customers",       // foreign collection
      localField: "customerId", // field in orders
      foreignField: "_id",      // field in customers
      as: "customerInfo"        // output array field
    }
  }
])
```

**Sample Output:**
```javascript
{
  _id: 1, customerId: 101, amount: 500,
  customerInfo: [ { _id: 101, name: "Priya", city: "Mumbai" } ]  // always an ARRAY
}
```

> 💡 To flatten to a single object (one-to-one), follow with `$unwind: "$customerInfo"`.

### 12.2 One-to-One vs One-to-Many

| Relationship | Behavior |
|---|---|
| One-to-One | `customerInfo` array has 0 or 1 elements — usually `$unwind`ed |
| One-to-Many | `customerInfo` array can have multiple elements (e.g., all orders for a customer) |

### 12.3 Pipeline Lookup (Advanced — with conditions)

```javascript
db.orders.aggregate([
  {
    $lookup: {
      from: "customers",
      let: { custId: "$customerId" },
      pipeline: [
        { $match: { $expr: { $eq: ["$_id", "$$custId"] } } },
        { $match: { active: true } },          // extra condition, not possible in basic $lookup
        { $project: { name: 1, _id: 0 } }
      ],
      as: "customerInfo"
    }
  }
])
```
Use pipeline-style `$lookup` when you need **filtering, projection, or multiple conditions** on the joined collection — plain `localField/foreignField` only supports equality.

### 12.4 Nested Lookup

```javascript
{ $lookup: { from: "products", localField: "items.productId", foreignField: "_id", as: "productDetails" } }
```
`$lookup` can also be chained (lookup → unwind → lookup again) to join across 3+ collections.

### 12.5 Performance Considerations

- `$lookup` is **expensive** — index the `foreignField` in the joined collection to speed it up.
- Place `$match` **before** `$lookup` to reduce the number of documents that need joining.
- For very large joined datasets, consider **denormalizing (embedding)** frequently-joined, rarely-changing data instead.

> ⚠️ **Common Mistake:** Forgetting that `$lookup` output is always an **array**, and then trying to access fields directly (`customerInfo.name`) instead of `customerInfo[0].name` or unwinding first.

**TCS Interview Perspective:** ⭐⭐⭐⭐⭐ "Write a query to join two collections" is one of the most common **live coding** asks in TCS Prime/Digital rounds. Practice `$lookup` + `$unwind` combo until it's muscle memory.

---

## Section 13: Embedding vs Referencing

### 13.1 Embedding (Denormalization)

```javascript
// Embedded — blog post with comments inside
{
  _id: 1,
  title: "MongoDB Basics",
  comments: [
    { user: "A", text: "Great post!" },
    { user: "B", text: "Very helpful" }
  ]
}
```

### 13.2 Referencing (Normalization)

```javascript
// Referenced — separate collections linked by ID
// posts collection
{ _id: 1, title: "MongoDB Basics", authorId: 501 }
// authors collection
{ _id: 501, name: "Dhanussh", bio: "..." }
```

### 13.3 Decision Table

| Factor | Embed When... | Reference When... |
|---|---|---|
| Relationship | One-to-few, tightly coupled | One-to-many/many-to-many, large or unbounded |
| Read Pattern | Data is always read together | Data is read independently |
| Update Frequency | Sub-document rarely updated | Sub-document updated often/independently |
| Data Growth | Bounded (won't exceed 16MB doc limit) | Unbounded (e.g., millions of comments) |
| Data Duplication | Acceptable / desired for speed | Must avoid duplication |
| Example | User + Address, Order + OrderItems | Blog Post + (huge) Comments, Student + Enrolled Courses |

### 13.4 Advantages & Disadvantages

| | Embedding | Referencing |
|---|---|---|
| **Pros** | Single query reads everything; atomic updates; no joins needed | No data duplication; smaller documents; independent scaling |
| **Cons** | Data duplication; risk of hitting 16MB limit; harder to update shared data | Requires `$lookup`/multiple queries; more complex application logic |

### 13.5 Real-World Examples

- **Embed:** A user's shipping address inside their profile (small, rarely queried separately).
- **Reference:** Products in an e-commerce order — you reference `productId` rather than embedding the full (changeable) product document, so price/name updates don't require touching every historical order... 

  *(Exception: for historical orders you often **embed a snapshot** of price/name at time of purchase — this is the classic "extended reference" pattern.)*

### 13.6 Hybrid Pattern (Extended Reference)

```javascript
// order embeds a SNAPSHOT of key product fields + a reference for full lookup
{
  _id: 1,
  items: [
    { productId: 501, name: "iPhone 15", priceAtPurchase: 79900 }
  ]
}
```
This avoids extra `$lookup` calls for common display fields while still keeping `productId` for full product lookups when needed.

**Interview Follow-ups:**
- Q: What happens if an embedded array grows unbounded? → Risk of exceeding the 16MB document limit and degraded read/write performance (the whole document is rewritten on update). Use referencing or bucketing instead.
- Q: Is embedding always faster? → For reads, usually yes (single query). For writes to shared/duplicated data, no — it requires updating every copy.

**TCS Interview Perspective:** ⭐⭐⭐⭐⭐ "When would you embed vs reference?" is asked in almost every MongoDB-focused interview — always answer with a **concrete example**, not just the theory.


---

## Section 14: Data Modeling & Schema Design

### 14.1 Relationship Patterns

#### One-to-One
```javascript
// Embed (most common)
{ _id:1, name:"Dhanussh", profile: { bio:"...", avatar:"..." } }
```

#### One-to-Many (bounded — embed)
```javascript
{ _id:1, name:"Order#1", items:[{product:"Pen",qty:2},{product:"Book",qty:1}] }
```

#### One-to-Many (unbounded — reference)
```javascript
// author collection
{ _id:501, name:"Dhanussh" }
// posts collection (many posts reference one author)
{ _id:1, title:"Post A", authorId:501 }
```

#### Many-to-Many
```javascript
// students reference courses AND courses reference students (or use a junction collection)
{ _id:1, name:"Rahul", courseIds:[101,102] }
{ _id:101, title:"DBMS", studentIds:[1,2,3] }
```

### 14.2 Tree / Category Structures

**Parent Reference Pattern:**
```javascript
{ _id:"electronics", parent:null }
{ _id:"mobiles", parent:"electronics" }
{ _id:"iphones", parent:"mobiles" }
```

**Materialized Path Pattern (fast subtree queries):**
```javascript
{ _id:"iphones", path:",electronics,mobiles,iphones," }
// query all descendants of electronics:
db.categories.find({ path: /,electronics,/ })
```

**Array of Ancestors Pattern:**
```javascript
{ _id:"iphones", ancestors:["electronics","mobiles"] }
```

### 14.3 Real-World Schema Designs

#### E-commerce
```javascript
// products (referenced from orders)
{ _id: 101, name:"iPhone 15", price:79900, category:"mobiles" }
// orders (embed line-item snapshot, reference customer)
{ _id: 1, customerId: 501, items:[{productId:101,name:"iPhone 15",price:79900,qty:1}], total:79900, status:"placed" }
```

#### Social Media (Instagram-style)
```javascript
// posts — embed a LIMITED number of recent comments, reference the rest
{
  _id: 1, userId: 501, imageUrl:"...",
  likesCount: 1200,
  recentComments: [ {userId:502, text:"Nice!"} ],   // embed latest 3-5
  commentCount: 340
}
// full comments in separate collection, paginated by postId
```

#### Banking / Transactions
```javascript
// accounts (balance must be strongly consistent → use transactions)
{ _id:"ACC001", balance: 50000 }
// transactions (append-only ledger, referenced by accountId)
{ _id:1, accountId:"ACC001", type:"debit", amount:5000, date:ISODate() }
```

#### Student Management System
```javascript
{ _id:1, name:"Rahul", rollNo:"CS101", department:"CSE",
  enrolledCourses:[{courseId:101, grade:"A"}],
  attendance: { present: 85, total: 90 } }
```

#### Library System
```javascript
// books (reference author, embed copies availability)
{ _id:1, title:"Clean Code", authorId:501, totalCopies:5, availableCopies:2 }
// borrow records (reference book + member)
{ _id:1, bookId:1, memberId:201, borrowDate:ISODate(), returnDate:null }
```

### 14.4 Schema Design Anti-Patterns (avoid these)

| Anti-Pattern | Why It's Bad | Fix |
|---|---|---|
| Massive unbounded arrays | Hits 16MB limit, slow updates | Reference + separate collection |
| Bloated documents with rarely-used fields | Wastes cache memory | Split into separate collection (attribute pattern) |
| Too many collections for simple 1:1 data | Unnecessary `$lookup` overhead | Embed instead |
| Indexing everything | Slows writes, wastes RAM | Index only what queries actually need |
| Using `$lookup` for every read | Defeats MongoDB's performance advantage | Denormalize hot-read data |

**Interview Follow-ups:**
- Q: How would you design a WhatsApp-style chat schema? → Reference `conversationId` in a `messages` collection (unbounded, high write volume), embed the last message preview in the `conversations` collection for fast chat-list rendering.
- Q: How do you avoid the 16MB limit for a post with millions of comments? → Reference comments in a separate collection, paginate by `postId` + timestamp index, optionally embed only the most recent N comments in the post for quick display (hybrid pattern).

**TCS Interview Perspective:** ⭐⭐⭐⭐⭐ Schema design questions are the **capstone** of MongoDB interviews at TCS Digital/Prime — always explain your **reasoning** (embed vs reference decision) rather than just drawing a schema.

---

## Section 15: Replication

### 15.1 What is a Replica Set

**Definition:** A group of `mongod` instances maintaining the **same dataset**, providing high availability and automatic failover.

```
                ┌────────────┐
        writes  │  PRIMARY   │
      ─────────▶│ (accepts   │
                │  R & W)    │
                └─────┬──────┘
                       │ oplog replication
           ┌───────────┴───────────┐
           ▼                       ▼
   ┌───────────────┐      ┌───────────────┐
   │  SECONDARY 1   │      │  SECONDARY 2   │
   │ (read-only,    │      │ (read-only,    │
   │  replicates)   │      │  replicates)   │
   └───────────────┘      └───────────────┘
```

### 15.2 Roles

| Role | Description |
|---|---|
| **Primary** | Accepts all writes; only one primary at a time |
| **Secondary** | Replicates data from primary via the **oplog**; can serve reads if configured |
| **Arbiter** | Participates in elections (votes) but holds **no data** — used to break ties with even node counts |

### 15.3 Election & Failover

- If the primary becomes unreachable (heartbeat timeout, default 10s), remaining nodes hold an **election**.
- A secondary with the most up-to-date oplog data and majority votes becomes the new primary.
- Requires a **majority** of voting members to elect — hence odd numbers of members (or an arbiter) are recommended.

### 15.4 Read Preference

| Mode | Behavior |
|---|---|
| `primary` (default) | All reads from primary — strongest consistency |
| `primaryPreferred` | Primary if available, else secondary |
| `secondary` | Always read from secondary — reduces primary load, may return stale data |
| `secondaryPreferred` | Secondary if available, else primary |
| `nearest` | Lowest network latency member, regardless of role |

### 15.5 Write Concern

```javascript
db.orders.insertOne({...}, { writeConcern: { w: "majority", j: true, wtimeout: 5000 } })
```
| Option | Meaning |
|---|---|
| `w: 1` | Acknowledged by primary only |
| `w: "majority"` | Acknowledged by majority of replica set members (durable against failover) |
| `j: true` | Written to the on-disk journal before acknowledging |
| `wtimeout` | Max time to wait for the requested acknowledgment |

> ⚠️ **Common Mistake:** Using `w:1` for critical financial writes — if the primary crashes before replicating, that write can be **rolled back** after failover. Use `w:"majority"` for anything that must survive a failover.

**TCS Interview Perspective:** ⭐⭐⭐⭐ Explain replica set architecture + failover process confidently; "What is an Arbiter and why use one?" is a common follow-up.

---

## Section 16: Sharding

### 16.1 What is Sharding

**Definition:** MongoDB's method of **horizontal scaling** — splitting a large dataset across multiple servers (**shards**), each holding a subset of the data.

```
                     ┌────────────┐
   Client ──────────▶│   mongos    │  (query router)
                     └──────┬─────┘
                             │
          ┌──────────────────┼──────────────────┐
          ▼                  ▼                   ▼
   ┌─────────────┐   ┌─────────────┐    ┌─────────────┐
   │   Shard 1    │   │   Shard 2    │    │   Shard 3    │
   │(replica set) │   │(replica set) │    │(replica set) │
   └─────────────┘   └─────────────┘    └─────────────┘
          ▲
          │  metadata
   ┌─────────────┐
   │Config Servers│  (store cluster metadata: which shard has which chunk)
   └─────────────┘
```

### 16.2 Key Concepts

| Term | Meaning |
|---|---|
| **Shard Key** | The field(s) used to distribute documents across shards — chosen at collection creation, hard to change later |
| **Chunk** | A contiguous range of shard-key values; the unit of data migrated between shards |
| **Balancer** | Background process that moves chunks to keep shards evenly loaded |
| **Config Servers** | Store metadata about which chunks live on which shards (themselves a replica set) |
| **mongos** | Stateless query router that clients connect to; routes queries to the correct shard(s) |

### 16.3 Choosing a Good Shard Key

- Should have **high cardinality** (many distinct values).
- Should distribute writes **evenly** (avoid monotonically increasing keys like `_id`/timestamp alone → causes "hot shard" problem where all new writes go to one shard).
- Should match common query patterns (**targeted queries** hit one shard; queries without the shard key become **scatter-gather**, hitting all shards — slow).

> ⚠️ **Common Mistake:** Using a monotonically increasing field (like `createdAt` or default `ObjectId`) as the sole shard key — all new documents route to the same (last) chunk, creating a **hot shard** bottleneck. Use a **compound** or **hashed** shard key instead.

### 16.4 Advantages & Disadvantages

| Advantages | Disadvantages |
|---|---|
| Near-limitless horizontal scaling | Increased operational complexity |
| Distributes read/write load | Cross-shard queries/joins are slower |
| Improves availability (failure isolation per shard) | Choosing a bad shard key is hard to fix later |
| Handles datasets larger than any single server's capacity | Transactions across shards have more overhead |

**Interview Follow-ups:**
- Q: Difference between replication and sharding? → Replication = **copies** of the same data for availability; Sharding = **partitions** of different data for scalability. They're often combined (each shard is itself a replica set).
- Q: What is a scatter-gather query? → A query without the shard key, forcing `mongos` to query every shard and merge results — much slower than a targeted single-shard query.

**TCS Interview Perspective:** ⭐⭐⭐⭐ Sharding is more common in **product-based** company interviews but still shows up in TCS Digital's advanced rounds — know the shard key hot-spot problem cold, it's the #1 follow-up.


---

## Section 17: Transactions

### 17.1 ACID in MongoDB

| Property | How MongoDB Guarantees It |
|---|---|
| **Atomicity** | Single document writes are always atomic; multi-document transactions (v4.0+) make a group of ops all-or-nothing |
| **Consistency** | Documents always satisfy schema validators (if defined) and index constraints after a commit |
| **Isolation** | Transactions use **snapshot isolation** — reads within a transaction see a consistent snapshot |
| **Durability** | Committed writes are journaled and (with `w:"majority"`) replicated before acknowledgment |

### 17.2 Using Sessions & Transactions (Node.js example)

```javascript
const session = client.startSession();
try {
  session.startTransaction();

  await accounts.updateOne({ _id: "A" }, { $inc: { balance: -500 } }, { session });
  await accounts.updateOne({ _id: "B" }, { $inc: { balance: 500 } }, { session });

  await session.commitTransaction();
} catch (err) {
  await session.abortTransaction();
  throw err;
} finally {
  session.endSession();
}
```

### 17.3 Commit / Abort / Rollback

- **Commit:** All operations in the transaction are applied atomically.
- **Abort:** All operations are discarded — as if none happened.
- **Rollback:** Happens automatically if a transaction fails or is explicitly aborted; also occurs during replica set failover for unacknowledged/non-majority writes.

### 17.4 Distributed Transactions (Sharded Clusters)

- Supported since MongoDB **4.2**.
- Uses a **two-phase commit** protocol internally across shards, coordinated via `mongos`.
- Higher latency than single-shard transactions — use only when truly necessary (e.g., cross-shard financial transfers).

### 17.5 Performance Considerations

- Transactions hold locks and resources longer than single-document ops — keep them **short** and **avoid unnecessary reads/writes** inside them.
- Default transaction timeout is 60 seconds (`transactionLifetimeLimitSeconds`).
- Prefer **document-level atomicity** (single-document updates with `$inc`, `$set`, etc.) whenever possible — it's faster and doesn't need a transaction at all.

> ⚠️ **Common Mistake:** Reaching for multi-document transactions by default (SQL habit). In MongoDB, good schema design (embedding related data in one document) often **eliminates the need for transactions** entirely.

**TCS Interview Perspective:** ⭐⭐⭐⭐ "Does MongoDB support transactions?" + "When would you use one?" — answer: yes since 4.0, but prefer schema design (embedding) to avoid needing them when possible.

---

## Section 18: Atomicity

### 18.1 Document-Level Atomicity

**Definition:** All updates to a **single document** (even affecting multiple fields/array elements) are atomic by default — no transaction needed.

```javascript
// This entire update is atomic — either all fields change or none do
db.accounts.updateOne(
  { _id: "A" },
  { $inc: { balance: -500 }, $push: { history: { type: "debit", amount: 500 } } }
)
```

### 18.2 Why This Matters

Because MongoDB guarantees document-level atomicity, a well-embedded schema (e.g., an order with embedded line items) can achieve transactional guarantees **without** the overhead of `startTransaction()`.

### 18.3 Multi-Document Atomicity → Transactions

For updates spanning **multiple documents or collections** (e.g., debit account A, credit account B), you need explicit **multi-document transactions** (Section 17) to get all-or-nothing behavior.

```
┌─────────────────────────┐     ┌──────────────────────────┐
│  Single Document Update  │     │  Multi-Document Update    │
│  → Always atomic          │     │  → Needs a transaction     │
│  (no extra code needed)   │     │  (session + commit/abort)  │
└─────────────────────────┘     └──────────────────────────┘
```

**TCS Interview Perspective:** ⭐⭐⭐ "Is a single `updateOne()` atomic?" — Yes, always, even with multiple field updates in one call. This is a common trick question testing whether you conflate document-level atomicity with the need for transactions.

---

## Section 19: Performance Optimization

### 19.1 Checklist for a High-Performance MongoDB App

| Area | Optimization |
|---|---|
| **Indexes** | Index fields used in `$match`/`find`/`sort`; follow ESR rule; avoid over-indexing |
| **Projection** | Only fetch fields you need — reduces I/O and network transfer |
| **Aggregation** | `$match` and `$project` early; avoid unnecessary `$lookup`; use `allowDiskUse` for big pipelines |
| **Schema** | Embed for read-heavy, bounded relationships; reference for write-heavy/unbounded |
| **Connection Pooling** | Reuse a single MongoClient/connection pool across the app (never open a new connection per request) |
| **Bulk Operations** | Use `bulkWrite()` for many writes instead of looping individual `insertOne`/`updateOne` calls |
| **Caching** | Use Redis/in-memory cache for hot, rarely-changing data to reduce DB load |
| **Avoid Anti-Patterns** | No unbounded arrays, no massive documents, no `$lookup` in hot paths |

### 19.2 Bulk Write Example

```javascript
db.employees.bulkWrite([
  { insertOne: { document: { name: "X", dept: "IT" } } },
  { updateOne: { filter: { name: "Arjun" }, update: { $set: { salary: 65000 } } } },
  { deleteOne: { filter: { name: "OldEmp" } } }
])
```
Bulk operations reduce network round-trips — a single call instead of N separate calls.

### 19.3 Connection Pooling (Node.js)

```javascript
// ✅ Create ONE client, reuse across the app
const client = new MongoClient(uri, { maxPoolSize: 50 });
await client.connect();
// pass `client` around / export the db instance — never re-instantiate per request
```

> ⚠️ **Common Mistake:** Creating a new `MongoClient` connection on every API request — exhausts connections and adds massive latency. Always use a shared, pooled client (singleton pattern).

**TCS Interview Perspective:** ⭐⭐⭐⭐ Performance checklist questions ("How would you optimize a slow MongoDB app?") are common scenario questions — structure your answer around: **Indexes → Query Design → Schema → Connection Handling**.


---

## Section 20: Mongoose

**Definition:** Mongoose is an **ODM** (Object Document Mapper) for Node.js that provides schema enforcement, validation, middleware, and a convenient query API on top of the native MongoDB driver.

### 20.1 Schema & Model

```javascript
const mongoose = require("mongoose");

const employeeSchema = new mongoose.Schema({
  name: { type: String, required: true, trim: true },
  dept: { type: String, enum: ["IT", "HR", "Finance"] },
  salary: { type: Number, min: 0 },
  createdAt: { type: Date, default: Date.now }
});

const Employee = mongoose.model("Employee", employeeSchema); // model = collection wrapper
```

| Schema | Model |
|---|---|
| Blueprint defining structure, types, validation | The actual constructor/class used to create, query & save documents based on the schema |

### 20.2 Validation

```javascript
name: { type: String, required: [true, "Name is required"] },
email: { type: String, match: /^\S+@\S+\.\S+$/ },
age: { type: Number, min: 18, max: 60 }
```

### 20.3 Middleware (Hooks)

```javascript
employeeSchema.pre("save", function(next) {
  this.name = this.name.trim();
  next();
});

employeeSchema.post("save", function(doc) {
  console.log(`Saved employee: ${doc.name}`);
});
```
Common hooks: `pre("save")`, `pre("find")`, `pre("remove")`, `post("save")`, etc. — useful for hashing passwords, logging, cascading deletes.

### 20.4 Populate (Reference Resolution)

```javascript
const orderSchema = new mongoose.Schema({
  customer: { type: mongoose.Schema.Types.ObjectId, ref: "Customer" },
  amount: Number
});

const order = await Order.findOne({ _id: 1 }).populate("customer");
// order.customer is now the full Customer document, not just an ObjectId
```

| `$lookup` (native) | `populate()` (Mongoose) |
|---|---|
| Runs inside the DB as an aggregation stage — single round trip | Runs as a **separate query** from the app (usually 2 queries) — more app-side overhead but simpler syntax |
| Better performance for large-scale joins | More convenient for typical CRUD apps |

### 20.5 Virtuals

```javascript
employeeSchema.virtual("annualSalary").get(function() {
  return this.salary * 12;
});
// NOT stored in DB — computed on the fly when accessed
```

### 20.6 Methods & Statics

```javascript
employeeSchema.methods.getSummary = function() {           // instance method
  return `${this.name} - ${this.dept}`;
};
employeeSchema.statics.findByDept = function(dept) {         // model-level method
  return this.find({ dept });
};
```

### 20.7 Discriminators (Schema Inheritance)

```javascript
const baseOptions = { discriminatorKey: "type" };
const Event = mongoose.model("Event", new mongoose.Schema({ time: Date }, baseOptions));
const ClickEvent = Event.discriminator("Click", new mongoose.Schema({ url: String }));
// Both stored in the same "events" collection, differentiated by "type" field
```

**Interview Follow-ups:**
- Q: `save()` vs `create()`? → `new Model(data).save()` creates an instance then saves it (2 steps, allows pre-save manipulation); `Model.create(data)` does both in one call.
- Q: Does Mongoose enforce schema at the database level? → No — validation happens in the **application layer** (Node.js); MongoDB itself remains schema-flexible unless you also add `$jsonSchema` validators at the DB level.

> ⚠️ **Common Mistake:** Assuming Mongoose validation protects data inserted via the native driver, other services, or `mongosh` directly — it doesn't; only writes going through Mongoose are validated.

**TCS Interview Perspective:** ⭐⭐⭐⭐⭐ Since most TCS Prime candidates list "MERN stack" on their resume, expect deep Mongoose questions: schema vs model, populate vs lookup, middleware, and validation are all near-certain.

---

## Section 21: MongoDB + Node.js

### 21.1 Native Driver Connection

```javascript
const { MongoClient } = require("mongodb");
const client = new MongoClient(process.env.MONGO_URI, { maxPoolSize: 20 });

async function connectDB() {
  await client.connect();
  console.log("MongoDB connected");
  return client.db("myapp");
}
```

### 21.2 Connection Pool

- The driver maintains a **pool of TCP connections** (default `maxPoolSize: 100`) reused across queries — avoids the overhead of opening/closing a connection per request.
- Always instantiate `MongoClient` **once** at app startup, not per-request.

### 21.3 Error Handling

```javascript
try {
  const result = await db.collection("employees").insertOne(doc);
} catch (err) {
  if (err.code === 11000) {
    console.error("Duplicate key error:", err.keyValue);
  } else {
    console.error("DB error:", err.message);
  }
}
```

### 21.4 Async/Await Best Practices

```javascript
// ✅ Good — proper error propagation with try/catch + async/await
async function getEmployee(id) {
  try {
    return await db.collection("employees").findOne({ _id: id });
  } catch (err) {
    throw new Error(`Failed to fetch employee: ${err.message}`);
  }
}
```

### 21.5 Repository Pattern

```javascript
class EmployeeRepository {
  constructor(db) { this.collection = db.collection("employees"); }
  findById(id) { return this.collection.findOne({ _id: id }); }
  create(data) { return this.collection.insertOne(data); }
  update(id, data) { return this.collection.updateOne({ _id: id }, { $set: data }); }
  delete(id) { return this.collection.deleteOne({ _id: id }); }
}
```
Encapsulates DB logic away from route handlers/controllers — improves testability and separation of concerns (common in production Node.js + MongoDB architectures).

### 21.6 Transactions in Node.js (recap from Section 17)

```javascript
const session = client.startSession();
await session.withTransaction(async () => {
  await accounts.updateOne({ _id: "A" }, { $inc: { balance: -500 } }, { session });
  await accounts.updateOne({ _id: "B" }, { $inc: { balance: 500 } }, { session });
});
session.endSession();
```
`withTransaction()` automatically handles commit/retry/abort logic — preferred over manual `startTransaction/commitTransaction/abortTransaction` in most Node.js apps.

**Interview Follow-ups:**
- Q: What happens if you don't await an async DB call? → It returns a pending Promise immediately; the function continues without the data, commonly causing `undefined` bugs or race conditions.
- Q: How do you prevent connection leaks in Node.js + MongoDB? → Use a single shared client/pool, never call `client.close()` per-request, and always release resources (`session.endSession()`) in `finally` blocks.

**TCS Interview Perspective:** ⭐⭐⭐⭐ Given your MERN background, expect practical questions here: "How do you structure a Node + MongoDB backend?" — mention connection pooling, repository pattern, and proper async error handling.


---

## Section 22: Query Practice Bank

> This section curates the **highest-yield** query-writing questions asked in TCS Prime/Digital rounds — covering CRUD, aggregation, and array manipulation. Each includes a problem, sample data, query, output, and interview notes.
> **Shared sample collection** (`employees`) unless stated otherwise:
> ```javascript
> [
>   {_id:1,name:"Arjun",dept:"IT",salary:55000,city:"Chennai",skills:["Node","Mongo"]},
>   {_id:2,name:"Priya",dept:"HR",salary:48000,city:"Mumbai",skills:["Excel"]},
>   {_id:3,name:"Kiran",dept:"IT",salary:62000,city:"Chennai",skills:["React","Node"]},
>   {_id:4,name:"Sara", dept:"IT",salary:62000,city:"Delhi", skills:["Java"]},
>   {_id:5,name:"Vikram",dept:"Finance",salary:70000,city:"Mumbai",skills:["Excel","SQL"]}
> ]
> ```

**Q1. Find the highest-paid employee.**
```javascript
db.employees.find().sort({ salary: -1 }).limit(1)
```
*Optimized:* `db.employees.aggregate([{$sort:{salary:-1}},{$limit:1}])` (same cost; create `{salary:-1}` index for large datasets).

**Q2. Find the 2nd highest salary (distinct).**
```javascript
db.employees.aggregate([
  { $group: { _id: "$salary" } },
  { $sort: { _id: -1 } },
  { $skip: 1 },
  { $limit: 1 }
])
```
*Explanation:* `$group` deduplicates salaries first (handles ties like Kiran & Sara both at 62000 correctly — 2nd **distinct** salary is 55000, not another 62000).

**Q3. Find the Nth highest salary (parameterized).**
```javascript
const N = 3;
db.employees.aggregate([
  { $group: { _id: "$salary" } },
  { $sort: { _id: -1 } },
  { $skip: N - 1 },
  { $limit: 1 }
])
```

**Q4. Find duplicate records (same salary appearing more than once).**
```javascript
db.employees.aggregate([
  { $group: { _id: "$salary", count: { $sum: 1 }, ids: { $push: "$_id" } } },
  { $match: { count: { $gt: 1 } } }
])
```
**Expected Output:** `{ _id: 62000, count: 2, ids: [3, 4] }`

**Q5. Get distinct department values.**
```javascript
db.employees.distinct("dept")   // → ["IT", "HR", "Finance"]
```

**Q6. Average salary per department.**
```javascript
db.employees.aggregate([
  { $group: { _id: "$dept", avgSalary: { $avg: "$salary" } } },
  { $sort: { avgSalary: -1 } }
])
```

**Q7. Count employees per department.**
```javascript
db.employees.aggregate([ { $group: { _id: "$dept", count: { $sum: 1 } } } ])
```

**Q8. Employees who know both "Node" and "React".**
```javascript
db.employees.find({ skills: { $all: ["Node", "React"] } })
```
**Expected Output:** Kiran (`_id:3`).

**Q9. Employees with exactly 2 skills.**
```javascript
db.employees.find({ skills: { $size: 2 } })
```

**Q10. Top 2 highest-paid employees per department (bucketed ranking).**
```javascript
db.employees.aggregate([
  { $sort: { dept: 1, salary: -1 } },
  { $group: { _id: "$dept", topEmployees: { $push: { name: "$name", salary: "$salary" } } } },
  { $project: { topEmployees: { $slice: ["$topEmployees", 2] } } }
])
```

**Q11. Running total of salaries (ordered by `_id`).**
```javascript
db.employees.aggregate([
  { $sort: { _id: 1 } },
  { $group: { _id: null, all: { $push: { id: "$_id", salary: "$salary" } } } },
  { $unwind: { path: "$all", includeArrayIndex: "idx" } },
  { $group: { _id: null, docs: { $push: "$all" } } }
])
// Simpler, MongoDB 5.0+: use $setWindowFields
db.employees.aggregate([
  { $setWindowFields: {
      sortBy: { _id: 1 },
      output: { runningTotal: { $sum: "$salary", window: { documents: ["unbounded", "current"] } } }
  }}
])
```
*Interview Tip:* Mentioning `$setWindowFields` (MongoDB 5.0+) for running totals/ranking impresses interviewers — it replaces clunky manual `$unwind`/`$reduce` tricks.

**Q12. Employees earning above department average.**
```javascript
db.employees.aggregate([
  { $group: { _id: "$dept", avgSalary: { $avg: "$salary" }, docs: { $push: "$$ROOT" } } },
  { $unwind: "$docs" },
  { $match: { $expr: { $gt: ["$docs.salary", "$avgSalary"] } } },
  { $replaceRoot: { newRoot: "$docs" } }
])
```

**Q13. Latest N orders (by date).**
```javascript
db.orders.find().sort({ orderDate: -1 }).limit(5)
```

**Q14. Monthly sales totals.**
```javascript
db.orders.aggregate([
  { $group: {
      _id: { year: { $year: "$orderDate" }, month: { $month: "$orderDate" } },
      totalSales: { $sum: "$amount" }
  }},
  { $sort: { "_id.year": 1, "_id.month": 1 } }
])
```

**Q15. Top 3 customers by total spend.**
```javascript
db.orders.aggregate([
  { $group: { _id: "$customerId", totalSpent: { $sum: "$amount" } } },
  { $sort: { totalSpent: -1 } },
  { $limit: 3 }
])
```

**Q16. Full-text search on a field.**
```javascript
db.articles.createIndex({ content: "text" })
db.articles.find({ $text: { $search: "mongodb performance" } })
```

**Q17. Regex search — names starting with "A", case-insensitive.**
```javascript
db.employees.find({ name: { $regex: "^A", $options: "i" } })
```

**Q18. Update a nested field.**
```javascript
db.employees.updateOne(
  { _id: 1 },
  { $set: { "address.city": "Coimbatore" } }
)
```

**Q19. Add an element to an array field (avoiding duplicates).**
```javascript
db.employees.updateOne({ _id: 1 }, { $addToSet: { skills: "Docker" } })
```

**Q20. Remove an element from an array field.**
```javascript
db.employees.updateOne({ _id: 1 }, { $pull: { skills: "Excel" } })
```

**Q21. Remove (delete) a nested field entirely.**
```javascript
db.employees.updateOne({ _id: 1 }, { $unset: { "address.pincode": "" } })
```

**Q22. Increment a numeric field atomically (e.g., stock decrement).**
```javascript
db.products.updateOne({ _id: 501, stock: { $gte: 1 } }, { $inc: { stock: -1 } })
```
*Interview Tip:* Including `stock: { $gte: 1 }` in the filter prevents stock from going negative — a classic **atomic guard condition** pattern asked in e-commerce scenario questions.

**Q23. Paginate results (page 2, 10 per page).**
```javascript
db.employees.find().sort({ _id: 1 }).skip(10).limit(10)
```

**Q24. Find employees in a list of cities.**
```javascript
db.employees.find({ city: { $in: ["Chennai", "Mumbai"] } })
```

**Q25. Group employees by city and list their names.**
```javascript
db.employees.aggregate([
  { $group: { _id: "$city", employees: { $push: "$name" } } }
])
```

**Q26. Find employees whose salary is between two values.**
```javascript
db.employees.find({ salary: { $gte: 50000, $lte: 65000 } })
```

**Q27. Complex aggregation — department-wise salary stats (min/max/avg/count) sorted.**
```javascript
db.employees.aggregate([
  { $group: {
      _id: "$dept",
      minSalary: { $min: "$salary" },
      maxSalary: { $max: "$salary" },
      avgSalary: { $avg: "$salary" },
      count: { $sum: 1 }
  }},
  { $sort: { avgSalary: -1 } }
])
```

**Q28. Join orders with customers and filter by customer city (pipeline lookup).**
```javascript
db.orders.aggregate([
  { $lookup: {
      from: "customers",
      localField: "customerId",
      foreignField: "_id",
      as: "customer"
  }},
  { $unwind: "$customer" },
  { $match: { "customer.city": "Chennai" } }
])
```

**Q29. Find and remove exact duplicate documents (keep one copy).**
```javascript
db.employees.aggregate([
  { $group: { _id: "$email", ids: { $push: "$_id" }, count: { $sum: 1 } } },
  { $match: { count: { $gt: 1 } } }
]).forEach(doc => {
  doc.ids.shift();               // keep the first _id
  db.employees.deleteMany({ _id: { $in: doc.ids } });
})
```

**Q30. Case-insensitive exact match using collation (better than regex for performance).**
```javascript
db.employees.find({ name: "arjun" }).collation({ locale: "en", strength: 2 })
```
*Performance Note:* Collation-based case-insensitive search **can use an index** built with the same collation — regex-based `$options:"i"` searches generally cannot use an index efficiently.

**TCS Interview Perspective:** ⭐⭐⭐⭐⭐ Q1–Q4 (highest/Nth salary, duplicates) are asked in **almost every** TCS Prime technical round — know these five cold, they map directly from classic SQL interview questions.


---

## Section 23: TCS Prime Rapid-Fire Q&A Bank

> 50 high-frequency questions in rapid-fire table format for quick revision. **Difficulty:** B=Beginner, I=Intermediate, A=Advanced. **Importance:** ⭐ (1–5).

| # | Question | Expected Answer (Core Idea) | Follow-up | Diff | Imp |
|---|---|---|---|---|---|
| 1 | Why MongoDB over SQL? | Flexible schema, horizontal scaling, natural fit for JSON/object data | When would you still pick SQL? (strong relational integrity, complex joins) | B | ⭐⭐⭐⭐⭐ |
| 2 | Why BSON over JSON? | Binary format = faster parsing, richer types (Date, ObjectId, Decimal128) | Is BSON human-readable? (No) | B | ⭐⭐⭐⭐ |
| 3 | What is WiredTiger? | Default storage engine; handles compression, caching, MVCC concurrency | What compression algo is default? (snappy) | I | ⭐⭐⭐⭐ |
| 4 | What is ObjectId? | 12-byte unique identifier: 4-byte timestamp + 5-byte random + 3-byte counter | Is ObjectId sequential/sortable by time? (Roughly yes, via its timestamp prefix) | B | ⭐⭐⭐⭐⭐ |
| 5 | How does MongoDB store data on disk? | As BSON documents in collections, managed by WiredTiger, compressed & journaled | What ensures durability? (Journal + checkpoints) | I | ⭐⭐⭐ |
| 6 | SQL vs MongoDB? | Tables/rows vs Collections/documents; fixed vs flexible schema; JOIN vs embed/$lookup | Is MongoDB ACID compliant? (Yes, doc-level always, multi-doc via transactions) | B | ⭐⭐⭐⭐⭐ |
| 7 | Collection vs Table? | Collection = group of documents (schema-flexible); Table = rows with fixed schema | Can two documents in one collection differ in structure? (Yes) | B | ⭐⭐⭐⭐ |
| 8 | Embedding vs Referencing? | Embed for tightly-coupled/bounded data; reference for large/independent/unbounded data | Give a real example of each | I | ⭐⭐⭐⭐⭐ |
| 9 | What is Aggregation? | Pipeline of stages transforming documents (filter, group, reshape, join) | Difference from `find()`? | I | ⭐⭐⭐⭐⭐ |
| 10 | `find()` vs `aggregate()`? | find = simple filter/projection; aggregate = multi-stage data processing pipeline | Can aggregate replace find? (Yes, `$match` alone ≈ find) | B | ⭐⭐⭐⭐ |
| 11 | What is `explain()`? | Shows the query execution plan — index used, docs scanned, timing | Which mode shows actual runtime stats? (`executionStats`) | I | ⭐⭐⭐⭐⭐ |
| 12 | What is a Covered Query? | Query answered entirely from the index, no document fetch needed | What's required? (All filter+projected fields in the index) | A | ⭐⭐⭐⭐ |
| 13 | What is the ESR Rule? | Compound index field order: Equality → Sort → Range | Why not Range before Sort? (breaks index-order sorting) | A | ⭐⭐⭐⭐⭐ |
| 14 | What is Projection? | Selecting which fields to return from a query | Can you mix inclusion & exclusion? (No, except `_id`) | B | ⭐⭐⭐⭐ |
| 15 | What is a Replica Set? | Group of mongod nodes maintaining the same data for HA & failover | What is an Arbiter? (Votes in elections, holds no data) | I | ⭐⭐⭐⭐ |
| 16 | What is Sharding? | Horizontal partitioning of data across multiple servers via a shard key | What's a "hot shard"? (Uneven load from a poor shard key choice) | A | ⭐⭐⭐⭐ |
| 17 | What is a Transaction? | Multi-document, all-or-nothing operation with ACID guarantees | Since which version? (4.0 replica sets, 4.2 sharded) | I | ⭐⭐⭐⭐ |
| 18 | `updateOne()` vs `replaceOne()`? | update modifies specified fields; replace overwrites the entire document | What happens to unlisted fields in replaceOne? (Removed) | B | ⭐⭐⭐⭐⭐ |
| 19 | `deleteMany({})` vs `drop()`? | Both empty the collection; drop() also removes indexes & is much faster (metadata op) | Which is faster for huge collections? (drop()) | I | ⭐⭐⭐⭐ |
| 20 | What is Populate (Mongoose)? | Resolves a referenced ObjectId into the full document via a separate query | Is it as fast as $lookup? (No — extra round trip) | I | ⭐⭐⭐⭐ |
| 21 | Schema vs Model (Mongoose)? | Schema = structure/validation blueprint; Model = usable class built from schema | Can one schema have multiple models? (Not directly; use discriminators) | B | ⭐⭐⭐⭐ |
| 22 | `save()` vs `create()` (Mongoose)? | save() on an instance (2 steps); create() does new+save in one call | Which allows pre-save hooks before persisting? (Both do — hooks fire either way) | I | ⭐⭐⭐ |
| 23 | `$push` vs `$addToSet`? | push always appends; addToSet only appends if the value doesn't already exist | Which prevents array duplicates? (`$addToSet`) | B | ⭐⭐⭐⭐ |
| 24 | `$unset` vs `$pull`? | unset removes a *field*; pull removes matching *array elements* | Can $pull remove based on a condition? (Yes, e.g. `$pull:{scores:{$lt:40}}`) | I | ⭐⭐⭐⭐ |
| 25 | `remove()` vs `deleteOne()`? | remove() is deprecated/legacy; deleteOne/deleteMany are the modern, explicit API | Should new code use remove()? (No) | B | ⭐⭐⭐ |
| 26 | What is `$lookup`? | Performs a left outer join between two collections in an aggregation pipeline | Is the output always an array? (Yes) | I | ⭐⭐⭐⭐⭐ |
| 27 | `$lookup` vs `populate()`? | $lookup runs server-side in one query; populate runs as a separate app-side query | Which scales better for huge datasets? ($lookup, generally) | A | ⭐⭐⭐⭐ |
| 28 | Index Scan vs Collection Scan? | IXSCAN uses the B-Tree index (fast); COLLSCAN reads every document (slow) | How do you detect a COLLSCAN? (via `explain()`) | B | ⭐⭐⭐⭐⭐ |
| 29 | What is a Compound Index? | Index on multiple fields together, supporting queries on left-to-right prefixes | Does field order matter? (Yes — critically) | I | ⭐⭐⭐⭐⭐ |
| 30 | What is a Multikey Index? | Auto-created index type when indexing a field containing an array | Can you compound-index two array fields together? (No — not allowed) | A | ⭐⭐⭐ |
| 31 | What is a TTL Index? | Automatically deletes documents after a specified number of seconds | Can it be on any field? (Must be a Date field) | I | ⭐⭐⭐⭐ |
| 32 | What is a Sparse Index? | Only indexes documents where the indexed field actually exists | Why use it? (Saves space when many docs lack the field) | I | ⭐⭐⭐ |
| 33 | What is a Partial Index? | Indexes only documents matching a specified filter expression | Difference from Sparse? (Partial = any custom condition, not just field existence) | A | ⭐⭐⭐ |
| 34 | What is $elemMatch used for? | Matches array elements that satisfy multiple conditions on the SAME element | What's the trap without it? (Conditions may match across different elements) | A | ⭐⭐⭐⭐ |
| 35 | What is the WiredTiger cache? | In-memory cache (~50% RAM−1GB) holding hot data & indexes for fast access | What happens on cache miss? (Reads from disk, slower) | A | ⭐⭐⭐ |
| 36 | What is the oplog? | A capped collection logging all writes on the primary, used to replicate to secondaries | Where does it live? (local database, `oplog.rs` collection) | A | ⭐⭐⭐ |
| 37 | Read Preference options? | primary, primaryPreferred, secondary, secondaryPreferred, nearest | Which reduces primary load but risks stale reads? (secondary) | I | ⭐⭐⭐ |
| 38 | Write Concern `w:"majority"`? | Waits for acknowledgment from a majority of replica set members before confirming | Why prefer it for critical writes? (Survives failover without rollback) | A | ⭐⭐⭐⭐ |
| 39 | What is a Shard Key? | Field(s) used to distribute documents across shards | What makes a bad shard key? (Low cardinality or monotonically increasing) | A | ⭐⭐⭐⭐ |
| 40 | What is `$facet`? | Runs multiple aggregation sub-pipelines in parallel, combining results into one document | When is it useful? (e.g., paginated results + total count in one query) | I | ⭐⭐⭐⭐ |
| 41 | What is `$unwind`? | Deconstructs an array field into one document per element | What happens with an empty array by default? (Document is dropped unless `preserveNullAndEmptyArrays:true`) | I | ⭐⭐⭐⭐ |
| 42 | `$match` placement in aggregation? | Should be placed as early as possible to reduce docs flowing downstream & use indexes | Can $match after $group use an index? (No) | I | ⭐⭐⭐⭐ |
| 43 | What is Document-Level Atomicity? | All fields/operators within one `updateOne()` call apply atomically | Does it apply across multiple documents? (No — needs a transaction) | I | ⭐⭐⭐⭐ |
| 44 | What does `upsert:true` do? | Inserts a new document if no match is found, otherwise updates the match | Is the inserted doc's shape based on filter+update? (Yes) | B | ⭐⭐⭐⭐ |
| 45 | Max document size in MongoDB? | 16 MB | Why this limit? (Prevents excessive memory usage for a single doc in transit) | B | ⭐⭐⭐⭐ |
| 46 | What is a capped collection? | Fixed-size collection that overwrites oldest documents when full (FIFO) | Real use case? (Logging, oplog itself) | A | ⭐⭐⭐ |
| 47 | What is `$merge` vs `$out`? | $merge updates/merges into a target collection; $out fully overwrites it | Which can target a different database? (`$merge`) | A | ⭐⭐⭐ |
| 48 | What is `allowDiskUse`? | Aggregation option letting stages spill to disk beyond the 100MB memory limit | When is it needed? (Large `$sort`/`$group` on big datasets) | I | ⭐⭐⭐ |
| 49 | What is a Hashed Index used for? | Distributing writes evenly — commonly used as a sharding shard key | Can it support range queries? (No, only equality) | A | ⭐⭐⭐ |
| 50 | Why avoid `skip()` for deep pagination? | It's O(n) — scans & discards skipped docs, slow at large offsets | What's the better alternative? (Range/cursor-based pagination using `_id` or a sort field) | I | ⭐⭐⭐⭐⭐ |

**TCS Interview Perspective:** ⭐⭐⭐⭐⭐ These 50 cover roughly **80% of actual TCS Prime MongoDB questions** reported by past candidates. Drill this table the night before your interview.


---

## Section 24: Scenario-Based Schema Design Questions

> For each: the core design decision + a minimal schema sketch. In interviews, always **narrate your reasoning** (embed vs reference, indexing choices) rather than just presenting the final schema.

**1. Design YouTube (Videos + Comments + Views)**
```javascript
// videos — reference channel, embed lightweight stats
{ _id:1, title:"...", channelId:501, views:1200000, likes:45000, uploadDate:ISODate() }
// comments — separate collection (unbounded), indexed by videoId + timestamp
{ _id:1, videoId:1, userId:201, text:"Great video!", createdAt:ISODate() }
```
*Reasoning:* Comments are unbounded and high-write → reference, not embed. View/like counters are embedded and incremented atomically (`$inc`) for speed.

**2. Design WhatsApp Chat**
```javascript
// conversations — embed last message preview for fast chat-list load
{ _id:1, members:[101,102], lastMessage:{text:"See you!",sentAt:ISODate()} }
// messages — separate collection, reference conversationId, indexed on (conversationId, sentAt)
{ _id:1, conversationId:1, senderId:101, text:"See you!", sentAt:ISODate(), status:"delivered" }
```
*Reasoning:* Messages are unbounded/high-volume → referenced. `lastMessage` embedded in `conversations` avoids querying the huge `messages` collection just to render a chat list.

**3. Design Instagram Posts**
```javascript
{ _id:1, userId:501, imageUrl:"...", caption:"...", likesCount:1200,
  recentComments:[{userId:502,text:"🔥"}], commentCount:340, createdAt:ISODate() }
// full comments in a separate "comments" collection, paginated by postId
```
*Reasoning:* Hybrid pattern — embed a handful of recent comments for instant display, reference the rest for scale.

**4. Design Banking Transactions**
```javascript
{ _id:"ACC001", balance:50000, ownerId:301 }                 // accounts
{ _id:1, accountId:"ACC001", type:"debit", amount:5000, date:ISODate() } // append-only ledger
```
*Reasoning:* Balance updates use `$inc` (atomic); transfers between accounts use **multi-document transactions** for strict consistency; ledger is append-only and referenced (never embedded — unbounded history).

**5. Design a Library System**
```javascript
{ _id:1, title:"Clean Code", authorId:501, totalCopies:5, availableCopies:2 }   // books
{ _id:1, bookId:1, memberId:201, borrowDate:ISODate(), returnDate:null }         // borrow records
```
*Reasoning:* `availableCopies` is decremented atomically on borrow (`$inc` with a `$gte:1` guard); borrow history referenced for unbounded growth.

**6. Design a College ERP**
```javascript
{ _id:1, name:"Rahul", rollNo:"CS101", dept:"CSE",
  enrolledCourses:[{courseId:101,grade:"A"}], attendance:{present:85,total:90} }  // students
{ _id:101, title:"DBMS", facultyId:301, credits:4 }                               // courses
```
*Reasoning:* Bounded course enrollment list → embed. Faculty/course master data referenced since it's shared across many students.

**7. Design an E-commerce Platform**
```javascript
{ _id:101, name:"iPhone 15", price:79900, category:"mobiles", stock:50 }         // products
{ _id:1, customerId:501, items:[{productId:101,name:"iPhone 15",price:79900,qty:1}],
  total:79900, status:"placed", createdAt:ISODate() }                              // orders
```
*Reasoning:* Order line items embed a **price/name snapshot** (extended reference) so historical orders remain accurate even if the product price changes later.

**8. Design an HR Portal (Employee + Payroll)**
```javascript
{ _id:1, name:"Arjun", dept:"IT", designation:"SDE-2", managerId:5 }             // employees
{ _id:1, employeeId:1, month:"2024-07", basic:50000, deductions:2000, netPay:48000 } // payroll (referenced, monthly records)
```
*Reasoning:* Payroll grows monthly per employee (unbounded over years) → separate, referenced, indexed on `(employeeId, month)`.

**9. Design an Attendance System**
```javascript
{ _id:1, employeeId:1, date:ISODate("2024-07-01"), status:"present", checkIn:"09:05" }
```
*Reasoning:* One document per employee per day → naturally unbounded over time, referenced collection, compound index `(employeeId, date)` for fast lookups & the ESR rule in reporting queries.

**10. Design an Inventory Management System**
```javascript
{ _id:501, sku:"SKU-1001", name:"Widget A", stock:120, warehouseId:9 }           // products
{ _id:1, productId:501, change:-5, reason:"sale", timestamp:ISODate() }           // stock movement log (referenced)
```
*Reasoning:* Current `stock` embedded for fast reads (updated via `$inc`); full movement history referenced (audit trail, unbounded).

**11. Design a Ride-Sharing App (Uber-style)**
```javascript
{ _id:1, riderId:101, driverId:501, status:"in_progress", pickup:{lat:12.9,lng:77.6}, fare:250 } // rides
// driver location updates — separate collection, high write frequency, TTL index to expire stale pings
{ driverId:501, location:{type:"Point",coordinates:[77.6,12.9]}, updatedAt:ISODate() }
```
*Reasoning:* Live location pings are extremely high-write and short-lived → separate collection with a **geospatial (2dsphere) index** + TTL index, decoupled from the ride record.

**12. Design a Hospital Management System**
```javascript
{ _id:1, name:"Patient X", age:45, admittedRecords:[{diagnosis:"Fever",date:ISODate()}] }  // patients (bounded embed)
{ _id:1, patientId:1, doctorId:301, prescription:"...", date:ISODate() }                    // consultations (referenced, unbounded)
```
*Reasoning:* A short embedded medical summary for quick profile view; detailed consultation history referenced since it grows indefinitely and is queried independently (e.g., by doctor).

**TCS Interview Perspective:** ⭐⭐⭐⭐⭐ Scenario design questions test **judgment**, not memorization — always state your embed/reference reasoning out loud, mention which fields you'd index, and flag where you'd use a transaction.


---

## Section 25: Tricky Questions

> These are the "gotcha" questions interviewers use to separate candidates who memorized definitions from those who truly understand MongoDB.

**1. Embedding vs Referencing — "Just embed everything for speed, right?"**
Wrong. Unbounded embedding risks hitting the 16MB doc limit and causes expensive full-document rewrites on every update. Embed only bounded, tightly-coupled data.

**2. `find()` vs `findOne()` — "Are they equally efficient for a single result?"**
`find().limit(1)` and `findOne()` perform similarly, but `findOne()` is more idiomatic/readable when you expect exactly one result.

**3. `save()` vs `create()` (Mongoose) — "Which is faster?"**
Negligible difference; `create()` is more concise for new documents, `save()` is needed when you must mutate/inspect an instance before persisting.

**4. `deleteMany()` vs `drop()` — "Are they interchangeable?"**
No — `drop()` also removes all indexes on the collection; recreate indexes if you `drop()` and plan to reuse the collection.

**5. `replaceOne()` vs `updateOne()` — "What happens to fields not mentioned?"**
`replaceOne` **deletes** any field not in the replacement document (except `_id`); `updateOne` with `$set` leaves untouched fields alone.

**6. Projection Trap — "Can I include and exclude fields together?"**
Only `_id` can be excluded while other fields are included; mixing any other inclusion/exclusion in one projection throws an error.

**7. `$lookup` Performance — "Is `$lookup` as fast as a SQL JOIN?"**
Generally no — it's an aggregation stage, not a native relational join; always index the `foreignField` and place `$match` before `$lookup` to minimize cost.

**8. Aggregation Pitfall — "Does `$match` after `$group` use an index?"**
No — once documents pass through `$group`, they're new synthetic documents disconnected from any collection index.

**9. TTL Index — "Does it delete documents exactly at the expiry second?"**
No — a background task runs every ~60 seconds, so actual deletion can lag by up to a minute.

**10. Text Index — "Can I have more than one text index per collection?"**
No — only **one** text index is allowed per collection (though it can cover multiple fields).

**11. Sparse Index — "Does a sparse index skip documents with the field set to `null`?"**
No — it skips documents where the field **doesn't exist at all**; a field explicitly set to `null` IS indexed.

**12. Unique Index — "Does a unique index allow multiple documents missing the field?"**
By default, **no** — multiple docs without the field are treated as having `null`, which violates uniqueness after the first. Combine with `sparse:true` to allow multiple missing values.

**13. Partial Index — "Is it the same as a Sparse index?"**
No — sparse only checks field *existence*; partial can filter on **any** expression (e.g., `salary: {$gt: 50000}`), making it strictly more flexible.

**14. ESR Rule — "Why not just index every field used in the query, in query order?"**
Field *order in the query* doesn't matter; what matters is the ESR structure — putting Range before Sort breaks the index's ability to serve pre-sorted results.

**15. Covered Query — "If I project a field not in the index, is it still covered?"**
No — **every** field in both the filter and the projection must exist in the index, or MongoDB must `FETCH` the full document, breaking coverage.

**16. ObjectId Ordering — "Is ObjectId guaranteed globally strictly increasing?"**
Not strictly — it's roughly time-ordered (second-level timestamp precision) but multiple ObjectIds generated in the same second aren't guaranteed to sort exactly by creation order.

**17. Atomicity — "Is a single `updateOne()` with 5 different `$set` fields atomic?"**
Yes — all field changes within one document-level operation are always atomic, transaction or not.

**18. Transactions — "Do transactions replace good schema design?"**
No — MongoDB's philosophy favors embedding related data to avoid needing transactions at all; transactions are a safety net for genuinely cross-document operations, not a default tool.

**19. Populate vs Lookup — "Is `populate()` a database-level join?"**
No — it's an **application-level convenience** that issues a second query using the driver; `$lookup` executes server-side within a single aggregation call.

**20. `$ne`/`$nin` on an indexed field — "Does MongoDB use the index efficiently?"**
Partially — it can use the index but must scan a wider range (everything except the excluded value), making it less selective than equality queries.

**21. Multikey Index — "Can you create a compound index on two array fields?"**
No — MongoDB disallows compound indexes with more than one array (multikey) field, to avoid a combinatorial explosion of index entries.

**22. `$elemMatch` — "Is it needed for querying a single scalar array (not objects)?"**
Only needed when you have **multiple conditions** that must match the **same element**; for simple value matching (`tags:"node"`), it's unnecessary.

**23. `_id` field — "Can you change it after insertion?"**
No — `_id` is immutable once set; to "change" it you must delete and re-insert with a new `_id`.

**24. Read Preference — "Does reading from `secondary` guarantee up-to-date data?"**
No — secondaries can lag behind the primary (replication lag), so `secondary` reads risk staleness; use `secondary` only when eventual consistency is acceptable.

**25. Write Concern — "Does `w:1` mean the write is durable?"**
It means the primary acknowledged it — but if the primary crashes before replicating, that write can be **rolled back** during failover. Use `w:"majority"` for durability guarantees.

**26. Sharding — "Can you change the shard key after data is loaded?"**
Historically very difficult (required manual re-sharding); MongoDB 5.0+ introduced `reshardCollection` to make this more feasible, but it's still a heavy operation — choose your shard key carefully upfront.

**27. Aggregation `$group` with `_id: null` — "What does it do?"**
Groups **all** documents in the pipeline into a single result — useful for overall totals/averages across the entire (filtered) collection.

**28. `$unwind` on an empty array — "What happens by default?"**
The document is **dropped** from the output entirely, unless you set `preserveNullAndEmptyArrays: true`.

**29. Explain() — "Does `explain()` actually execute the query and modify data?"**
`queryPlanner` mode does **not** execute; `executionStats`/`allPlansExecution` **do execute** the query (read-only, so no data is modified) to gather real runtime numbers.

**30. Capped Collections — "Can you delete individual documents from a capped collection?"**
No — you cannot manually `deleteOne()`/`deleteMany()` from a capped collection (only automatic FIFO eviction or `drop()` the whole collection).

**TCS Interview Perspective:** ⭐⭐⭐⭐⭐ These tricky questions are exactly where interviewers **catch surface-level knowledge**. Read through this list twice — once to learn, once right before your interview.

---

## Section 26: Common Errors & Fixes

| Error Category | Example | Cause | Fix |
|---|---|---|---|
| **Connection Errors** | `MongoServerSelectionError: connect ECONNREFUSED` | Wrong URI, DB not running, IP not whitelisted (Atlas) | Verify connection string, check Atlas Network Access, ensure `mongod` is running |
| **Duplicate Key Error** | `E11000 duplicate key error collection: db.users index: email_1` | Inserting a value that violates a unique index | Check for existing record first, or handle the error (`err.code === 11000`) gracefully |
| **Validation Errors** | `Document failed validation` | Insert/update violates `$jsonSchema` validator or Mongoose schema rules | Fix the document to match required fields/types, or relax the validator |
| **Aggregation Errors** | `Exceeded memory limit for $group` | Pipeline stage exceeds 100MB in-memory limit | Add `{ allowDiskUse: true }` to the aggregate() options |
| **Lookup Errors** | `$lookup 'from' field must be a string referring to a collection` | Misconfigured `$lookup` stage (typo in field names, wrong collection name) | Double-check `from`, `localField`, `foreignField`, `as` spelling |
| **Transaction Errors** | `TransientTransactionError` | Write conflict or network blip during a transaction | Retry the transaction (driver's `withTransaction()` does this automatically) |
| **Performance Problems** | Slow query, high `totalDocsExamined` | Missing/wrong index, `COLLSCAN` on large collection | Run `explain()`, add the correct compound index using the ESR rule |
| **Cast/Type Errors (Mongoose)** | `CastError: Cast to ObjectId failed` | Passing an invalid/malformed ID string to a query | Validate ID format (`mongoose.Types.ObjectId.isValid(id)`) before querying |
| **Version Conflict** | `WriteConflict` | Two concurrent transactions modifying the same document | Retry the operation; keep transactions short to minimize contention |

> ⚠️ **Interview Tip:** When asked "How do you debug a slow MongoDB query?", always walk through: `explain()` → check `COLLSCAN`/`totalDocsExamined` → design/add index (ESR rule) → re-verify.

---

## Section 27: Best Practices

### Schema Design
- Design around your **query patterns**, not around normalization purity — MongoDB rewards "design for how you read."
- Embed bounded, frequently-co-accessed data; reference unbounded or independently-changing data.
- Use the **extended reference** pattern for order/transaction line items (snapshot key display fields).

### Indexes
- Follow the **ESR Rule** (Equality → Sort → Range) for compound indexes.
- Regularly audit unused indexes (`$indexStats`) — every unused index is pure write overhead.
- Prefer a few well-designed compound indexes over many single-field indexes.

### Aggregation
- Put `$match`/`$sort` as early as possible; use indexes where you can.
- Use `$project`/`$unset` early to shrink documents before expensive stages (`$lookup`, `$group`).
- Use `$facet` to combine paginated results + total count in a single round trip.

### Transactions
- Keep transactions **short** — minimize the number of operations and network calls inside them.
- Prefer document-level atomicity (well-designed embedding) over reaching for transactions by default.

### Security
- Never expose the DB directly to the internet — use application-layer auth + firewall/VPC rules.
- Enable **authentication** and **role-based access control (RBAC)** in production.
- Use environment variables for connection strings; never hardcode credentials.

### Validation
- Use `$jsonSchema` validators at the DB level for critical collections (defense in depth beyond app-layer Mongoose validation).

### Naming Conventions
- Collections: plural, lowercase, snake_case or camelCase consistently (e.g., `orders`, `orderItems`).
- Fields: consistent casing (camelCase is standard in JS ecosystems).

### Performance
- Use connection pooling (a single shared client) — never open a connection per request.
- Use `bulkWrite()` for batch operations instead of looping individual writes.
- Monitor with `explain()`, Atlas Performance Advisor, or `mongostat`/`mongotop`.

### Production Tips
- Always run a **replica set** in production (never a standalone `mongod`) for availability.
- Set appropriate **write concern** (`w:"majority"`) for critical data.
- Regularly back up data (Atlas continuous backups or `mongodump`/`mongorestore`).


---

## Section 28: One-Page Cheat Sheet

### CRUD
```javascript
db.col.insertOne({...}) | db.col.insertMany([{...}])
db.col.find({filter}, {projection}) | db.col.findOne({filter})
db.col.updateOne({filter}, {$set:{...}}) | db.col.updateMany({filter}, {$inc:{...}})
db.col.replaceOne({filter}, {newDoc})
db.col.deleteOne({filter}) | db.col.deleteMany({filter}) | db.col.drop()
```

### Operators
```
Comparison: $eq $ne $gt $gte $lt $lte $in $nin
Logical:    $and $or $not $nor
Element:    $exists $type
Array:      $all $size $elemMatch $push $addToSet $pull $pop
Update:     $set $unset $inc $mul $rename $min $max
Evaluation: $regex $text $expr
```

### Aggregation Stages
```
$match  $group  $project  $sort  $limit  $skip  $count
$lookup $unwind $facet $bucket $bucketAuto $sample
$replaceRoot $addFields $unset $merge $out $setWindowFields
```

### Indexing
```javascript
db.col.createIndex({field:1})                        // ascending single
db.col.createIndex({f1:1, f2:-1})                     // compound (ESR order!)
db.col.createIndex({field:1}, {unique:true})
db.col.createIndex({field:1}, {sparse:true})
db.col.createIndex({field:1}, {expireAfterSeconds:3600}) // TTL
db.col.createIndex({field:"text"})
db.col.createIndex({field:"hashed"})
db.col.find(...).explain("executionStats")
```
**ESR Rule:** Equality fields → Sort fields → Range fields (left to right in the index).

### Transactions (Node.js)
```javascript
const session = client.startSession();
await session.withTransaction(async () => {
  await colA.updateOne({...}, {...}, { session });
  await colB.updateOne({...}, {...}, { session });
});
session.endSession();
```

### Replication
```
Primary (R/W) ── oplog ──▶ Secondary(s) (R only, if configured)
Read Pref: primary | primaryPreferred | secondary | secondaryPreferred | nearest
Write Concern: {w:1|"majority", j:true, wtimeout:ms}
```

### Sharding
```
mongos (router) → Config Servers (metadata) → Shards (each a replica set)
Shard Key: high cardinality + even distribution + matches query patterns
```

### Mongoose Quick Reference
```javascript
const schema = new mongoose.Schema({...}, {timestamps:true});
const Model = mongoose.model("Name", schema);
schema.pre("save", fn) | schema.post("save", fn)
Model.find().populate("ref")
schema.virtual("x").get(fn)
schema.methods.fn = fn   // instance
schema.statics.fn = fn   // model-level
```

### `$lookup` Template
```javascript
{ $lookup: { from:"col2", localField:"f", foreignField:"_id", as:"out" } }
{ $unwind: "$out" }   // flatten if one-to-one
```

### Performance Quick Checklist
```
1. explain("executionStats") → check for COLLSCAN
2. Add compound index (ESR rule)
3. Use projection to limit fields (enables covered queries)
4. $match early in aggregation pipelines
5. bulkWrite() for batch ops; connection pooling always
```

---

## Section 29: Last-Minute Revision Index

> **The night before your interview:** re-read this section only, then skim the tables in Sections 23 and 28.

### Top Concepts You MUST Be Able to Explain Fluently
1. MongoDB vs SQL (Section 1.4)
2. Document, Collection, Database hierarchy (Section 1.8)
3. WiredTiger + Read/Write Path (Section 2.3–2.6)
4. CRUD method differences — `updateOne` vs `replaceOne`, `deleteMany` vs `drop` (Section 4)
5. `$elemMatch` trap (Section 5.5)
6. Projection inclusion/exclusion rule (Section 6)
7. Why `skip()` is inefficient for deep pagination (Section 7.1)
8. All index types + Compound Index prefix rule (Section 8)
9. `explain()` output fields + COLLSCAN vs IXSCAN (Section 9)
10. **ESR Rule** — Equality, Sort, Range (Section 10)
11. Aggregation pipeline stages, especially `$match`, `$group`, `$lookup`, `$unwind`, `$facet` (Section 11)
12. `$lookup` mechanics + performance (Section 12)
13. Embedding vs Referencing decision table (Section 13)
14. Schema design for at least 3 real-world systems (Section 14 & 24)
15. Replica Set roles + election + write concern (Section 15)
16. Sharding + shard key hot-spot problem (Section 16)
17. Transactions vs document-level atomicity (Sections 17–18)
18. Mongoose: Schema vs Model, `populate()` vs `$lookup`, middleware (Section 20)
19. Node.js connection pooling + repository pattern (Section 21)
20. Highest/Nth-highest salary and duplicate-finding aggregation queries (Section 22, Q1–Q4)

### Rapid-Fire Drill Order (Morning of the Interview)
1. Section 28 — Cheat Sheet (5 min skim)
2. Section 23 — 50-question rapid-fire table (10 min skim)
3. Section 25 — Tricky Questions (10 min skim)
4. Section 22, Q1–Q10 — re-derive from memory without looking (10 min active recall)
5. Pick 2 schemas from Section 24 and explain your reasoning out loud (5 min)

### Interview-Day Mindset Reminders
- If asked to write a query live: **narrate your thought process** — interviewers weigh reasoning as much as syntax.
- If you don't know something: say what you *do* know that's adjacent, and reason toward an answer rather than going silent.
- Always mention **`explain()`** when asked about performance/optimization — it signals real hands-on experience, not just theory.
- For schema design questions, always state your **embed vs reference** decision explicitly, with a one-line justification.

---

*End of handbook. Good luck with your TCS Prime interview! 🚀*
