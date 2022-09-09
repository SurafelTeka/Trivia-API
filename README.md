<div class="cell markdown" data-editable="true">

<h1>Trivia API Project</h1>

Trivia enables users to play a trivia game based on general questions
either with friends or by themselves.

**Features and Functionalities**

1.  Display questions - both all questions and by category. Questions
    should show the question, category and difficulty rating by default
    and can show/hide the answer.
2.  Delete questions.
3.  Add questions and require that they include question and answer
    text.
4.  Search for questions based on a text query string.
5.  Play the quiz game, randomizing either all questions or within a
    specific category.

</div>

<div class="cell markdown" data-editable="true">

## Getting Started

<h3>Pre-requisites and Local Development</h3>

Make sure python 3 is installed alonside node and flask in your local
environemnt

### Development Setup

#### Backend

First, [install
Flask](http://flask.pocoo.org/docs/1.0/installation/#install-flask) if
you haven't already.

    $ cd ~
    $ sudo pip3 install Flask

To start and run the local development server,

1.  Initialize and activate a virtualenv:

<!-- end list -->

    $ cd YOUR_PROJECT_DIRECTORY_PATH/
    $ virtualenv --no-site-packages env
    $ source env/bin/activate

1.  Install the dependencies:

<!-- end list -->

    $ pip install -r requirements.txt

1.  Run the development server:

<!-- end list -->

    $ export FLASK_APP=flaskr
    $ export FLASK_ENV=development # enables debug mode
    $ flask run

**Database Setup**

With Postgres running, restore a database using the trivia.psql file
provided. From the backend folder in terminal run:

``` bash
psql trivia < trivia.psql
```

1.  Navigate to Home page <http://localhost:5000>

#### Frontend

This project depends on Nodejs and Node Package Manager (NPM). Find and
download Node and npm (which is included) at:
[https://nodejs.com/en/download](https://nodejs.org/en/download/).

This project uses NPM to manage software dependencies. NPM Relies on the
package.json file located in the `frontend` directory of this
repository.Inside the frontend folder run the following commands to
initialize the client:

``` bash
npm install
```

    npm install // only once to install dependencies
    npm start

\#\#\#Tests From the backend folder run the following commands to carry
out tests:

    dropdb trivia_test
    createdb trivia_test
    psql bookshelf_test < trivia.psql
    python test_flaskr.py

If its the first time running tests, exclude the first command. Future
test files should be stored in the specified file.

## Authors

Udacity team, Surafel Teka and Kerry McCarthy.

## Acknowledgements

My colleage from AAIT helped me on majority of the concepts during
development of the project without whom this project would be pushed by
months or years from completion. I also like to thank my instructor for
clearing some doubts on parts of the project requirements.

</div>

<div class="cell markdown">

<h2>API Reference</h2>

**Getting Started** <ul> <li>Base Url: Currently this applicatios runs
on local server. By default it is hosted on the default,
<code><https://localhost:5000/></code> or
<code><https://127.0.0.1:5000/></code> configured s a proxy for frontend
configuration. </li> <li> Authentication: This app doesn't require API
keys as of its current version is concerned.</li>

</ul>

**Error Handling**

Errors have the following JSON format: <code> { "success": False,
"error": 400, "message": "bad request" } </code>

The API will return the following error types when request fails: <ul>
<li>400: Bad Request </li> <li>404: Resource Not Found </li> <li>422:
Unprocessable </li> </ul>

### Endpoints

**GET /categories** <ul> <li> General <ul> <li>Returns available
categories, object with a single key in key value pairs. </li>  
</ul> </li> <li> Sample: <code>curl
<https://127.0.0.1:5000/categories></code></li> </ul>

    {
      "categories: {
        '1' : "Science",
        '2' : "Art",
        '3' : "Geography",
        '4' : "History",
        '5' : "Entertainment",
        '6' : "Sports"
        },
      "success": true
    }

**GET /questions?page=<page_number>**

Fetches a paginated dictionary of questions of all available categories

  - *Request parameters (optional):* page:int
  - *Example response:*  

<!-- end list -->

``` {
 "categories": {
   "1": "Science", 
   "2": "Art", 
   "3": "Geography", 
   "4": "History", 
   "5": "Entertainment", 
   "6": "Sports"
 }, 
 "current_category": null, 
 "questions": [
   {
     "answer": "Maya Angelou", 
     "category": 4, 
     "difficulty": 2, 
     "id": 5, 
     "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
   },  
   {
     "answer": "Escher", 
     "category": 2, 
     "difficulty": 1, 
     "id": 16, 
     "question": "Which dutch football player in 1921 was celebrated as hall of fame?"
   }
 ], 
 "success": true, 
 "total_questions": 2
}
```

**POST /questions**

  - Searches for questions using a search term,
  - Returns a JSON object with paginated questions matching the search
    term
  - Sample: `curl http://127.0.0.1:5000/questions -X POST -H
    "Content-Type: application/json" -d '{"searchTerm": "author"}'`

<!-- end list -->

    {
      "questions": [
        {
          "answer": "Tom Cruise",
          "category": 5,
          "difficulty": 4,
          "id": 4,
          "question": "Which actor did played in the original Maverick movie as the protagonist?"
        }
      ],
      "success": true,
      "total_questions": 1
    }

**DELETE /questions/<int:id>**

  - Deletes a question by id using url parameters
  - Returns id of deleted questions if successful
  - Sample: `curl -X DELETE http://127.0.0.1:5000/questions/2`

<!-- end list -->

    {
      "deleted": 2,
      "success": true,
      "total_questions": 20
    }

**POST /quizzes**

  - Allows user to play the trivia game
  - Uses JSON request parameters of a chosen category and previous
    questions
  - Returns JSON object with random available questions which are not
    among previous used questions
  - Sample: `curl http://127.0.0.1:5000/quizzes -X POST -H
    "Content-Type: application/json" -d '{"previous_questions":
    [10, 11], "quiz_category": {"type": "Sports", "id": "6"}}'`

<!-- end list -->

    {
      "question": {
        "answer": "Bayern",
        "category": 6,
        "difficulty": 3,
        "id": 25,
        "question": "which is the champion team of the champions 2020?"
      },
      "success": true
    }

</div>
