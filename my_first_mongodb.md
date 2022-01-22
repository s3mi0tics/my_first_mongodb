<!-- Using MongoDB -->

<!-- Create a database called 'my_first_db'. -->
use my_first_db

<!-- Create students collection. -->

<!-- Each document you insert into this collection should have the following format: ({name: STRING, home_state: STRING, lucky_number: NUMBER, birthday: {month: NUMBER, day: NUMBER, year: NUMBER}})

Create 5 students with the appropriate info. -->
db.students.insert(
                {name: "Jon Kelly", 
                home_state: "Ohio", 
                lucky_number: 25, 
                birthday:{month: 12, day:12, year: 2012}})
db.students.insert(
                {name: "Joe Jhonson", 
                home_state: "Georgia", 
                lucky_number: 1, 
                birthday:{month: 2, day:5, year: 2022}})

db.students.insertMany([
                {name: "Jon Kelly", 
                home_state: "Ohio", 
                lucky_number: 25, 
                birthday:{month: 12, day:12, year: 2012}},
                {name: "Chris Kelly", 
                home_state: "Ohio", 
                lucky_number: 23, 
                birthday:{month: 12, day:12, year: 2012}},
                {name: "Tyler Smith", 
                home_state: "Maine", 
                lucky_number: 12, 
                birthday:{month: 1, day:10, year: 2010}},
                {name: "Chelsea Kauk", 
                home_state: "Hawaii", 
                lucky_number: 13, 
                birthday:{month: 3, day:9, year: 1985}}
                ])

db.students.insertMany([
                {name: "Joe Mongo", 
                home_state: "Washington", 
                lucky_number: 25, 
                birthday:{month: 12, day:12, year: 2012}},
                {name: "Josh James", 
                home_state: "California", 
                lucky_number: 23, 
                birthday:{month: 12, day:12, year: 2012}}
                ])

<!-- Get all students. -->
db.students.find()

<!-- Retrieve all students who are from California (San Jose Dojo) or Washington (Seattle Dojo). -->
db.students.find({$or: [
                        {home_state: 'California'},
                        {home_state: 'Washington'}
                        ]
                        })

<!-- Get all students whose lucky number is greater than 3 -->
db.students.find({lucky_number:{$lt:3}})

<!-- Get all students whose lucky number is less than or equal to 10 -->
db.students.find({lucky_number:{$lte:10}})

<!-- Get all students whose lucky number is between 1 and 9 (inclusive) -->
db.students.find({$and: [
                    {lucky_number:{$lte:9}},
                    {lucky_number:{$gte:1}}
                    ]
                    })


<!-- Add a field to each student collection called 'interests' that is an ARRAY. It should contain the following entries: 'coding', 'brunch', 'MongoDB'. Do this in ONE operation. -->
db.students.updateMany({},{$set:{interests: ['coding', 'brunch', 'mongoDB']}})

<!-- Add some unique interests for each particular student into each of their interest arrays. -->
db.students.update({name:"Jon Kelly"}, {$push:{interests:'guitar2'}})
db.students.update({name:"Tyler Smith"}, {$push:{interests:'flute2'}})
db.students.update({name:"Chris Kelly"}, {$push:{interests:'piano2'}})
db.students.update({name:"Chelsea Kauk"}, {$push:{interests:'accordian2'}})
db.students.update({name:"Joe Mongo"}, {$push:{interests:'databases2'}})
db.students.update({name:"Joe Jhonson"}, {$push:{interests:'drums2'}})
db.students.update({name:"Josh James"}, {$push:{interests:'sitar2'}})

<!-- Add the interest 'taxes' into someone's interest array. -->
db.students.update({name:"Joe Mongo"}, {$push:{interests:'taxes'}})


<!-- Remove the 'taxes' interest you just added. -->
db.students.update({interests: 'taxes'}, {$pull: {interests:"taxes"}})

<!-- Remove all students who are from California. -->
db.students.deleteMany({home_state: 'California'})

<!-- Remove a student by name. -->
db.students.deleteOne({name: 'Jon Kelly'})

<!-- Remove a student whose lucky number is greater than 5 (JUST ONE) -->
db.students.deleteOne({lucky_number : {$gt: 5}})


<!-- Add a field to each student collection called 'number_of_belts' and set it to 0. -->
db.students.updateMany({}, {$set:{number_of_belts: 0}})

<!-- Increment this field by 1 for all students in Washington (Seattle Dojo). -->
db.students.updateMany({home_state: "Washington"},{$inc:{number_of_belts: 1 }})

<!-- Rename the 'number_of_belts' field to 'belts_earned' -->
db.students.updateMany({}, {$rename: {'number_of_belts':"belts_earned"}})

<!-- Remove the 'lucky_number' field. -->
db.students.updateMany({}, {$unset: {lucky_number:""}})

<!-- Add a 'updated_on' field, and set the value as the current date. -->
db.students.updateMany({},{$currentDate: {updated_on:{$type:'date'}}})

