# Flask Overview

## What is Flask?
Flask is a web application framework written in Python. It is developed by Armin Ronacher.  
Flask is based on the Werkzeug WSGI toolkit and Jinja2 template engine.

**WSGI**  
Web Server Gateway Interface (WSGI) has been adopted as a standard for Python web application development. WSGI is a specification for a universal interface between the web server and the web applications.

**Werkzeug**  
It is a WSGI toolkit, which implements requests, response objects, and other utility functions. This enables building a web framework on top of it. The Flask framework uses Werkzeug as one of its bases.

**Jinja2**  
Jinja2 is a popular templating engine for Python. A web templating system combines a template with a certain data source to render dynamic web pages.

Flask is often referred to as a micro framework. It aims to keep the core of an application simple yet extensible. Flask does not have built-in abstraction layer for database handling, nor does it have form a validation support. Instead, Flask supports the extensions to add such functionality to the application.  

## Flask Environment
Flask and its dependencies work well with Python 3.  

**Install virtualenv for development environment**  
`virtualenv` is a virtual Python environment builder. It helps a user to create multiple Python environments side-by-side. Thereby, it can avoid compatibility issues between the different versions of the libraries.

The following command installs virtualenv  
`pip install virtualenv`  

Once installed, new virtual environment is created in a folder.  
`mkdir newproj`  
`cd newproj`  
`virtualenv venv`  

On Windows, activate the venv  
`venv\scripts\activate`

**Install Flask in this environment.**  
`pip install Flask`  
The above command can be run directly, without virtual environment for system-wide installation.

## Flask Application
Let us now create a simple flask application.

Create a file named `Hello.py` and add the follwoing code to it.
```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
   return 'Hello World'

if __name__ == '__main__':
   app.run()
```  
Importing flask module in the project is mandatory. An object of Flask class is our WSGI application.  
Flask constructor takes the name of current module `(__name__)` as argument.  
The route() function of the Flask class is a decorator, which tells the application which URL should call the associated function.  
`app.route(rule, options)`  
- The `rule` parameter represents URL binding with the function.  
- The `options` is a list of parameters to be forwarded to the underlying Rule object.  

In the example, `/ URL` is bound with `hello_world()` function. When the home page of web server is opened in browser, the output of this function will be rendered.  
Finally the `run()` method of Flask class runs the application on the local development server.
`app.run(host, port, debug, options)`

**host** : Hostname to listen on. Defaults to 127.0.0.1 (localhost). Set to 0.0.0.0 to have server available externally  
**port** : Defaults to 5000  
**debug** : Defaults to false. If set to true, provides a debug information  
**options** : To be forwarded to underlying Werkzeug server.  

## Flask Routing  
`route` typically refers to the mechanism used in web frameworks to map specific URLs to corresponding functions or actions within an application. This allows the application to respond to different user requests based on the URL they access.  
The `route()` decorator in Flask is used to bind URL to a function
```python
@app.route(/hello)
def hello_world():
   return hello world
```  
URL `/hello` rule is bound to the `hello_world()` function. 
When a user visits `http://localhost:5000/hello` URL, the output of the hello_world() function will be rendered in the browser.  
The `add_url_rule()` function of an application object is also available to bind a URL with a function.
The `add_url_rule()` method in Flask is used to register a URL rule and associate it with a view function. This provides an alternative to using the @app.route() decorator, particularly useful for dynamic URL registration or when organizing routes in a centralized manner.  
```python
def hello_world():
   return hello world

app.add_url_rule('/hello', 'hello', hello_world)
```

**Key Parameters:**
- **rule**: This defines the URL path. It can include variable parts like `<username>` which will be passed as arguments to the view_func.  
- **endpoint**: This is a unique name for the URL rule, used for URL generation with `url_for()`. If not provided, Flask defaults to the name of the `view_func`.  
- **view_func**: This is the function that will be executed when a request matches the specified rule.
- **methods**: (Optional) A list of HTTP methods that the rule should respond to (e.g., ['GET', 'POST']). By default, it listens for GET requests.
- **defaults**: (Optional) A dictionary of default values for URL variables.
- **subdomain**: (Optional) Specifies a subdomain for the URL rule.
- **options`**: (Optional) Additional options passed to the underlying Rule object.  

**Advantages of `add_url_rule()`**:  
- **Dynamic URL Registration**: Allows you to register URL rules programmatically, which is useful when URLs are generated based on data or configuration.
- **Centralized URL Mapping**: You can define all your URL rules in a single location, potentially in a separate file, for better organization, especially in larger applications.
- **Lazy Loading Views**: Can be beneficial for performance in certain deployment environments where quick application startup is critical, as view functions don't need to be imported upfront.  

## Flask Variable Rules
It is possible to build a URL dynamically, by adding variable parts to the rule parameter. This variable part is marked as `<variable-name>`. It is passed as a keyword argument to the function with which the rule is associated.

```python
from flask import Flask
app = Flask(__name__)

