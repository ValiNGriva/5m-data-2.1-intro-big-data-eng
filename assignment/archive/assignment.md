# Assignment

## Brief

Write the Python codes for the following questions.

## Instructions

Paste the answer as Python in the answer code section below each question.

### Question 1

Question: From the `movies` collection, return the documents with the `plot` that starts with `"war"` in acending order of released date, print only title, plot and released fields. Limit the result to 5.

Answer:

```python
import pymongo
my_query = {"plot": {
    "$regex": "^war",
    "$options": "i"
    }
} 

# Count the total number of matching documents
total_count_War = movies.count_documents(my_query)

print(f"Total matching movies having plot starts with War: {total_count_War}")

# Select title, plot and released fields
projection = {
    # "_id": 0,
    "title": 1,
    "plot": 1,
    "released":1
}

# Return with plot starts with War in ascending released date with specific field selection
for i, movie in enumerate(movies.find(my_query,projection).sort('released', pymongo.ASCENDING).limit(5), start =1):
    print(f"No: {i}") # counter variable i beginning at 1 
    print(f"Title: {movie.get('title')}")
    print(f"Plot: {movie.get('plot')}")
    print(f"Released: {movie.get('released')}")
    print("-" * 20)  # separator for readability
```

### Question 2

Question: Group by `rated` and count the number of movies in each.

Answer:

```python
# Group movies by column 'rated' and count them
stage_group_rated = {
      "$group": {
            # "_id": "$rated",
            "_id": {"$toUpper": "$rated"},      # Convert the 'rated' field to uppercase
            "movie_count": { "$sum": 1 },       # Count the number of movies in the group
      }
}

# Sort the final groups by number of movies
stage_sort_rated = {
      "$sort": {"_id": pymongo.ASCENDING}
}

# Assemble the complete sequential pipeline
pipeline = [
      stage_group_rated,
      stage_sort_rated,
]

# Execute aggregation
results = movies.aggregate(pipeline)

for group in results:
      print(group)
```

### Question 3

Question: Count the number of movies with 3 comments or more.

Answer:

```python

```

## Submission

- Submit the URL of the GitHub Repository that contains your work to NTU black board.
- Should you reference the work of your classmate(s) or online resources, give them credit by adding either the name of your classmate or URL.
