#The Model-View-Controller Design Pattern
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

#