@app.route('/hello/<name>')
def hello_name(name):
   return 'Hello %s!' % name

if __name__ == '__main__':
   app.run(debug = True)
```

In addition to the default string variable part, rules can be constructed using the following converters  
**int** : accepts integer  
**float** : For floating point value  
**path** : accepts slashes used as directory separator character  
```python
from flask import Flask
app = Flask(__name__)

@app.route('/blog/<int:postID>')
def show_blog(postID):
   return 'Blog Number %d' % postID

@app.route('/rev/<float:revNo>')
def revision(revNo):
   return 'Revision Number %f' % revNo

if __name__ == '__main__':
   app.run()
```  

```python
from flask import Flask
app = Flask(__name__)

@app.route('/flask')
def hello_flask():
   return 'Hello Flask'

@app.route('/python/')
def hello_python():
   return 'Hello Python'

if __name__ == '__main__':
   app.run()
   ```
Both the rules appear similar but in the second rule, trailing slash (/) is used. Using /python or /python/ returns the same output. However, in case of the first rule, /flask/ URL results in 404 Not Found page.

## Flask URL Building  
The `url_for()` function is very useful for dynamically building a URL for a specific function. The function accepts the name of a function as first argument, and one or more keyword arguments, each corresponding to the variable part of URL.

```python
from flask import Flask, redirect, url_for
app = Flask(__name__)

@app.route('/admin')
def hello_admin():
   return 'Hello Admin'

@app.route('/guest/<guest>')
def hello_guest(guest):
   return 'Hello %s as Guest' % guest

@app.route('/user/<name>')
def hello_user(name):
   if name =='admin':
      return redirect(url_for('hello_admin'))
   else:
      return redirect(url_for('hello_guest',guest = name))

if __name__ == '__main__':
   app.run(debug = True)
   ```

## Flask HTTP methods

- **GET** : Sends data in unencrypted form to the server. Most common method.
- **HEAD** : Same as GET, but without response body
- **POST** : Used to send HTML form data to server. Data received by POST method is not cached by server.
- **PUT** : Replaces all current representations of the target resource with the uploaded content.
- **DELETE** : Removes all current representations of the target resource given by a URL

```html
<html>
   <body>
      <form action = "http://localhost:5000/login" method = "post">
         <p>Enter Name:</p>
         <p><input type = "text" name = "nm" /></p>
         <p><input type = "submit" value = "submit" /></p>
      </form>
   </body>
</html>
```

```python
from flask import Flask, redirect, url_for, request
app = Flask(__name__)

@app.route('/success/<name>')
def success(name):
   return 'welcome %s' % name

@app.route('/login',methods = ['POST', 'GET'])
def login():
   if request.method == 'POST':
      user = request.form['nm']
      return redirect(url_for('success',name = user))
   else:
      user = request.args.get('nm')
      return redirect(url_for('success',name = user))

if __name__ == '__main__':
   app.run(debug = True)
```
## Flask Templates
It is possible to return the output of a function bound to a certain URL in the form of HTML. For instance, in the following script, hello() function will render Hello World with `<h1>` tag attached to it.
```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def index():
   return '<html><body><h1>Hello World</h1></body></html>'

if __name__ == '__main__':
   app.run(debug = True)
```  
We can use `Jinja2` template engine, on which Flask is based. Instead of returning hardcode HTML from the function, a HTML file can be rendered by the render_template() function.
```python
from flask import Flask, render_template
app = Flask(__name__)
#app = Flask(__name__, template_folder='views')
@app.route('/')
def index():
   return render_template("hello.html")

if __name__ == '__main__':
   app.run(debug = True)
```
Flask will try to find the HTML file in the templates folder, in the same folder in which this script is present.

```html
<!doctype html>
<html>
   <body>
      <h1>Hello {{ name }}!</h1>
   </body>
</html>
```

```python
from flask import Flask, render_template
app = Flask(__name__)

@app.route('/hello/<user>')
def hello_name(user):
   return render_template('hello.html', name = user)

if __name__ == '__main__':
   app.run(debug = True)
