![Django CI](https://github.com/VuMedi/django-last-seen/workflows/Django%20CI/badge.svg)

# django-last-seen

Keep track of when a user has been last seen on a website.
The last seen time is kept on the database.

The app is ready for python 3.6, 3.7, 3.8 and django 2.2, it uses the AUTH_USER_MODEL setting to get
the user model,

## Installation

Install with ``pip install django-last-seen"`` or add ``"last_seen"`` directory to your Python path.

Add ``"last_seen"`` to the ``INSTALLED_APPS`` tuple found in your settings file.

Add 'last_seen.middleware.LastSeenMiddleware' to MIDDLEWARE_CLASSES tuple found in your settings file.

Run ``manage.py migrate`` to create the new tables

## Usage

To get when a user has been last seen::

```python
from last_seen.model import LastSeen

seen = LastSeen.object.when(user=user)
```


To save a last seen user without the middleware::

```python
from last_seen.model import LastSeen

# save with a special module
LastSeen.object.when(user=user, module='forum')
```

## Middleware

The provided middleware keeps track of when an authenticated user has been
last seen on the site,

If you want to keep track of a user last seen on a part of a site, you can
use a special module name and use::

```python
from last_seen.model import LastSeen

# save with a special module
LastSeen.object.when(user=user, module='forum')
```

Then to get the data::

```python
from last_seen.model import LastSeen

# user last seen on any part of the site
seen = LastSeen.object.when(user=user)

# user last seen on a module
seen = LastSeen.object.when(user=user, module='forum')
```

## Settings

**LAST_SEEN_DEFAULT_MODULE**: The default module used on the middleware. The default value is ``default``.

**LAST_SEEN_INTERVAL**: How often is the last seen timestamp updated to the database. The default is 2 hours.

