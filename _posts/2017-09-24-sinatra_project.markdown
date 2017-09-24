---
layout: post
title:  "Sinatra project"
date:   2017-09-24 20:26:35 +0000
---


I enjoyed finally getting to build my first actual web app project for the course. I had a lot of different ideas for it, but in the end I decided to save a lot of the more complex ones for later on and do a simple book tracking app with users and books. Users would have many books, and books would belong to a user.

Since I kept the structure of the app simple, it was pretty straightforward to get the database and all the models/views/controllers set up. I'm sure it helped that the curriculum makes us build very similar sites several times by the time we get to the Sinatra project (and I'd also used a similar pattern with Node.js for a different class, before joining Flatiron).

I thought it would be really cool if I could get the cover art for books that users entered, so I looked into APIs for book information and decided to try using the Google Books API. This wasn't part of the requirements, but I thought it would be a good opportunity to try to teach myself something new, and it makes my app a lot more usable and visually appealing.

I also got a bit carried away with CSS styling, since I have prior experience with that and always find it fun. I used [Masonry](https://masonry.desandro.com/) for the responsive grid and used media queries to adjust the number of columns and navbar position on different screen sizes.

You can view the github repository [here](https://github.com/Cecily2/sinatra-book-tracker) or view a preview of the design below.


<img src="https://i.imgur.com/ZghFTfi.jpg" title="source: imgur.com" />
