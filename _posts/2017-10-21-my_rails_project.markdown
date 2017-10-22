---
layout: post
title:      "My Rails project"
date:       2017-10-22 00:31:11 +0000
permalink:  my_rails_project
---

This project is certainly the most complex thing I've built for the course! I finished the majority of my Sinatra project over only two days (and it probably would've been one day if I hadn't spent so much time on the css). In contrast, my Rails project has taken nine days to feel ready.

My project is a website for fiction writers to keep track of their writing projects and to share their progress with other writers. I decided that users would have many Projects, and that each project would have many Progress Updates. Projects would also have Genres, so that they could be easily sorted into different types. And Progress Updates would have Comments, allowing users to cheer on their colleagues.

I wanted to keep the complexity down for the first version, so there were some other ideas that I scrapped but may return to later: users being able to friend each other, a Facebook-style "like" feature, a project status field to indicate things like "First Draft," personal user word goals, and tracking a project's progress over time.

I started with figuring out what my database and routes would look like, keeping in mind the project requirements. Once I got those working I set up Devise user authentication. This ended up being a bit challenging since I knew I wanted to include a name and avatar for each user, which involved customising the default settings. Getting the avatar image to crop and scale correctly turned out to be the hardest and most frustrating part, since one of the image manipulation methods in the carrierwave gem wasn't working the way all the documentation said it was supposed to. Thank goodness for experimentation and Stack Overflow!

I decided to use Bootstrap as a base for the design, since I wanted to get more experience with the framework that so many people use. I really appreciated how easy it made everything, especially styling all the form fields. I also added some of my own styles on top of Bootstrap and used the opportunity to try out some SCSS, though I suspect I didn't take advantage of its features nearly as much as I could have.

The project was also very helpful at solidifying my understanding of nested forms, partials/helpers, and scope methods. It can be hard to remember all the little details of how everything works, so playing around with them in my own project was a nice review.

GitHub link: https://github.com/Cecily2/writing-project-tracker
