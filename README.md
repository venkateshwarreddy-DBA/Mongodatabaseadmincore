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














