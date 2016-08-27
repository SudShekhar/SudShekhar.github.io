---
layout: post
title: "Getting rid of username in Django"
date: 2016-08-13 00:42:56 +0530
comments: true
categories: Django, Programming 
---

Django is an awesome web framework. But one of the problems of being a very old and mature framework is that it
comes with a lot of features and attributes that you just don't need anymore.
Features such as username. Reddit, twitter etc have usernames but unless you're
sure you will be soon joining their ranks, do you really want to burden your
users with yet another username to remember?

It makes a lot of sense to let go of the username completely and just use the
email id as your identification field.

Below are the steps, should you choose to do that

### Replacing Django Auth User with an Email user

 - Install the
     [**django-custom-user**](https://github.com/jcugat/django-custom-user) app
        
        pip install django-custom-user

 - Add `custom_user` to your `INSTALLED_APPS` settings
    
        INSTALLED_APPS = (
            # other apps
            'custom_user',
        )

 - In your settings.py file, set `AUTH_USER_MODEL` to use `EmailUser`:
    
        AUTH_USER_MODEL = 'custom_user.EmailUser'

 - Create the database tables:
    
        python manage.py migrate
 
 - In whichever file you've used the contrib user model add this line: 

        import settings.AUTH_USER_MODEL as User

And you're done! The app will automatically handle all the use cases you can
think of and many you won't.

This is why, Django is awesome.
