---
layout: post
title: Analysing my reading habits from Goodreads data
subtitle: Data visualisation
tags: [data science, projects]
comments: true
---

[Goodreads](goodreads.com) is an amazing platform for tracking and organizing your reading, discovering new books, and sharing reviews or recommandations with friends. I downloaded my library (from My Books > Tools > Import and Export > Export Library), which included the book titles, authors' names, publishing year, number of pages, the average book rating on goodreads and my rating. For extra fun, I added two dimensions to the dataset: the author's country of origin and the language in which I've read the book.

On my quest to becoming a data scientist, I've recently played with [my goodreads](https://www.goodreads.com/Lorenanda) data to get some insights into my reading habits in the past six years. You can have a look [here](https://github.com/lorenanda/goodreads) at the full dataset and basic analysis with Python. For a quick and colorful overview, I create two interactive dashboards: [one in Google Data Studio](https://datastudio.google.com/embed/reporting/1G4jH00ImVcFU1c8X_wFyWRNP2SN6v5WH/page/Ivkh) and one in [Tableau](https://public.tableau.com/profile/lorena.ciutacu).

In this post I'll focus only Tableau. First of all, I mapped the books I've read to have an overview of **my global library**. The color gradient represents the count of books read from that country -- the darker the color, the more books. In the Tableau viz you can hover over each country to see the exact number of books.

![map](https://lorenaciutacu.files.wordpress.com/2018/10/map-e1539944679944.jpg?w=736)

Since I've graduated a bilingual Romanian-English highschool and a BA in German and French Translation, I've mostly read American, British, Romanian, French, and German literature. And also a good share of Russian classics to sharpen my heart. Looking at the map made me realize what a small part of the world how little I've actually read. Even of European literature, I've only read works from some of the most prominent countries, not to mention the other continents. Moreover, this indicates the American influence on the book market, which also reveals the power of translation, looking at what authors are promoted and given a voice across borders by translating their works into widely spoken languages. Consequently, I've decided to read at least one book from each country in the world, so please let me know if you have any recommandations.

Next, I was interested to see **how many books I've read every year, monthly.** Seems like 2016 was my bookaholic year, with a whopping 37 books, of which 8 read in July. That was time when I was writing my BA thesis, travelling often for a long-distance relationship, and spending many nights paralyzed with anxiety, so naturally I turned to books for inspiration, distraction, and consolation. Based on the pattern of the past six years, Tableau helped me predict that in 2018 I will read 17 books or 7087 pages, and in 2019 25 books or 8576 pages. Let's see how that goes...

![yearly book count](https://lorenaciutacu.files.wordpress.com/2018/10/yearly-book-count.jpg?w=736)

![reading timeline](https://lorenaciutacu.files.wordpress.com/2018/10/reading-timeline.jpg?w=736)

I've rated most of the books I've read with 4 stars out of 5, which indicates that (a) I've read mostly subjectively good books, (b) I'm generous with rating, (c) I only bothered to rate books that I really liked, (d) I only continued and finished reading books that I liked.

![histogram my rating](https://lorenaciutacu.files.wordpress.com/2018/10/histogram-my-rating.jpg?w=736)

I'm a polyglot and reading literature is my favorite way to learn languages. Whenever possible, I prefer to read books in their original language or, if I don't speak that language or I can't get the original edition, then in a related language or ultimately in English. This is in fact the **language in which I've read** more than half of the books in the past six years, even more than in my native language Romanian.

![languages](https://lorenaciutacu.files.wordpress.com/2018/10/languages-e1539946580647.jpg?w=736)

This is my first Tableau viz and it was exciting to learn the software with the goodreads data. Tableau is quite intuitive to use and offers some [helpful tutorials and datasets](https://www.tableau.com/learn/training)[, ](https://www.tableau.com/learn/training)which makes data analysis so playful!