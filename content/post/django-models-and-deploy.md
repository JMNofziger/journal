+++
author = "JMNofziger"
categories = ['Tech']
date = "2017-05-20T13:42:55-07:00"
description = "In which we learn about Django object models and deploy our work to the WORLD WIDE WEB..."
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "Django Models and Deployment"

+++

Finally had some free time to come back to my prepared Django environment and mess around with a starter project. You can follow [the same walkthrough I did](https://tutorial.djangogirls.org/en/django_models/). I'll just highlight some of the interesting things learned.

1. Object Models and Django
  1. Objects - a way to describe real things in code with properties and actions 
    1. object properties == property of a thing
    2. methods == actions of a thing
  2. Applying object model to Django blog posts 
    1. properties: title, text, author, created\_date, published\_date
    2. methods: publish
2. Applications and Django
  1. Create separate apps within prject to keep things organized
    1. Create app with manage.py 'startapp' command
      ```shell
      python manage.py startapp yourappname
      ```
    2. Update your settings.py file to reflect new app, create list of database fields that the model defines.

The [Django models documentation page](https://docs.djangoproject.com/en/1.11/topics/db/models/) has great introductory information but also dives way deep (you know, documentation style) once it has the basics covered. Another super cool django doc page is the [Model instance reference page](https://docs.djangoproject.com/en/1.11/ref/models/instances/) which explains that each model you make is a python class that subclasses 'django.db.models.Model'. Whatcha know about [inheiritance in Python](https://docs.python.org/3.6/tutorial/classes.html)?

After creating our model and  migrating the model to the database, we register the model to our app admin page to make it visible there. This will serve up the Post model for us through the admin view. We will have to log in to see that so first we need to make our Django superuser with the 'createsuperuser' command. Nice. 

Then we login with our baseurl (in this case localhost:8000) with the '/admin' directory appended to the url name. 

The next section covered deployment and I was going to skip it because ~~*ya boy is a \_\_woke\_\_ playa*~~ but then I read through it and was like, ~*this is actually interesting*~

By this point the DjangoGirls tutorial has set you up with a local dev environment. Their deploy step has track changes by setting up a github repository for your project and then host your application on [PythonAnywhere](https://www.pythonanywhere.com/). 

I had never heard of PythonAnywhere and once I started reading about it I got interested in this step. PythonAnywhere allows you to host small applications with low traffic for free. That means all your learner projects hosted for free, available online for you to link to on your portfolio site. Nice! ***yes, I know about github pages, codepen, free digital ocean credits, blah blah blah...*** but if you do know other good resources for free deployment of learner projects... lemme know.

I had already set up a git repository for this project and needed to update my .gitignore file (a file that tells git which files to ignore as it track for changes). After updating that list to match the DjanoGirls setup I needed to get my repository to remove the files no longer being tracked. One quick google search later resulted in [a stack overflow post made for me](https://stackoverflow.com/questions/13541615/how-to-remove-files-that-are-listed-in-the-gitignore-but-still-on-the-repositor). 

Here's the basic command for removing the now 'untracked' files from your repo:

```git
git rm --cached filename1 filename2
```

But that's annoying and Samy Dindane says that if you have access to the bash terminal you can run a command to totally skip the manual input of files:

```shell
git rm --cached `git ls-files -i --exclude-from=.gitignore`
```
And that worked like a dream for me. Beleza! Read up on [git rm --cached vs. git reset -- ](https://stackoverflow.com/questions/12661306/git-rm-cached-file-vs-git-reset-file) and [git ls-files and related flags](https://git-scm.com/docs/git-ls-files) and [.gitignore](https://git-scm.com/docs/gitignore) to your delight... 

Cool, once that was resolved I could clone my project onto my PythonAnywhere environment and reconfigure my settings for 'production'. PythonAnywhere is pretty fun but my excitement was a lil tempered by the realization that your projects are limited to a three-month lifespan. But then elevated again by the realization that you can renew via email when the expiration draws near. [They're actually pretty sweet about this all.](http://blog.pythonanywhere.com/129/)

We then modify our wsgi.py file to reflect our project location, django site settings file, and how we want our static files to be handled. And that's that. You reload your app on PythonAnywhere and bam! Your site is live at your chosen subdomain. 

Baiiiii!
