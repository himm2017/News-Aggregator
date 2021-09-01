# News-Aggregator
DESCRIPTION:

In this Python django project, you will learn to build your own news aggregator web application by integrating Django with other technologies.

You need to have some basic knowledge of these libraries:
Django Framework
BeautifulSoup
requests module

What is a News Aggregator?

It is a web application which aggregates data (news articles) from multiple websites. Then presents the data in one location.News aggregator service is a very important start of the day.There are various publications and news sites online. They publish their content on multiple platforms. Now, imagine when you open 10-20 news sites every day. The time you waste to gain information. Information gain is everything in today’s world.It can give you leverage over those who don’t have it. Now, is there a way we can make it easier? Yes!!
A news aggregator makes this task easier. In a news aggregator, you can select the websites you want to follow. Then the news aggregator collects the articles for you. And, you are just a click away to get information from various websites.This task otherwise takes too much time on our schedule.

About the Django Project:
A news aggregator is a combination of web crawlers and web applications. Both of these technologies have their implementation in Python. That makes it easier for us.So, our news aggregator will work in 3 steps:

It scrapes the web for the articles. (In this Django project, we are scraping a website called theonion)
Then it stores the article’s images, links, and title.
The stored objects in the database are served to the client. The client gets information in a nice template.
So, that’s how our web app will work.

You can find the complete source code of this Django project in this Github repository:

News Aggregator Files:

Also, check out the page of theonion website before proceeding.

So, let’s get started.

Steps to Build Django Project on News Aggregator App:
Before starting, we will need to install some of the libraries. We will install the requests and BeautifulSoup libraries. You can install them using pip.
Now, we will make a new Python Django project named DataFlair_NewsAggregator. Then we will make new application news.
Move into the folder where manage.py is present.
Writing Models:
We will be storing the urls and articles in our database. For that, we will need the model.
In news/models.py, create these models

Our models will be able to store three things:
Title of the article
URL of the origin or source
URL of the article image

We are using simple model fields for that purpose. Also, the image field can be blank. The __str__() method will return the string representation of the object. These are simple Django concepts.

Now, let’s start with the steps for web crawlers.

Step 1 :
Scrape the website
We will be scraping the website for getting articles. Web-Scraping means extracting data from the websites. We extract meaningful data from the websites. In this case, we will be extracting the articles from the theonion website.
To scrape the website, we will use beautifulsoup and requests module. These libraries are the bs4 and requests and modules are used for web crawling.
Open news/views.py file.
First, import these libraries before using them.
We will be making the first view function as scrape().
This view function uses modules like requests, bs4 and Django’s shortcuts.
We have imported the model Headline from news.models. Also, we have other libraries.

The first line of the function is a setting for requests framework. These settings are necessary. They will prevent the errors to stop the execution of the program. Then we write our view function scrape(). The scrape() method will scrape the news articles from the URL “theonion.com”.
The first variable is the session object of the requests module. These are essential to make a connection to the server. This is the abstraction provided by requests framework.
The session variables have headers as HTTP headers. These headers are used by our function to request the webpage. The scrapper acts like a normal http client to the news site. The User-Agent key is important here.
This HTTP header will tell the server information about the client. We are using Google bot for that purpose. When our client requests anything on the server, the server sees our request coming as a Google bot. You can configure it look like a browser User-Agent.
That won’t affect our use-case though. After that, we introduce the content variable. We store the webpage or response given by the server in content. Now, the beautifulsoup comes in.
The beautiful soup is a library that can extract data from HTML web pages. We create a soup object where we pass the HTML page. Alongside the HTML page, we also pass HTML parser as a parameter.
The HTML parser will parse the HTML as a BeautifulSoup object. In this object, we can access HTML elements and their texts.
In the News object, we return the <div> of a particular class. We selected this class from the webpage inspection. We inspected the webpage of the website theonion. Now, we select the elements which have the information we need.
As you can see from this image, by inspecting the element, we find a common class. The rest is just extracting information from that element.
Now we get 3 elements of this class. That means that the three articles are present in this class. These articles have a very general structure. Now, we will extract the information which we need. In this case, we have to extract the title, link, and image link.
Using a for loop, we can iterate over soup objects. In the for loop, the main variable will hold the link to the origin webpage. The main attribute gets the anchor tag. Since, the <div>s returned only have one <a>tag, we get most of our work done here.
The <a> tag contains title and href of the original link. We can access the href in <a> tag by writing main[‘href’].
Similarly, we can extract the title by main[‘title’]. Remember the main is the <a> tag beautifulsoup object.  
Then we find the image URL. To get the image_src, we find the image in the main. This is all according to the webpage layout. We are not doing this because of syntax.
These are how the website has made its webpage. We are simply finding the elements and accessing them appropriately. You need to have some basics clear of beautiful soup and HTML.
So, once we get the image, we extract the srcset attribute from the same.  
 
The srcset attribute contains various sizes of images, as we can see in the image. There we have to extract the size of the image which is big enough for us. We select the one with 800 width.

We get a string that has the source of the image and its width. And, we can travel over that list using Python indexing. As you can see in the code, we use the split() on the string to get a list. There we use index [-4]. That will give us the URL of 80 width image. That is stored as string in the image_src variable. 
  
  Step 2 :
Store the data in the database
We have made our model Headline for this purpose. Now we will be performing the standard storing procedure. We create a new Headline() object. There we fill the corresponding fields.
This the standard code for storing in the database.

Step 3 :
Serve the stored database objects
This step is very easy too. We create a new view function for this purpose. That is news_list() method. The code lies in the file news/views.py file.Here is a simple Django code. We simply extract all the elements from the database. Since we want the latest info on top, we reverse the list. Then we simply pass the list in a context. The context is then given to home.html in folder news/template/news.
  
Writing Templates
Here is the code for home.html. In this template, we are using bootstrap and HTML. The code in the home.html:
The basic knowledge of bootstrap and HTML can help here. It’s a simple Django template.
We have provided a link to the scrape view function. At line 10, the link to the scrape view function is provided. We will be defining our urls and then you will have a clearer picture.
Then at line 15, our news logic is written. Here we print the news objects one by one. The for loop is used for that purpose.
  
Configuring urls.py
Last, we configure our urls.py file. Make a file news/urls.py. Paste this code inside the urls.py. 
Then we also need to connect this to main urls.py. Open DataFlair_NewsAggregator/urls.py file and paste this code inside that or update it.
This is the normal Django code to connect urls.
So, our Python example project is complete. Let’s run it and see the homepage. In this case, when we open server and run news_list view.  
You can click on the links. That will take you to the original article page.
Now, you can configure this to gather your favorite article websites. Although, be wary of blocks. Many times, bots are not legally allowed to scrape content. So, web scraping comes at its own cost.
But, for our purpose, we now know some very cool basics. We also have a very interesting project to showcase. You can enhance this Django application as much as you can.

Summary:

  We have successfully completed the first project in Django. We are using web scraping and Django. This integration is as easy as invoking a function in Python.
You can make some more projects in Django using the same concepts. Django lets you integrate machine learning too.
  








