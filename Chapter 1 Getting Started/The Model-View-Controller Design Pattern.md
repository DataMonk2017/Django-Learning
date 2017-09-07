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
- from the django.conf.urls module import include, url: include which allows you to include a full Python import path to another URLconf module, and url which uses a regular expression to pattern match the URL in your browser to a module in your Django project.
- from the django.contrib module import admin. This function is called by the include function to load the URLs for the Django admin site.
- urlpatterns – a simple list of url() instances. The main thing to note here is the variable urlpatterns, which Django expects to find in your URLconf module. This variable defines the mapping between URLs and the code that handles those URLs. To add a URL and view to the URLconf, just add a mapping between a URL pattern and the view function.
- Django removes the slash from the front of every incoming URL before it checks the URLpatterns. This means that our URLpattern doesn’t include the leading slash in /hello/. At first, this may seem unintuitive, but this requirement simplifies things – such as the inclusion of URLconfs within other URLconfs.
- The pattern includes a caret (^) and a dollar sign ($). These are regular expression characters that have a special meaning: the caret means “require that the pattern matches the start of the string,” and the dollar sign means “require that the pattern matches the end of the string.”
- You may be wondering what happens if someone requests the URL /hello (that is, without a trailing slash). Because our URLpattern requires a trailing slash, that URL would not match. However, by default, any request to a URL that doesn’t match a URLpattern and doesn’t end with a slash will be redirected to the same URL with a trailing slash (This is regulated by the APPEND_SLASH Django setting, which is covered in Appendix D).

- ROOT_URLCONF tells Django which Python module should be used as the URLconf for this web site.

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
