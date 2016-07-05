---
layout: post
title: My Ruby CLI Gem
---

**Overview:**

As a part of Flatiron School's [Learn](https://learn.co/){:target="_blank"}, I have just completed my first [command line interface Ruby gem!](https://github.com/sameera91/ted-talks-cli-gem/){:target="_blank"} This project involved gathering data from a website and then displaying the information back to the user. I thought about a number of different websites I could scrape for this project, but I picked the one that immediately stood out. I’m a huge fan of TED talks and wanted a quick way to see some of the most popular talks today. I even wanted a way to drill into a specific TED talk and learn more about it, so I’ve decided to scrape the [TED Talks](https://www.ted.com/talks){:target="_blank"} website. 

The basic requirements for the project were as follows: 

1.  Package as a gem
2.  Provide a CLI on gem installation.
3.  CLI must provide data from an external source, whether scraped or via a public API.
4.  Data provided must go at least a level deep, generally by showing the user a list of available data and then being able to drill into a specific item.

When the user runs the gem, a list of categories (e.g. science, business, technology, design) is displayed. The user can then choose a category and get a list of the top 10 TED talks in that category. Additionally, the user can enter a search term and get a list of the top 10 talks relating to that term. When the user selects one among the top 10 talks, they see more detailed information about that specific talk. Here's a visual of the command line interface:

List of categories:

![Categories screenshot](/img/categories.jpg)

List of talks:

![talks screenshot](/img/talks.jpg)

Talk description:

![description screenshot](/img/description.jpg)

**The Process:**

Before I started coding, I thought about the number of classes I wanted to have and the purpose of each class. After some thinking, and using Avi's [CLI Gem Walkthrough](https://www.youtube.com/watch?v=_lDExWIhYKI){:target="_blank"} as a helpful guide, I created three separate classes — a TedTalks::CLI class, TedTalks::Talk, and TedTalks::Info class. The purpose of the CLI class was to list the different categories and talks and allow the user to choose from the options on the command line. The basic flow of the class is defined within the call method:

![CLI method screenshot](/img/cli.jpg)

One of the most interesting parts of this project was getting information from the [TED](https://ted.com/talks){:target="_blank"} website. In the TedTalks::Talk and TedTalks::Info classes, I used the Nokogiri Ruby gem to scrape relevant information such as the title, author, date and rating of a talk. This appeared to be challenging at first, but chrome developer tools made the process of finding the exact CSS selectors rather efficient. Here's a code snippet of how I used Nokogiri and CSS selectors to gather the data:

![scraping method screenshot](/img/scrape.jpg)

Once I had scraped the information from the TED talks website, I had to display the information back to the user! 

![list_talks method screenshot](/img/list_talks.jpg)

**Challenges:**

This was an enjoyable project, but I did encounter some challenges along the way. The first one was getting my code to be more efficient. I had just learned about DRY (don’t repeat yourself), and worked to make sure I didn't repeat any line of code too many times. For example, after obtaining user input, I used if statements to determine what the program does with each possible user input value. Initially, I had twice the number of if statements that I have currently — one for every category and its number. However, I later decided that it would be easier to store input values in a hash and iterate over them. When the user enters in a number, I use the hash to get the word that corresponds to the user input, and store that word in the input variable. When I implemented my code this way, I found that I greatly reduced the number of if statements.

![hash method screenshot](/img/hash.jpg)


I had initially also placed the functionality of scraping both the list of TED talks and the individual talk info into just one class, but then later decided that it may be more efficient to place both of these into separate classes. This way, each class was responsible for just one set of information.

At the end, I had three different classes and a working Ruby gem! I now have a way to go through TED talk information through the command line. In the next few days, I will go through a code review, improve upon what I have, and publish the gem!