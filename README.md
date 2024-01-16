## refined following code in chat.openai.com
# Change the data type from String to Integer for RatingValue
rating_update = [{'$set': {'RatingValue': {'$toInt': '$RatingValue'}}}]

# Update documents for RatingValue
establishments.aggregate([
    {
        '$match': {
            'RatingValue': {'$type': 'string'}
        }
    },
    {
        '$unwind': '$RatingValue'
    },
    *rating_update,
    {
        '$out': 'establishments'
    }
])

## corrected this code with chat.openai.com
# Find the establishments with a hygiene score of 20
query = {"scores.Hygiene": {"$eq": 20}}

# Use count_documents to display the number of documents in the result
count = establishments.count_documents(query) <<<<<<<<<< specifically this part
print("Number of places with a hygiene score of 20:", count)
print("----------------")

# Display the first document in the results using pprint
result = establishments.find(query).limit(1)
pprint(list(result))
