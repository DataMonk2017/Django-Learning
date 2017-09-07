# Chapter 1 Gettings Started
## The Model-View-Controller Design Pattern
The MVC design pattern is:
> - The model(M) is a model or representation of your data. It’s not the actual data, but an interface to the data. The model allows you to pull data from your database without knowing the intricacies of the underlying database. The model usually also provides an abstraction layer with your database, so that you can use the same model with multiple databases.
> - The view(V) is what you see. It’s the presentation layer for your model. On your computer, the view is what you see in the browser for a Web app, or the UI for a desktop app. The view also provides an interface to collect user input.
> - The controller(C) controls the flow of information between the model and the view. It uses programmed logic to decide what information is pulled from the database via the model and what information is passed to the view. It also gets information from the user via the view and implements business logic: either by changing the view, or modifying data through the model, or both.

MVC 是目前互联网常见网站建立设计模式。 Model 模型：建立数据库的联系， View 视图： 决定你的网页效果。 Controller 控制器: 掌控了视图和模型的之间信息流。
Django 已经将controller 集成包装了，人们只需要关注 models，templates and views 也就是django 所谓的 MTV框架。

> - M stands for “Model,” the data access layer. This layer contains anything and everything about the data: how to access it, how to validate it, which behaviors it has, and the relationships between the data. We will be looking closely at Django’s models in Chapter 4.
> - T stands for “Template,” the presentation layer. This layer contains presentation-related decisions: how something should be displayed on a Web page or other type of document. We will explore Django’s templates in Chapter 3.
> - V stands for “View,” the business logic layer. This layer contains the logic that accesses the model and defers to the appropriate template(s). You can think of it as the bridge between models and templates. We will be checking out Django’s views in the next chapter.

Django MVT 和 MVC 的对应
<br>

| MVT | MVC |
|-----:|:-----|
|Models|Models|
|View|Controller|
|Template|View|

# Chapter 2: Django Views and URLconfs
## Views and URLconfs

- The contents of the page are produced by a view function, and the URL is specified in a URLconf. 

- A URLconf is like a table of contents for your Django-powered web site. Basically, it’s a mapping between URLs and the view functions that should be called for those URLs. It’s how you tell Django, “For this URL, call this code, and for that URL, call that code.” For example, when somebody visits the URL /foo/, call the view function foo_view(), which lives in the Python module views.py.

### 需要import的模组
- from the django.conf.urls module import include, url: 
1. include which allows you to include a full Python import path to another URLconf module
2. , and url which uses a regular expression to pattern match the URL in your browser to a module in your Django project.
- from the django.contrib module import admin. This function is called by the include function to load the URLs for the Django admin site.

### urlparttern
- urlpatterns – a simple list of url() instances. The main thing to note here is the variable urlpatterns, which Django expects to find in your URLconf module. This variable defines the mapping between URLs and the code that handles those URLs. To add a URL and view to the URLconf, just add a mapping between a URL pattern and the view function.
- Django removes the slash from the front of every incoming URL before it checks the URLpatterns. This means that our URLpattern doesn’t include the leading slash in /hello/. At first, this may seem unintuitive, but this requirement simplifies things – such as the inclusion of URLconfs within other URLconfs.

#### parttern里面 ^ 和 $ 以及 Regular Expressions
- The pattern includes a caret (^) and a dollar sign ($). These are regular expression characters that have a special meaning: the caret means “require that the pattern matches the start of the string,” and the dollar sign means “require that the pattern matches the end of the string.”


### 为什么就算 网页打成/hello少了一个slash， django 还能成功render 回来而不报错？
> You may be wondering what happens if someone requests the URL /hello (that is, without a trailing slash). Because our URLpattern requires a trailing slash, that URL would not match. However, by default, any request to a URL that doesn’t match a URLpattern and doesn’t end with a slash will be redirected to the same URL with a trailing slash (This is regulated by the APPEND_SLASH Django setting, which is covered in Appendix D).

### django 如何处理一个request的？ django 网页与视图匹配流程
Before continuing to our second view function, let’s pause to learn a little more about how Django works. Specifically, when you view your “Hello world” message by visiting http://127.0.0.1:8000/hello/ in your web browser, what does Django do behind the scenes?

It all starts with the settings file. When you run python manage.py runserver, the script looks for a file called settings.py in the inner mysite directory. This file contains all sorts of configuration for this particular Django project, all in uppercase: TEMPLATES, DATABASES, etc.

The most important setting is called ROOT_URLCONF. ROOT_URLCONF tells Django which Python module should be used as the URLconf for this web site. Remember when django-admin startproject created the files settings.py and urls.py? The auto-generated settings.py contains a ROOT_URLCONF setting that points to the auto-generated urls.py. Open the settings.py file and see for yourself; it should look like this:

`ROOT_URLCONF = 'mysite.urls'` 

This corresponds to the file mysite/urls.py. When a request comes in for a particular URL – say, a request for /hello/ – Django loads the URLconf pointed to by the ROOT_URLCONF setting. Then it checks each of the URLpatterns in that URLconf, in order, comparing the requested URL with the patterns one at a time, until it finds one that matches.
When it finds one that matches, it calls the view function associated with that pattern, passing it an HttpRequest object as the first parameter. (We’ll cover the specifics of HttpRequest later.) As we saw in our first view example, a view function must return an HttpResponse.

