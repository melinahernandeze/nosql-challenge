# nosql-challenge

## Eat Safe, Love

### Part 1: Database and Jupyter Notebook Set Up

#### Importing Data

To import the dataset from the establishments.json file, follow these steps:

1. Open your terminal.
2. Navigate to the directory containing the establishments.json file.
3. Use the following command to import the dataset into MongoDB:

   ```bash
   mongoimport --db uk_food --collection establishments --file establishments.json

   Setting Up Jupyter Notebook
Import dependencies:

python
Copy code
from pymongo import MongoClient
from pprint import pprint
Create an instance of MongoClient:

python
Copy code
mongo = MongoClient(port=27017)
Assign the uk_food database to a variable:

python
Copy code
db = mongo['uk_food']
List the collections in the uk_food database:

python
Copy code
db.list_collection_names()
Review a document in the establishments collection:

python
Copy code
pprint(db.establishments.find_one())
Assign the collection to a variable:

python
Copy code
establishments = db['establishments']
Part 2: Updating the Database
Adding a New Restaurant
To add a new restaurant "Penang Flavours" to the database, follow these steps:

Create a dictionary for the new restaurant data.

Insert the new restaurant into the collection:

python
Copy code
insert_result = establishments.insert_one(new_restaurant)
Updating BusinessTypeID
To update the new restaurant with the correct BusinessTypeID, follow these steps:

Find the BusinessTypeID for "Restaurant/Cafe/Canteen" and return only the BusinessTypeID and BusinessType fields.

Update the new restaurant with the correct BusinessTypeID.

python
Copy code
business_type_id = restaurant_type["BusinessTypeID"]
establishments.update_one({"BusinessName": "Penang Flavours"}, {"$set": {"BusinessTypeID": business_type_id}})
Removing Establishments in Dover
To remove any establishments within the Dover Local Authority from the database, follow these steps:

Check how many documents contain the Dover Local Authority.

Delete all documents where LocalAuthorityName is "Dover".

Check the number of documents to ensure they were deleted.

python
Copy code
dover_count = establishments.count_documents({"LocalAuthorityName": "Dover"})
delete_result = establishments.delete_many({"LocalAuthorityName": "Dover"})
remaining_dover_count = establishments.count_documents({"LocalAuthorityName": "Dover"})
Updating Data Types
To update the data types for latitude, longitude, and RatingValue fields, follow these steps:

Convert latitude and longitude fields from strings to decimal numbers.

Convert RatingValue to integer numbers.

Requirements
This README provides an overview of setting up the database
