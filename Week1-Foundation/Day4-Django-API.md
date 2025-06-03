django views - a view function or "view", is a python function that takes a web req and returns a web response. this response can be the html contents of a web page, or a redirect, or a 404 error, or an XML doc, or an image...

function-based views - simple python functions that receive an HttpRequest object as their first argument and are expected to return an HttpResonse object (or a subclass like JsonResponse)

class-based views - an alternative way to write views using python classes. they offer more structure and reusability for complex scenarios but FBVs are great for getting started and for simpler endpoints.

URL routing (urls.py)
when a user requests a URL from your django application, django's URL dispatcher determines which view function should handle that request. this mapping is defined in urls.py files.

how it works:
- you have a root urls.py in your project dir (e.g., redacted_platform/urls.py)
- each app can have its own urls.py (e.g., redacted_api/urls.py)
- the root urls.py can include() the app-specific urls.py
- each url pattern maps a url path to a view function

JsonResponse - a subclass of HttpResponse that automatically serializes a python dictionary into a JSON response and sets the Content-Type header to application/json. 

mini-project
1. create views in redacted_api/views.py
2. create redacted_api/urls.py
3. include app urls in project urls.py
4. test your api endpoint

