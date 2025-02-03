---
title: Building a Book Lending App in Apple Shortcuts
layout: post
---

Apple Shortcuts is, in my opinion, a rather undersold feature of the iPhone. It’s basically a complete programming language that can be used to hack the features of your phone to no end. Certain apps integrate with it very well, like [Instapaper](https://www.instapaper.com/) and [Bear](https://bear.app/). You can grab a certain number of elements from an RSS feed, and the open your link of choice in Instapaper — so that without any separate app, you now basically have an RSS reader. You can take a list of ingredients from a recipe and export them into a shopping list. You can set a Do Not Disturb focus, bring up a reading focus music playlist, and open your favorite reading app. You can query APIs and trigger shell scripts. You can create pipelines of shortcuts processing data and sending it along to other shortcuts.

I made a Shortcut recently that basically acts as a [book lending app](https://www.icloud.com/shortcuts/63e26f9d08ac42feb3c0f8dcd02a4688). You get the ISBN from the book (perhaps using the camera to grab the text), and the shortcut queries the [Open Library API](https://openlibrary.org/developers/api) to get some basic data about the book (really only the title at this point, though at the future I plan to have it grab the cover picture as well). It then asks you how long this loan should last, and bundles all this information together into a note in Bear and then sets a reminder for the due date. 

By the way, this is a really handy [list of public APIs](https://github.com/public-apis/public-apis?tab=readme-ov-file). 
