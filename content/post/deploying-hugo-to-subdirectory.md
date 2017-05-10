+++
author = ""
categories = ["Tech"]
date = "2017-05-09T12:39:41-07:00"
description = ""
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "Deploying Hugo To Subdirectory"

+++

I've been exploring Hugo for a bit and decided that I'd like to deploy my fresh blog site to the /blog/ subdirectory of my https://jmnofziger.github.io base url. However, my attempts to do that locally resulted in resources not being linked correctly. CSS stylesheets couldn't be found, JS scripts couldn't be found; all my resources were return 404. An inspection with the browser console showed that resource URL's weren't being updated to reflect https://jmnofziger.github.io/blog/ as the base URL. Hmph! I confirmed the issue by correcting the elements and watching the browser correctly pull in the resources. Google'in time. I can't be the first loser who ran into this issue.   
