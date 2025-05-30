---
layout: post
title: Flask RESTful API JSON
date: 2018-08-11 13:39:23.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- api
- docker
- flask
- json
- python
author:
  display_name: deparkes
permalink: "/2018/08/11/flask-restful-api-json/"
---
JSON is a common format for sending data to and from a RESTful API. In this post we'll see how we can allow a simple Flask API to receive a JSON input. This post extends my <a href="{{site.baseurl}}/2018/03/02/simple-docker-flask-sqlite-api/">previous post</a> which made a simple Flask RESTful API and uses the Flask 'get_json()' method to accept JSON input.

If you just want to get stuck in and have a go, you can <a href="https://github.com/deparkes/docker_flask_example/tree/json_api">check out this code</a> on GitHub and get started. (I'm using a docker-ised version of flask, but you can use the information in this for any Flask app.)
<h1>How To Accept JSON Input</h1>
The basic unit we will use is <a href="https://flask.pocoo.org/docs/0.12/api/#flask.Request.get_json">request.get_json()</a>. This is a method available within the Flask framework and allows the app to handle JSON input. (<a href="https://flask.pocoo.org/docs/0.12/api/#flask.request">'request' is an object created as part of the flask 'route' decorator</a>.)

We will use 'get_json()' to return a dictionary, like this:

```python
json_dictionary = requests.get_json()
```
<h2>GET Request With JSON</h2>
The following is an example of how get_json can be incorporated into to a 'GET' request.  'request.get_json()' returns a dictionary, which we can then handle as normal.

```python
@app.route("/api/v1/resources/books/json", methods=['GET'])
def api_filter_json():
    books = request.get_json()
    results = []
    for book in books['books']:
        to_filter = []
        id = book['id']
        published = book['published']
        author = book['author']
        query = build_select_books_query(author, id, published, to_filter)
        conn = sqlite.connect('../data/books.db')
        conn.row_factory = dict_factory
        cur = conn.cursor()
        results.append(cur.execute(query, to_filter).fetchall()[0])
    return jsonify(results)
```

<h2>Other Request Types</h2>
The basic 'request.get_json()' approach can also be applied to <a href="https://stackoverflow.com/questions/504947/when-should-i-use-get-or-post-method-whats-the-difference-between-them">other HTTP protocol request</a> types such as POST or PUT. The application itself handles what it does with the JSON input it has received. <a href="https://stackoverflow.com/questions/19637459/rest-api-using-post-instead-of-get">Read more about different RESTful request types</a>.
<h1><strong>Testing the API</strong></h1>
Once you have added get_json to your api you will want to test it. This is more involved than a simple url-based request as we need to somehow<a href="https://stackoverflow.com/questions/7172784/how-to-post-json-data-with-curl-from-terminal-commandline-to-test-spring-rest"> send json as part of the request</a>.

To do this we will use '<a href="https://en.wikipedia.org/wiki/CURL">curl</a>', but other <a href="https://alternativeto.net/software/curl/">approaches are possible</a>.

```
curl --header "Content-Type: application/json" -X GET -d "{"books":[{"id":null,"author":"Ann Leckie ","""published""":2014},{"""id""":null,"""author""":"""John Scalzi""","""published""":2013}]}"" https://127.0.0.1:5000/api/v1/resources/books/json
```

If you are using windows, you will need to escape the quotation marks in your JSON, and put the whole string in quotation marks. For example:

```
curl --header "Content-Type: application/json" -X GET -d ""{"""books""":[{"""id""":null,"""author""":"""Ann Leckie ""","""published""":2014},{"""id""":null,"""author""":"""John Scalzi""","""published""":2013}]}"" https://127.0.0.1:5000/api/v1/resources/books/json
```

