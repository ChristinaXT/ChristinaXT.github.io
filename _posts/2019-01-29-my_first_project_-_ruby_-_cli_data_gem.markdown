---
layout: post
title:      "My first Project - Ruby - CLI Data GEM "
date:       2019-01-29 14:46:53 +0000
permalink:  my_first_project_-_ruby_-_cli_data_gem
---



Hi, well, this has been fun and crazy and frustrating and a bit disconnected, but mainly fun. I have learned so much in this project, and I still trying to figure out if the code I scraped is working correctly, but for the most part, I am happy with what I have done. It took me quite awhile to do this project, but not because it is too difficult. It is because I had a baby (5 months old now) and sometimes, just when I am getting a really good flow, I have to stop and it is sometimes difficult to find that frame of thought that was leading me. I have been trying to keep as many notes as possible to help with this. 

I decided for this project that I would scrape a website about the top ten Theatre Arts performance colleges in the United States since that was my undergraduate degree and experience. You can type in the number according to ranking and read about the school's name, address, see a link to their website, read about the cost per year and the program details. 
https://www.niche.com/colleges/search/best-colleges-for-theater/ 

I watched all the suggested videos and read all of the source articles on the past CLI and Scraping labs and readmes as well. I watched videos of other students' projects and read a ton of blogs. I took forever to get started because I was terrified that I was not ready.

Once I actually started, I felt silly that I was so afraid this. Avi's video is extremely helpful and I followed all his instructions, rewound the video a lot and watched certain parts over again until I completely understood. 

Writing the code is fun and I realized that I really did learn something in all those labs and I understand this code writing thing without really understanding how or why I understand it.

My code was inspired by a combination of links I read and I am still hoping that I put it together correctly. 
I wrote the code first and added all the files and connected them together by adding the requires. 

I created the class and Attr_accessor to distinguish the items we are looking to learn about with the scrape:

```
class Niche_TS::School
	

	  attr_accessor :name, :location, :url,  :rank, :cost, :acceptance_rate
			
			
		My lib file : Niche_TS/lib/Niche_TS.rb
		
		looks like this: 
		
		require_relative './Niche_TS/version'
    require_relative './Niche_TS/scraper'
    require_relative './Niche_TS/school'
    require_relative './Niche_TS/cli'

    require 'pry'
    require 'nokogiri'
    require 'open-uri'
```
	 
	 

	 
I am used nokogiri for the scrape gem. I used the google chrome tools  -View-Developer  - Developer tools.
	
I then highlighted the information I wanted to scrape, right clicked and chose inspect. I then scraped the code that was left highlighted and placed it in my written project code. 

Example of what this looks like:
	
![](https://www.google.com/search?biw=1327&bih=596&tbm=isch&sa=1&ei=WRtPXP-CK8_i_AaQkYKIBQ&q=view+developer+developer+tools&oq=view+developer&gs_l=img.1.2.0i24l10.3549.10491..15561...2.0..0.95.770.12......1....1..gws-wiz-img.xHVvgMIUUhg#imgrc=v9vZrl9KwdL57M:http://)
	
	
This is a fun project. After I finished, I ran the bin executable file to test. The only errors I am getting are the scraping sections.  I am still trying to figure out what I am doing wrong.
I am very close to submitting my project.
			
	
	
			
	
