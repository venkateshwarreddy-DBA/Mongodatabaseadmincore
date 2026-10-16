# Mongodatabaseadmincore

Mongo Scripts : 

Complete List of collections : 
db.products.find()

Limit List for 3 : 
db.products.find({},{}).limit(3)

Fetch with condition : 
db.student.find({ "address.country": "Bharat" })

Update Script :  (Update all)

db.student.updateMany(
  { "address.country": "India" },
  { $set: { "address.country": "Bharat" } }
)

Update with Condition : 

Update with condition where the state = TG
db.student.updateMany(
  { "address.state": "Telangana" },
  { $set: { "address.country": "Bharat" } }
)

Sorting : db.student.find().sort({"address.state":1})

Sorting with Limitation : db.student.find().sort({"address.state":1}).limit(3)

* Rebuilds all indexes on a collection in the background.
  ```javascript
  db.LAB.reIndex({background:true})
  ```
* Retrieves a list of all indexes present on a single collection.
  ```javascript
  db.LAB.getIndexes()
  ```
* Loops through every collection in the database to display their indexes.
  ```javascript
  db.getCollectionNames().forEach(function(collection) { indexes = db[collection].getIndexes(); print("Indexes for " + collection + ":"); printjson(indexes); });
  ```

### Server Monitoring & Metrics

* Checks the total server uptime in seconds (divide by 60 for minutes, 3600 for hours, 84600 for days).
  ```javascript
  db.serverStatus().uptime
  ```
* Displays active, available, and total created connection counts on the server.
  ```javascript
  db.serverStatus().connections
  ```
* Checks global lock details, read/write operation counts, and blocked client queues.
  ```javascript
  db.serverStatus().globalLock
  ```
* Counts total database operations (inserts, queries, updates, deletes) since the last reboot.
  ```javascript
  db.serverStatus().opcounters
  ```
* Monitors resident and virtual RAM usage metrics utilized by MongoDB.
  ```javascript
  db.serverStatus().mem
  ```
* Identifies the hostname of the server to which you are currently connected.
  ```javascript
  db.serverStatus().host
  ```
* Retrieves the current MongoDB server software version.
  ```javascript
  db.serverStatus().version
  ```

### Server Shutdown & Recovery

* Switches to the administrative database and safely shuts down the server instance.
  ```javascript
  use admin
  db.shutdownServer()
  ```
* Forces a server shutdown from any active database connection using an admin command.
  ```javascript
  db.adminCommand({shutdown:1})
  ```
* Repairs data files and clears the lock file after an unexpected server crash.
  ```bash
  mongod –dbpath /data/db --repair
  ```















