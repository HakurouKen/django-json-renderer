django-json-renderer
====================

A Simple json renderer for django.

Install
-------
::

    pip install django-json-renderer

Api
---
.. role:: python(code)
    :language: python

:python:`JsonResponse` Native Django :python:`JsonResponse` (or it’s polyfill).

:python:`ModelJSONEncoder`  Inherit from :python:`DjangoJSONEncoder`, extends the parser
of :python:`QuerySet` (using :python:`list(queryset.values())`) and :python:`Models` (using
:python:`model_to_dict`).

:python:`render_json(encoder=ModelJSONEncoder,safe=True,**kwargs)`  Return the
decorator that convert json-serializable to JsonResponse (using
:python:`ModelJSONEncoder` as default). :python:`encoder` and :python:`safe` params has the same
meaning as `Django JsonResponse <https://docs.djangoproject.com/en/1.10/ref/request-response/#jsonresponse-objects>`_.

Example
-------
.. code-block:: python

    from django.db import models
    from django_json_encoder import render_json

    class Person(models.Model):
        first_name = models.CharField(max_length=30)
        last_name = models.CharField(max_length=30)

    @render_json()
    def get_first_person(request):
        return Person.objects.all().first()

    ## `safe` params
    @render_json(safe=False):
        return Person.objects.all()

License
-------

MIT
