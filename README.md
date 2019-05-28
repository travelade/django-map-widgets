[![Coverage Status](https://coveralls.io/repos/github/erdem/django-map-widgets/badge.svg?branch=master)](https://coveralls.io/github/erdem/django-map-widgets?branch=master)
[![Build Status](https://travis-ci.org/erdem/django-map-widgets.png)](https://travis-ci.org/erdem/django-map-widgets)
[![PyPI version](https://badge.fury.io/py/django-map-widgets.svg)](https://badge.fury.io/py/django-map-widgets)

### Django Map Widgets
Configurable, pluggable and more user friendly map widgets for Django PostGIS fields.

* **Documentation**: <a href="http://django-map-widgets.readthedocs.io/" target="_blank">http://django-map-widgets.readthedocs.io/</a>
* **Project Home Page**: <a href="https://github.com/erdem/django-map-widgets">https://github.com/erdem/django-map-widgets/</a>

### Achievements
The aim of the Django map widgets is to make all Geo Django widgets more user friendly and configurable. Map widgets are currently supporting only Google Map services, but we are planning to add other major map services.

### Installation

    pip install django-map-widgets


Add ‘map_widgets’ to your `INSTALLED_APPS` in settings.py

```python
INSTALLED_APPS = [
     ...
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    'mapwidgets',
]
```

Collects the static files into `STATIC_ROOT`.

```bash
python manage.py collectstatic
```

**Django Admin**

```python
from django.contrib.gis.db import models
from mapwidgets.widgets import GooglePointFieldWidget


class CityAdmin(admin.ModelAdmin):
    formfield_overrides = {
        models.PointField: {"widget": GooglePointFieldWidget}
    }
```

**Django Forms**

```python
from mapwidgets.widgets import GooglePointFieldWidget, GoogleStaticOverlayMapWidget


class CityForm(forms.ModelForm):

    class Meta:
        model = City
        fields = ("coordinates", "city_hall")
        widgets = {
            'coordinates': GooglePointFieldWidget,
            'city_hall': GoogleStaticOverlayMapWidget,
        }
```

...and your template should look something like this

```html
<form method="POST" action="">
    {% csrf_token %}
    {{form.media}}
    {{form.as_p}}
</form>
```

### Requirements

Django Map Widgets needs Jquery dependency to work in your regular views. In Django Admin case, you don't need to provide the jQuery just because it's already available on ``django.jQuery`` namespace.

### Screenshots

##### Google Map Point Field Widget

![](https://cloud.githubusercontent.com/assets/1518272/26807500/ad0af4ea-4a4e-11e7-87d6-632f39e438f7.gif)

##### Google Map Static Overlay Widget
This widget is working with <a href="http://dimsemenov.com/plugins/magnific-popup/" target="_blank">Magnific Popup</a> jQuery plugin.

![](https://cloud.githubusercontent.com/assets/1518272/18732296/18f1813e-805a-11e6-8801-f1f48ed02a9c.png)


### Release Notes

#### v0.2.0

> -   Fixed Python 3.6, Django 2.x compatible issues. 
> -   Fixed SRID format converter issues. 
> -   Removed `pyproj` package dependency.
> -   Various development infrastructure updates. (Docker, Fabric files etc.)
> -   Point map widget JS objects associated to the map HTML elements with jQuey `$.data` method.
> -   Passing Google Place AutoComplete full response object to jQuery triggers.

#### v0.1.9

> -   Google Place Autocomplete object binding to jQuery triggers.
> -   Implemented Google Geocoding support for the marker coordinates.
> -   Added custom widget settings feature for each widget.
> -   Added Portuguese localisation support.
> -   Fixed Google Place Autocomplete widget bugs in Django Admin Inlines.
> -   Fixed Python 3.6 errors.
> -   Fixed Javascript bugs.
> -   The GitHub repository Integrated with Travis CI.
> -   Implemented unit tests for backend code. (%100 code coverage)
> -   Change development environment from Vagrant to Docker.


#### v0.1.8

> -   Full documentation integrated to readthedocs.org.
> -   Fixed Google Map static widget issues.
> -   Added Russian localisation support.
> -   Added [Google Places Autocomplete] options support.
> -   Fixed CSS issues.