```  

The **jinja2** template engine uses the following delimiters for escaping from HTML.

- **{% ... %}** for Statements
- **{{ ... }}** for Expressions to print to the template output
- **{# ... #}** for Comments not included in the template output
- **# ... ##** for Line Statements

```python
from flask import Flask, render_template
app = Flask(__name__)

@app.route('/hello/<int:score>')
def hello_name(score):
   return render_template('hello.html', marks = score)

if __name__ == '__main__':
   app.run(debug = True)
   ```
```html
<!doctype html>
<html>
   <body>
      {% if marks>50 %}
         <h1> Your result is pass!</h1>
      {% else %}
         <h1>Your result is fail</h1>
      {% endif %}
   </body>
</html>
```

```python
from flask import Flask, render_template
app = Flask(__name__)

@app.route('/result')
def result():
   dict = {'phy':50,'che':60,'maths':70}
   return render_template('hello.html', result = dict)

if __name__ == '__main__':
   app.run(debug = True)
```

```html
<!doctype html>
<html>
   <body>
      <table border = 1>
         {% for key, value in result.items() %}
            <tr>
               <th> {{ key }} </th>
               <td> {{ value }} </td>
            </tr>
         {% endfor %}
      </table>
   </body>
</html>
```

## Flask Request Object
The Flask request object is a central component in Flask web applications, providing access to all information associated with an incoming HTTP request. It is automatically created by Flask for each request and made available within the request context.  
**Key attributes and properties of the request object:**
- **request.method:** The HTTP method of the request (e.g., 'GET', 'POST', 'PUT', 'DELETE').
- **request.args:** A dictionary-like object containing the parsed contents of the URL query string (parameters after the ? in the URL).
- **request.form:** A dictionary-like object containing key-value pairs of form parameters submitted via 'POST' or 'PUT' requests.
- **request.json: or request.get_json():** Used to access JSON data sent in the request body, typically for API requests.
- **request.cookies:** A dictionary-like object holding the names and values of cookies sent with the request.
- **request.files:** A dictionary-like object containing data about uploaded files.
- **request.headers:** A dictionary-like object providing access to the HTTP headers of the request.
- **request.url:** The complete requested URL.
- **request.host:** The host and port number from the request.
- **request.remote_addr:** The IP address of the client making the request.  
**Accessing the request object:** 
To utilize the request object within a Flask view function, it needs to be imported from the flask package:

```python
from flask import Flask, request

app = Flask(__name__)

@app.route('/data', methods=['GET', 'POST'])
def handle_data():
    if request.method == 'POST':
        username = request.form.get('username')
        password = request.form.get('password')
        # Process form data
        return f"Received POST data: Username={username}, Password={password}"
    else: # GET request
        query_param = request.args.get('param')
        # Process query parameters
        return f"Received GET data: Query Parameter={query_param}"

if __name__ == '__main__':
    app.run(debug=True)
```

## Flask Redirect & Errors
Flask class has a `redirect()` function. When called, it returns a response object and redirects the user to another target location with specified status code.  
`Flask.redirect(location, statuscode, response)`
```python
from flask import Flask, redirect, url_for, render_template, request
# Initialize the Flask application
app = Flask(__name__)

@app.route('/')
def index():
   return render_template('log_in.html')

@app.route('/login',methods = ['POST', 'GET']) 
def login(): 
   if request.method == 'POST' and request.form['username'] == 'admin' :
      return redirect(url_for('success'))
   else:
      return redirect(url_for('index'))

@app.route('/success')
def success():
   return 'logged in successfully'
	
if __name__ == '__main__':
   app.run(debug = True)
```

Flask class has `abort()` function with an error code.  
`Flask.abort(code)`

- _400_ : for Bad Request
- _401_ : for Unauthenticated
- _403_ : for Forbidden
- _404_ : for Not Found
- _406_ : for Not Acceptable
- _415_ : for Unsupported Media Type
- _429_ : Too Many Requests

```python
from flask import Flask, redirect, url_for, render_template, request, abort
app = Flask(__name__)

@app.route('/')
def index():
   return render_template('log_in.html')

@app.route('/login',methods = ['POST', 'GET'])
def login():
   if request.method == 'POST':
      if request.form['username'] == 'admin' :
         return redirect(url_for('success'))
      else:
         abort(401)
   else:
      return redirect(url_for('index'))

@app.route('/success')
def success():
   return 'logged in successfully'

if __name__ == '__main__':
   app.run(debug = True)
```

