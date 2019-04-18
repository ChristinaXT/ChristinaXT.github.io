---
layout: post
title:      " Oh, Ruby, I Review You"
date:       2019-04-18 01:38:07 -0400
permalink:  oh_ruby_i_review_you
---

![](https://i.imgur.com/FvMuQons.jpghttp://)

**Class and Instance Methods**
     
		
Ruby is made up of objects. Methods allow objects to function and return values. Basically, a method calls for an action or function to happen within an instance or a class. Classes are also objects and a **Class Method** provides functionality to the Class.  An *Instance Method *does the same, but for an instance, not for the class.   A **Class Method** should be composed when the action you are going for does not apply to an instance of that class.
		 
 When creating a class method, the self keyword is needed; this is how we know we are defining a class method. 
	This is a class method example from the user model of my Sinatra App portfolio project:

			def self.username_check(username)
          self.all.detect do |user|
          user.username == username
       end
    end

		
The "self" keyword sets up this method so that it applies to the scope of the user class. 
		
Think of "class" as an actual classroom.  There are several students in one classroom and all of them want to sign up for a classroom provided email account. However, the system is set up to prevent more than one student to create a username that has been chosen by another student, no repeats. In order to create a method that will prevent this from happening, as applies to the entire classroom, we create a class method. 
	

	
Now, within this classroom, we have several students who want to access individual subjects for studyhall. Each of those individual subjects within the classroom would be a new instance. For this, we would create  **Instance Methods**. 
	
class Classroom
		 def subject_one
				 puts "science"
		 end


			def subject_two
				 puts "art"
		 end


		 def subject_three
				 puts "history"
		 end


		 def subject_four
				 puts "literature"
		 end
	end
________________________________________________________________________________________________________

Helper Methods.  are another type of method and are created to reduce the writing of excess code. They "help" us by providing shortcuts. Helper methods are written in the controller and are accessible in the views. You can also create a separate helper file in the directory and place your helper class methods there.  Here is an example of helper methods from my Sinatra App portfolio project from the application controller:



helpers do
	def logged_in?
		!!session[:user_id]
	end

	def current_user
		 User.find(session[:user_id])
	end

	def redirect_if_not_logged_in
		unless logged_in?
			redirect to "/login"
		 end
	end
		
Let's look at the last helper method. How would we call this helper method?
Let's look at this code from the Things controller of my project:
		
get '/things' do
 redirect_if_not_logged_in
	@things = Thing.all
	erb :'/things/things'
end

get '/things/new' do
  if logged_in?
	erb :'/things/new'
else
	redirect to "/login"
end
end
	
In the first section "get '/things' do", you can see how the helper method "redirect_if_not_logged_in" allowed our code to be crisp and to the point without excess data.  The helper was called in the second line of the code and we did not have to include all the extra code in the " get '/things/new' do". We could fix this by using the same helper method here:
	
get '/things/new' do
	 redirect_if_not_logged_in
		erb :'/things/new'
end

**Dot Notation** <br>
One of the coolest and most convenient things ever is dot notation. This allows us to assign a task to an object within a method by simply applying a dot.  Let's look at more code from my Sinatra app portfolio project:

delete '/things/:id/delete' do
      @thing = Thing.find(params[:id])
        if @thing.user_id == current_user.id
          @thing.delete
           erb :'/things/show'
        end
          redirect to "/things"
      end

The receiving object is the word before the dot and the message is the word that follows. In the second line, "Thing" is the receiving object and "find" is the message being sent to "Thing".  In the third line "delete" is the message and "@thing" is the receiver. Once an object has been established, you can use a dot notation to assign a task to it.  In the above example, the third line shows how the dot notation can be used with the objects identifier "user_id".   The dot notation is a handy little friend to play with when creating code. 



**Attributes, Readers, Writers, Accessors Shortcuts >> Getter and Setter Methods**

The specific properties of an object are called attributes. To review, methods provide the functionality of the object. Here is an example of code from my CLI Data Gem portfolio project:

class Niche_TS::School
	
   @@all = []
  
	 attr_accessor :name, :rank, :location,  :acceptance_rate, :cost, :description, :url
	
	 def self.all
     @@all
   end
end

In the above code, the attributes are name, rank, location, acceptance rate, cost, description and url.  This attribute accessor method displays a list of attributes for the object school class. 

You can also use the attribute writer to create setter methods and attribute reader to create getter methods. 

In addition, you can create getter methods yourself: 


class Student
def initialize(name)
    @name = name
  end
	 
  def name                                      # this creates getter method for name
    @name
  end
end

Zelda = Student.new('Zelda')
zelda.name                                      # this calls getter method and returns "Zelda" 



**The Initialize Method**

To complete the code from before:


class Niche_TS::School
	
   @@all = []
  
	 attr_accessor :name, :rank, :location,  :acceptance_rate, :cost, :description, :url
	
	 def self.all
     @@all
   end
      
    def initialize(name=nil, rank=nil, location=nil, acceptance_rate=nil, cost=nil, url=nil, description=nil)
	    @name = name
	    @rank = rank
	    @location = location
	    @acceptance_rate = acceptance_rate
	    @cost = cost
	    @url = url
	    @description = description
	    @@all << self
	  end
	    
	 def self.find_by_rank(search_rank)
     all.each do |school|
      if school.rank.gsub("#", "") == search_rank
      return school
      end	 
      end
   end
end 



If we want each instance of our class to include our attributes, an initialize method must be defined. The name variable above has the name attribute assigned in the line "@name =name".  Now when we can call on "school.rank, school.name, school.cost" and so on. 



**Parentheses and (Arguments/Parameters)**
The general rule is you use parentheses for most (there are a couple of exceptions) method calls that take arguments. The difference between params or parameters and arguments can be confusing if you think about too much. They both can use parentheses and there are many more complex ideas to spend more time on than this one. 


def method(args) 
end 


This is an example from the strong params lesson from Flatiron:



def create
  @post = Post.new(post_params(:title, :description))
  @post.save
  redirect_to post_path(@post)
end
 
def update
  @post = Post.find(params[:id])
  @post.update(post_params(:title))
  redirect_to post_path(@post)
end
 
private
 
def post_params(*args)
  params.require(:post).permit(*args)
end



**Square Brackets [ ] ** and **Curly Brackets { } **

In Ruby, I have come across *Square Brackets* when:

1) defining arrays:    Letters = [a, b, c, d...]

2) accessing the elements inside arrays and hashes.  

3) In Sinatra, for dynamic routing. 


get '/things/:id/edit' do
     @thing = Thing.find(params[:id])
    	 if @thing.user_id == session[:user_id]
    	  erb :'/things/edit'
   	  else
        redirect to "/login"
      end
  end


*Curly Braces *
Curly braces are usually found surrounding hashes and can also surround blocks. 


my_hash = {:a => 1, :b => 2, :c => 3}



In conclusion, this blog was meant to be a review to think out loud, and make sure I understand what the "H" I am doing. It is easy to take for granted that when studying and doing the readme lessons and code-a-longs that you will remember everything. This hasn't been the case for me.  It is easy to forget. There is so much information to grasp, learn and build on.  

When I get stuck, I take a break.  If I force myself to keep working with spots in my eyes, it creates a bigger mess of code and I get really lost or I learn incorrectly. If I take a break, sometimes for the entire night and start fresh later, I usually get it pretty quickly.  

Also, I have learned that this is not easy. So I have stopped beating myself up. It is okay to struggle with learning difficult things. The important thing is not to give up. 

Lastly, This is really fun. I actually love the challenge and I think one day, I will be an expert. My hope anyway!


