# Chapter 6 Djano Forms

## Django Forms
```python
request.path #The full path, not including the domain but including the leading slash.
request.get_host() #The host
request.get_full_path() #The path, plus a query string
request.is_secure() # True if the request was mad via HTTPS. Otherwise, False.

# GOOD
def current_url_view_good(request):
    return HttpResponse("Welcome to the page at %s"
% request.path)

#Common available keys in the Request.META dictionary are:
HTTP_REFERER # The referring URL, if any. (Note the misspelling of REFERER.)
HTTP_USER_AGENT # The user’s browser’s user-agent string, if any. This looks something like: "Mozilla/5.0 (X11; U; Linux`` i686; fr-FR; rv:1.8.1.17) Gecko/20080829 Firefox/2.0.0.17".
REMOTE_ADDR # The IP address of the client, e.g., "12.345.67.89". (If the request has passed through any proxies, then this might be a comma-separated list of IP addresses, e.g., "12.345.67.89,23.456.78.90".)

## To handle the case of undefined keys:
##
# GOOD (VERSION 1)
def ua_display_good1(request):
    try:
        ua = request.META['HTTP_USER_AGENT']
    except KeyError:
        ua = 'unknown'
    return HttpResponse("Your browser is %s" % ua)

# GOOD (VERSION 2)
def ua_display_good2(request):
    ua = request.META.get('HTTP_USER_AGENT', 'unknown')
    return HttpResponse("Your browser is %s" % ua)

## display all of the request.META data
def display_meta(request):
    values = request.META   
    html = []
    for k in sorted(values):
        html.append('<tr><td>%s</td><td>%s</td></tr>' % (k, values[k]))
    return HttpResponse('<table>%s</table>' % '\n'.join(html))
    

request.GET #data can come from a <form> or the query string in the page’s URL.
request.POST #data generally is submitted from an HTML <form>

```
```html
<head>
    <title>Search</title>
</head>
<body>
    {% if error %}
        <p style="color: red;">Please submit a search term.</p>
    {% endif %}
    <form action="" method="get">
        <input type="text" name="q">
        <input type="submit" value="Search">
    </form>
</body>
</html>
```
<form action="" method="get"> The action="" means “Submit the form to the same URL as the current page.”

```python
def search(request):
    error = False
    if 'q' in request.GET:
        q = request.GET['q']
        if not q:
            error = True
        else:
            books = Book.objects.filter(title__icontains=q)
            return render(request, 'books/search_results.html', {'books': books, 'query': q})
    return render(request, 'books/search_form.html', {'error': error})
```

## Simple Validation

```python
def search(request):
    errors = []
    if 'q' in request.GET:
        q = request.GET['q']
        if not q:
            errors.append('Enter a search term.')
        elif len(q) > 20:
            errors.append('Please enter at most 20 characters.')
        else:
            books = Book.objects.filter(title__icontains=q)
            return render(request, 'search_results.html', {'books': books, 'query': q})
    return render(request, 'search_form.html', {'errors': errors})
```
```html
<html>
<head>
    <title>Search</title>
</head>
<body>
    {% if errors %}
        <ul>
            {% for error in errors %}
            <li>{{ error }}</li>
            {% endfor %}
        </ul>
    {% endif %}
    <form action="/search/" method="get">
        <input type="text" name="q">
        <input type="submit" value="Search">
    </form>
</body>
</html>
```

### Making a Contact Form
```python
from django import forms

class ContactForm(forms.Form):
    subject = forms.CharField()
    email = forms.EmailField(required=False)
    message = forms.CharField()

f = ContactFrom({'subject': 'Hello', 'email': 'nige@example.com', 'message': 'Nice site!'})
{{f.as_p}}
{{f.as_ul}}
f.is_bound() #Once you’ve associated data with a Form instance, you’ve created a “bound” form:
f.is_valid() #whether its data is valid
f.cleaned_data
f.errors/f['email'].errors
```
