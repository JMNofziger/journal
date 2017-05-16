+++
author = "JMN"
categories = ["Tech"]
date = "2017-05-15T18:12:15-07:00"
description = ""
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "Initial Django Env Setup"

+++

![Image](http://docs.django-cms.org/en/release-2.4.x/_images/it-worked.png)

Django is a web framework that runs on python. Now that I've gotten well acquainted with the python syntax exploring Django has become much more intriguing. In this post I work through the DjangoGirls intro to Django tutorial which was presented in Seattle in April 2017. One of my classmates attended (Margarita) and passed on the tutorial to me. You can find the walkthrough here: https://tutorial.djangogirls.org/en/

In this post I'll just summarize the setup through the point at which Django serves its default project page. Don't wanna read mine? Try the --[tldr](#tldr)--

The tutorial begins with a general explanation of how requests to web servers are handled. The good ol' post office analogy is used. This is followed by a command line crash course which guides the user through a few common commands on the operating system of their choice. Finally, we're introduced to Python. 

This section begins with a guide for installing Python and the tutorial calls for users to use version 3.5 (As of May 2017). I actually had 3.6.1 installed and everything worked fine. Curious what version you might be running? Try the following command in your terminal.

```shell
python --version
```
From there the tutorial introduces the user to code editors and basic Python. This is a long section and probably intense for a newbie but now a total breeze for a three month pro like me. I did a quick skim and it seems legit, maybe even overwhelming for a new learner. For someone in that situation I'm sure the group setting with coaches would make the experience much better. This section also includes links to videos to accompany the reading for those more visual learners. 

Django is introduced and a quick overview of web frameworks is given. We meet Django's **urlresolver** which takes a list of patterns and tries to them to the URL; if a match is found the request is passed on to the associated function (the **view**).

We are then taken through setting up a virtual environment to isolate our Python/Django setup for this project. This is followed by using pip to make sure the pip package is updated and then installing Django. I've summarized the commands below (remember, I'm using Arch Linux).

First the creation of the virtual environment within your chosen project directory. You can choose whatever name you please for your venv but I would keep it short.
```shell
python -m venv jacobs-venv
```
Quick explanation of the above syntax. We are calling python from the command line and supplying the *venv* module as the argument for the -m option. The -m option indicates to python that a module-name will be supplied for execution. You can check out the python *man* page or [python documentation about the cli environment](https://docs.python.org/3.6/using/cmdline.html) for more information about the different options available and you can see the following python module documentation for information about [the *venv* module](https://docs.python.org/3/library/venv.html).

Sweet. Now we activate our virtual environment by running our source command on the activate script found within the bin folder of our newly minted virtual environment.
```shell
source jacobs-venv/bin/activate
```
The *source* command will read and execute commands from the supplied file (in our case the 'activate' file found within the venv bin directory) and is a Bourne Shell built-in command. You can read more about *source* on [Simon Sheppard's site](https://ss64.com/bash/source.html) or directly on [the GNU documentation page](https://www.gnu.org/software/bash/manual/bash.html#Bourne-Shell-Builtins-1).

Now, with our virtual environment activated, we use pip to make sure that pip is up to date. Meta. 
```shell
pip install --upgrade pip
```

That seems pretty self-explanatory. Pip is a package management used to install and manage software packages written in Python. I took that definition from the [pip (package manager) wikipedia page](https://en.wikipedia.org/wiki/Pip_(package_manager).

Finally we install Django using pip. The tutorial requests that we use a version greater than or equal to (~=) 1.10
```shell
pip install django~=1.10.0
```

You should then see pip's installation progress bar which I think is very cool. Cooler than Arch's pacman default progress bar? Yes. Cooler than Arch's pacman [pacman progress bar]( Linu://wiki.manjaro.org/index.php?title=Progress_Bar_as_Pacman_Eating_Power_Pills)? No. 

Wait, [nevermind](https://pypi.python.org/pypi/pacmanprogressbar/). Thanks Jesus.

Anyhow, now we have our venv configured, pip up to date, and django installed. Yay! Now we will run some django scripts to get our site skeleton set up. 

```shell
django-admin startproject mysite .
```
This django-admin script with the startproject argument creates the default site directories and files within a directory with a name of our choice ('mysite') and placed at a location of our choice ('.' or in other words, here). You can read more about [django-admin](https://docs.djangoproject.com/en/1.11/ref/django-admin/) and the [startproject](https://docs.djangoproject.com/en/1.11/ref/django-admin/#s-startproject) on the official django documentation site. 

The tutorial then has us make some adjustments to our settings.py file that was generated by the *startproject* command but we'll pass over that now. We then create the database for our site sing the manage.py migrate command. By default Django is set up to use sqlite3 as it's database. Remember we should still have our venv activated.

```shell
python manage.py migrate
```
You should then see a bunch of output with 'OK' status endings. Nice. Now we run the command to start the web server and check out our skeleton site in the browser.

```shell
python manage.py runserver
```

This should server your site at http://localhost:8000 or http://127.0.0.1:8000 by default. Your commandline will show requests to your 'server' and the status code associated with the request. You'll probably see a 404 for a favicon request since there is no favicon resource.

And that's that! Django is set up within a venv isolated within a project folder and serving up its skeleton site based on the default database.

<a name="tldr"></a>

---

### tldr
I just summarize the first 10 sections of the [Django Girls Tutorial](https://tutorial.djangogirls.org/en/). 