Once it does this, Django does the rest, converting the Python object to a proper web response with the appropriate HTTP headers and body (i.e., the content of the web page). In summary:
1. A request comes in to /hello/.
2. Django determines the root URLconf by looking at the ROOT_URLCONF setting.
3. Django looks at all of the URLpatterns in the URLconf for the first one that matches /hello/.
4. If it finds a match, it calls the associated view function.
5. The view function returns an HttpResponse.
6. Django converts the HttpResponse to the proper HTTP response, which results in a web page.

## Django Views: Dynamic Content

### URLconfs and Loose Coupling

- Now’s a good time to highlight a key philosophy behind URLconfs and behind Django in general: the principle of loose coupling. Simply put, loose coupling is a software-development approach that values the importance of making pieces interchangeable. If two pieces of code are loosely coupled, then changes made to one of the pieces will have little or no effect on the other.

### Dynamic URLS - wildcard URLpatterns

### Django’s Pretty Error Pages
> Notes: If you’re experienced in another web development platform, you may be thinking, “Hey, let’s use a query string parameter!” – something like /time/plus?hours=3, in which the hours would be designated by the hours parameter in the URL’s query string (the part after the ‘?’).You can do that with Django (and I’ll tell you how in Chapter 7), but one of Django’s core philosophies is that URLs should be beautiful.
> The URL /time/plus/3/ is far cleaner, simpler, more readable, easier to recite to somebody aloud and just plain prettier than its query string counterpart. Pretty URLs are a characteristic of a quality web application. Django’s URLconf system encourages pretty URLs by making it easier to use pretty URLs than not to.

At any point in your view, temporarily insert an assert False to trigger the error page. Then, you can view the local variables and state of the program. Here’s an example, using the hours_ahead view:

```python
def hours_ahead(request, offset):
    try:
        offset = int(offset)
    except ValueError:
        raise Http404()
    dt = datetime.datetime.now() + datetime.timedelta(hours=offset)
    assert False
    html = "<html><body>In %s hour(s), it will be  %s.</body></html>" % (offset, dt)
    return HttpResponse(html) 
```
    
Finally, it’s obvious that much of this information is sensitive – it exposes the innards of your Python code and Django configuration – and it would be foolish to show this information on the public Internet. A malicious person could use it to attempt to reverse-engineer your web application and do nasty things.

For that reason, the Django error page is only displayed when your Django project is in debug mode. I’ll explain how to deactivate debug mode in Chapter 13. For now, just know that every Django project is in debug mode automatically when you start it. (Sound familiar? The “Page not found” errors, described earlier in this chapter, work the same way.)

## Django Templates

### Reasons why it’s not a good idea to hard-code HTML directly into your views:
- Any change to the design of the page requires a change to the Python code. The design of a site tends to change far more frequently than the underlying Python code, so it would be convenient if the design could change without needing to modify the Python code.

- This is only a very simple example. A common webpage template has hundreds of lines of HTML and scripts. Untangling and troubleshooting program code from this mess is a nightmare (cough-PHP-cough).

- Writing Python code and designing HTML are two different disciplines, and most professional web development environments split these responsibilities between separate people (or even separate departments). Designers and HTML/CSS coders shouldn’t be required to edit Python code to get their job done.

- It’s most efficient if programmers can work on Python code and designers can work on templates at the same time, rather than one person waiting for the other to finish editing a single file that contains both Python and HTML.

### tags
```
{{ variable }}
{% for x in y %} {% endfor %}
{% if conditions %} {% endif %}
{{ ship_date|date:"F j, Y"}} | is a filter
```

### use a dot to access dictionary keys, attributes, methods, or indices of an object. but negative list indices are not allowed.
- Dot lookups can be summarized like this: when the template system encounters a dot in a variable name, it tries the following lookups, in this order:

- Dictionary lookup (e.g., foo["bar"])
- Attribute lookup (e.g., foo.bar)
- Method call (e.g., foo.bar())
- List-index lookup (e.g., foo[2])

The system uses the first lookup type that works. It’s short-circuit logic. Dot lookups can be nested multiple levels deep. For instance, the following example uses {{ person.name.upper }}, which translates into a dictionary lookup (person['name']) and then a method call (upper())

#### Method Call Behavior
- If, during the method lookup, a method raises an exception, the exception will be propagated, unless the exception has an attribute silent_variable_failure whose value is True. If the exception does have a silent_variable_failure attribute, the variable will render as the value of the engine’s string_if_invalid configuration option (an empty string, by default).

- A method call will only work if the method has no required arguments. Otherwise, the system will move to the next lookup type (list-index lookup).

- By design, Django intentionally limits the amount of logic processing available in the template, so it’s not possible to pass arguments to method calls accessed from within templates. Data should be calculated in views and then passed to templates for display.

- Obviously, some methods have side effects, and it would be foolish at best, and possibly even a security hole, to allow the template system to access them.

- Say, for instance, you have a BankAccount object that has a delete() method. If a template includes something like {{ account.delete }}, where account is a BankAccount object, the object would be deleted when the template is rendered! To prevent this, set the function attribute alters_data on the method.

The template system won’t execute any method marked in this way. Continuing the above example, if a template includes {{ account.delete }} and the delete() method has the alters_data=True, then the delete() method will not be executed when the template is rendered, the engine will instead replace the variable with string_if_invalid.

NOTE: The dynamically-generated delete() and save() methods on Django model objects get alters_data=true set automatically.

### How Invalid Variables Are Handled
Generally, if a variable doesn’t exist, the template system inserts the value of the engine’s string_if_invalid configuration option, which is an empty string by default. 


