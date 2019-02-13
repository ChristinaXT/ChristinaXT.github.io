---
layout: post
title:      "CLI Data Gem Project Completed"
date:       2019-02-13 02:44:19 +0000
permalink:  cli_data_gem_project_completed
---

I am happy that I had to go back and really dig in more after the first assessment because I learned so much from this project. I had created the code in several attempts with time lapses in between, as things have been crazy at home with new baby and I hadn't been able to focus time in large blocks. Going back in, I realized I had created extra, redundant code that made everything really confusing.

I had some guidance from CLI office hours with Jenn, and after really working through each section, class, method, object and so on, I was able to slim it all down and only include clear and straight to the point code. I had made it much more complicated than it needed to be the first go around, which actually was quite a relief when it became much simpler. I now feel comfident that I could repeat this again in real applications. 

One thing I would remind anyone who is scraping to do is to not forget about the arrays in some of the HTML. I got stuck at one point and could not figure out why what I was scraping was outputing extra information that was on the same line as the info I wanted to capture. Then I realized that if I tried to break it down and number each item (array), I would be able to capture only what I needed. 

For example: 

	school_xml.css("div.search-result-fact")[0].text, #acceptance_rate
	school_xml.css("div.search-result-fact")[1].text, #cost


The first line above scrapes data for the acceptance rate for the top 25 colleges for theatre arts and the second line scrapes data for the yearly cost. These items appeared next to each other on the same line and when capturing the data for them, the HTML code looks identical. If you do not include the numbers for the array of items on the same line (and don't forget to start with zero), then your output will include everything on that line that is included in the same HTML code for that particular array.  At first, I was not adding the [0] and [1] and I was getting the acceptance rate and cost together on each line of output. After I put the array numbers in, I got only the data I wanted on each line. 

https://github.com/ChristinaXT/Niche_TS









