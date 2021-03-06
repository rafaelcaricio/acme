ACME Thumbnails
---------------

ACME Thumbnails is a thumbnail service to be hosted in google app engine.

It exposes urls like the following::

    http://mythumbservice.appspot.com/200x100/right/middle/somedomain.com/images/somepicture.jpg

Don't worry about what all of those mean. Suffice to say that this URL will
give us a 200px of width per 100px of height version of the image
'somepicture.jpg' in the best possible way.

Hosting the Service
-------------------

The best possible way for you to learn how to host this service is to check
Google App Engine tutorials on how to deploy an application.

The process is as simple as::

    * Create an application under your user in Google App Engine;
    * Change the app.yaml file to have the configuration 'application' contain
      that name;
    * Deploy and be happy.

URL Formation
-------------

Let's get the sample URL::

    http://mythumbservice.appspot.com/200x100/right/middle/somedomain.com/images/somepicture.jpg

Now, let's decompose that in parts:

* First comes the service hostname (http://mythumbservice.appspot.com);
* Then you get to choose the dimensions of your generated image, being
  width x height;
* After that comes two cropping arguments, horizontal align and vertical align.
  Those help ACME identify how to better crop your image;
* Last, but not least, comes the url for the image you want to generate. It's
  imperative that the image **IS NOT** preceded by http.

Now let's check the options we get for each argument.

Width
-----

The first argument you get to specify is the width. Some examples::

    http://mythumbservice.appspot.com/200x100/right/middle/somedomain.com/images/somepicture.jpg
    http://mythumbservice.appspot.com/-200x100/right/middle/somedomain.com/images/somepicture.jpg
    http://mythumbservice.appspot.com/200x/right/middle/somedomain.com/images/somepicture.jpg
    http://mythumbservice.appspot.com/x200/right/middle/somedomain.com/images/somepicture.jpg

In the first example we are specify 200px of width.

In the second we are specifying the same 200px, but we are saying we want a horizontal flip.

In the third example we are specifying we want 200px of width with proportional height.

In the fourth example we are specifying we want 100px of height with
proportional width.

Height
------

Analogue to width, but is the second argument in the size portion of the url.

A negative height specifies a vertical flip.

Horizontal Align
----------------

This part of the url specifies how we want images to be cropped if they need
horizontal cropping.

Possible values are::

    * left - crops right portion of the image (aligned left);
    * right - crops left portion of the image (aligned right);
    * center - crops same amount of the image on the left and right (aligned
      center).

Vertical Align
----------------

This part of the url specifies how we want images to be cropped if they need
vertical cropping.

Possible values are::

    * top - crops bottom portion of the image (aligned top);
    * bottom - crops top portion of the image (aligned bottom);
    * middle - crops same amount of the image on the top and bottom(aligned
      top).

Settings
--------

There's a settings.py file you can edit to change some built-in behaviors of
ACME thumbnails.

**ALLOWED_DOMAINS** are the domains that are allowed to use the service. They can
be specified using regular expressions. Some examples::

    'localhost',
    '(.)+.appspot.com', # not recommended, lol!

**ALLOWED_SOURCES** are the domains where pictures can come from. These domains can 
be specified using regular expressions. Some examples::

    'localhost',
    '(.)+.appspot.com', # not recommended, lol!

**QUALITY** is a setting that ranges from 1 to 100 and is used when converting JPEG
images.

**EXPIRATION** is the amount of seconds to wait before expiring an image conversion
in the cache. Defaults to 1 month.
