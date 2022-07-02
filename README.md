# Trivia App

Udacity is invested in creating bonding experiences for its employees and students. A bunch of team members got the idea to hold trivia on a regular basis and created a webpage to manage the trivia app and play the game, but their API experience is limited and still needs to be built out.

I Helped them finish the trivia app so they can start holding trivia and seeing who's the most knowledgeable of the bunch. Following are the application requirements:

1. Display questions - both all questions and by category. Questions should show the question, category and difficulty rating by default and can show/hide the answer.
2. Delete questions.
3. Add questions and require that they include question and answer text.
4. Search for questions based on a text query string.
5. Play the quiz game, randomizing either all questions or within a specific category.

## Getting Started

### Pre-requisites and Local Development 

Developers using this project should already have [Python3](https://www.python.org/downloads/), pip, [Node](https://nodejs.org/en/download/) and [Postgres](https://www.postgresql.org/download/) installed on their local machines. 

### Backend

#### Set up and Populate the Database

- Make sure that Postgres is running then create a `trivia` database: `createdb trivia`
- From the `/backend` folder in terminal, Populate the database using the trivia.psql file provided by running: `psql trivia < trivia.psql`

#### Install Dependencies

From the `/backend` folder run `pip install requirements.txt`. All required packages are included in the requirements file. 

#### Start the Server

To run the application, run the below commands in the `/backend` directory, start the Flask serve

```
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

These commands put the application in development and directs our application to use the `__init__.py` file in our flaskr folder. Working in development mode shows an interactive debugger in the console and restarts the server whenever changes are made. If running locally on Windows, look for the commands in the [Flask documentation](http://flask.pocoo.org/docs/1.0/tutorial/factory/).

The application is run on `http://127.0.0.1:5000/` by default and is a proxy in the frontend configuration. 

### Frontend

From the `/frontend` folder, run the following commands to start the client: 
```
npm install // only once to install dependencies
npm start 
```

By default, the frontend will run on localhost:3000. 

#### Tests

In order to run tests navigate to the backend folder and run the following commands: 

```
dropdb bookshelf_test
createdb bookshelf_test
psql bookshelf_test < books.psql
python test_flaskr.py
```

The first time you run the tests, omit the dropdb command. 

All tests are kept in that file and should be maintained as updates are made to app functionality. 

## API Reference

### Getting Started
- Base URL: At present this app can only be run locally and is not hosted as a base URL. The backend app is hosted at the default, `http://127.0.0.1:5000/`, which is set as a proxy in the frontend configuration. 
- Authentication: This version of the application does not require authentication or API keys. 

### Error Handling
Errors are returned as JSON objects in the following format:
```
{
    "error": 405,
    "message": "Method not allowed",
    "success": false
}
```
The API will return four error types when requests fail:
- 400: Bad Request
- 404: Resource Not Found
- 405: Method not allowed
- 422: Not Processable 

### Endpoints

#### GET /categories
- General:
    - Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
    - Request Arguments: None
    - Returns: An object with a single key, categories, that contains an object of id: category_string key:value pairs and a success message.
- Sample: `curl http://127.0.0.1:5000/categories`

``` 
{
  "categories": {
    "1": "Science", 
    "2": "Art", 
    "3": "Geography", 
    "4": "History", 
    "5": "Entertainment", 
    "6": "Sports"
  }, 
  "success": true
}
```

#### GET /questions?page=${integer}

- General:
  - Fetches a paginated set of questions, a total number of questions, all categories and current category string.
  - Request Arguments: page - integer
  - Returns: An object with 10 paginated questions, total questions, object including all categories, and a success message.

- Sample: `curl "http://127.0.0.1:5000/questions?page=2"`

```
{
  "categories": {
    "1": "Science", 
    "2": "Art", 
    "3": "Geography", 
    "4": "History", 
    "5": "Entertainment", 
    "6": "Sports"
  }, 
  "questions": [
    {
      "answer": "The Liver", 
      "category": 1, 
      "difficulty": 4, 
      "id": 20, 
      "question": "What is the heaviest organ in the human body?"
    }, 
    {
      "answer": "Alexander Fleming", 
      "category": 1, 
      "difficulty": 3, 
      "id": 21, 
      "question": "Who discovered penicillin?"
    }, 
    {
      "answer": "Blood", 
      "category": 1, 
      "difficulty": 4, 
      "id": 22, 
      "question": "Hematology is a branch of medicine involving the study of what?"
    }, 
    {
      "answer": "Scarab", 
      "category": 4, 
      "difficulty": 4, 
      "id": 23, 
      "question": "Which dung beetle was worshipped by the ancient Egyptians?"
    }, 
    {
      "answer": "Banana", 
      "category": 1, 
      "difficulty": 1, 
      "id": 24, 
      "question": "I am a yellow fruit and can be a 'split'."
    }, 
    {
      "answer": "Strawberry", 
      "category": 1, 
      "difficulty": 1, 
      "id": 25, 
      "question": "I'm red and heartshaped and am often eaten with cream."
    }
  ], 
  "success": true, 
  "totalQuestions": 16
}
```

#### GET /categories/${id}/questions
- General: 
  - Fetches questions for a cateogry specified by id request argument
  - Request Arguments: id - integer
  - Returns: An object with questions for the specified category, total questions, and current category string

- Sample: `curl "http://127.0.0.1:5000/categories/1/questions"`

```
{
  "current_category": "Science", 
  "questions": [
    {
      "answer": "The Liver", 
      "category": 1, 
      "difficulty": 4, 
      "id": 20, 
      "question": "What is the heaviest organ in the human body?"
    }, 
    {
      "answer": "Alexander Fleming", 
      "category": 1, 
      "difficulty": 3, 
      "id": 21, 
      "question": "Who discovered penicillin?"
    }, 
    {
      "answer": "Blood", 
      "category": 1, 
      "difficulty": 4, 
      "id": 22, 
      "question": "Hematology is a branch of medicine involving the study of what?"
    }, 
    {
      "answer": "Banana", 
      "category": 1, 
      "difficulty": 1, 
      "id": 24, 
      "question": "I am a yellow fruit and can be a 'split'."
    }, 
    {
      "answer": "Strawberry", 
      "category": 1, 
      "difficulty": 1, 
      "id": 25, 
      "question": "I'm red and heartshaped and am often eaten with cream."
    }
  ], 
  "success": true, 
  "total_questions": 16
}
```

#### DELETE /questions/${id}
- General:
  - Deletes a specified question using the id of the question
  - Request Arguments: id - integer
  - Returns: The id of the question and the success message.

- Sample: `curl -X DELETE http://127.0.0.1:5000/questions/16`

```
{
  "deleted": 16, 
  "success": true
}
```

#### POST /quizzes
- General:
    - Sends a post request in order to get the next question 
    - Request Body: previous questions and quiz category
    - Returns: a single new question object and a success message
- Sample: `curl http://127.0.0.1:5000/quizzes -X POST -H "Content-Type: application/json" -d '{"quiz_category":{"type":"Science","id":"1"}, "previous_questions":[11]}'`
```
{
  "question": {
    "answer": "Blood", 
    "category": 1, 
    "difficulty": 4, 
    "id": 22, 
    "question": "Hematology is a branch of medicine involving the study of what?"
  }, 
  "success": true
}
```

#### POST /questions
- General:
  - Sends a post request in order to add a new question
  - Request Body: A string value of a question, answer, int value of difficulty and category id
  - Returns the id of the created question and a success message

- Sample: `curl http://127.0.0.1:5000/questions -X POST -H "Content-Type: application/json" -d '{"question": "Heres a new question string", "answer": "Heres a new answer string", "difficulty": 1, "category": 3}'`

```
{
  "created": 38, 
  "success": true
}
```

#### POST /search
- General:
  - Sends a post request in order to search for a specific question by search term
  - Request Body: The search term
  - Returns: any array of questions, a number of totalQuestions that met the search term and the current category string

  - Sample: `curl http://127.0.0.1:5000/search -X POST -H "Content-Type: application/json" -d '{"searchTerm": "Here"}'`

```
{
  "questions": [
    {
      "answer": "Heres a new answer string", 
      "category": 3, 
      "difficulty": 1, 
      "id": 37, 
      "question": "Heres a new question string"
    }, 
    {
      "answer": "Heres a new answer string", 
      "category": 3, 
      "difficulty": 1, 
      "id": 38, 
      "question": "Heres a new question string"
    }
  ], 
  "success": true, 
  "totalQuestions": 2
}
```

# Deployment N/A

# Authors
Yours truly, Patrick K. Rashidi

# Acknowledgements 
The awesome team at Udacity, the session leader and all of the full stack students! 
