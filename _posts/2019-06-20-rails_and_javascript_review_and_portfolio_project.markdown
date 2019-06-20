---
layout: post
title:      "Rails and Javascript Review and Portfolio Project"
date:       2019-06-20 09:46:42 -0400
permalink:  rails_and_javascript_review_and_portfolio_project
---


At first, I was quite intimidated by Javascript. I was just getting really comfortable with Rails, and then JS came to dance and I wasn't sure if I liked the steps. 
<a href="https://imgur.com/PVN6SOd"><img src="https://i.imgur.com/PVN6SOd.jpg" title="source: imgur.com" /></a>

However, after a few tutorials and reviewing the labs for second time, I felt comfortable to start working on the Rails/JS portfolio project. This project expands on the the previous rails portfolio project but with added dynamic features using Javascript and JSON. 

The first step I took was to duplicate my rails app repository. I chose this instead of adding a new branch. I wanted to be able to have two separate repositories.  To duplicate the repository, I followed the method to mirror a repository as listed on [ https://help.github.com/articles/duplicating-a-repository/ ](http://)GitHub Help
First, I created a new repository (github help) [https://help.github.com/en/articles/creating-a-new-repository](http://) for the new Rails-JS app. I kept the same name I had for my rails project, which is BabyGuide, but added JS so the new project name is BabyGuide_JS. 

The next step I followed was to create a bare clone of the original rails app repository by typing in terminal without the paranthesis: 
( git clone --bare [https://github.com/yourusername/existing-rails-repository.git)](http://)
( cd existing-rails-repository.git)
( git push --mirror [https://github.com/yourusername/new-repository-js.git)](http://)

This mirror push copyied and pasted everything in the rails app repo into the new rails - JS repo. 

Finish up by typing in terminal (no paranthesis) 
( cd ..)
( rm -rf existing-rails-repository.git)

After this, I cloned the new repo I created 
( git clone git@github.com:yourusername/new-repository_js.git)
( cd new-repository_js) 

And we are ready to start new project :) 
<a href="https://imgur.com/5id2aJa"><img src="https://i.imgur.com/5id2aJa.jpg" title="source: imgur.com" /></a>

Next, I added jquery-rails and active_model_serializers to the Gemfile. 

**jquery-rails:** provides access to jQuery, a Javascript Library that simplifies DOM manipulation and AJAX requests, and the jQuery UJS adapter, enables JavaScript functionality for browsers that support it without negatively impacting browsers that don’t.

**active_model_serializers:** provides a Rails-y way to facilitate converting models into JSON by specifying attributes and relationships that should be present in the JSON version of your data.

In the Gemfile, I added active_model_serializers and gem ‘jquery-rails’ and then did a bundle install

( gem ‘jquery-rails’ )
( gem ‘active_model_serializers’ )
( bundle install )

<a href="https://imgur.com/YcF1V4b"><img src="https://i.imgur.com/YcF1V4b.jpg" title="source: imgur.com" /></a>

**Next step was to Add jquery and jquery_ujs to your Asset Pipeline**
Rails optimizes the use of **Javascript** and **CSS** through the **asset pipeline**. According to **RailsGuides**, The three main features of the pipeline are:

* Concatenate assets into one master .js and one master .css file to allow the browser to make one request for all JS and all CSS content (fewer requests —> faster loading)
* 
* Minify/compress files, moving them from a human-friendly format to the smallest possible version (smaller files —> faster loading)
* 
* Allow assets to be written in higher-level languages, such as Sass for CSS and CoffeeScript for JavaScript


`application.js` is a manifest file–a file that tells the Asset Pipeline which files it should include when it makes the minified, concatenated JS file to send to your browser.

This works through “directives”, a functionality enabled by the Sprockets gem, the gem that powers the asset pipeline. The syntax for a directive is: <br>


`//= require your_js_file` <br>

(This is where all JS requirements, including libraries (such as jQuery) and your own JavaScript files, should be listed.)

I added these:

`//= require jquery` <br>
`//= require jquery_ujs ` <br>
`//= require_tree .`  <br>

See the Rails Guide on the  Pipeline [https://guides.rubyonrails.org/asset_pipeline.html#manifest-files-and-directivesAsset](http://) to learn about how to add files from other directories to your application.js manifest.


We are getting there ... with the set up...
<a href="https://imgur.com/fFZ8Dvj"><img src="https://i.imgur.com/fFZ8Dvj.jpg" title="source: imgur.com" /></a>

**Next Step - Create the Serializer(s)**

I used the Active Model Serializers using generator - eg, 

`rails g serializer your_model` <br>

your_model_serializer_rb should look something like : <br>

	class YourModelSerializer < ActiveModel::Serializer 
			 attributes :id
	end
		
You can then remove and add the other attributes as you need, for example `attributes :id, :title, :body, :name`
		
	**Next Step -	Render JSON **
	
In the controller:

	
```
def index
			 @posts = Post.all
				respond_to do |format|
							 format.html
							 format.json {render json: @posts}
			 end 
 end 
```

			

**JSON** is short for **JavaScript Object Notation**

from my project :

```
class ChecklistsController < ApplicationController
         before_action :authorized_to_edit?, only: [:edit, :update]
         before_action :set_checklists, only: [:show, :edit, :update, :destroy]

        def index
            @checklists = Checklist.all
             respond_to do |f|
                 f.html { render :index }
                f.json { render json: @checklists}
          end
       end

       def new
           @checklist = Checklist.new(user_id: current_user.id)
        end

       def create #JSON rep of the checklist can be used without page refresh or redirect
          @checklist = Checklist.new(checklist_params)
                if @checklist.save
                   render json: @checklist
                  #redirect_to user_checklist_path(current_user, @checklist)
        else
                  flash[:notice] = "Your checklist creation was unsuccessful"
                  render 'new'
             end
       end



       def show
           respond_to do |format|
                format.html { render :show }
                format.json { render json: @checklist}
          end
       end

     def edit
          @checklist = Checklist.find_by(id: params[:id])
     end

     def update
         @checklist = Checklist.find_by(id: params[:id])
              if @checklist.update(checklist_params)
              redirect_to checklist_path(@checklist)
        else
             flash[:notice] = "Something went wrong, please try again"
             render 'edit'
         end
      end

      def destroy
          checklist = Checklist.find_by(id: params[:id])
          checklist.destroy
					redirect_to user_path(current_user)
      end


        private

      def set_checklists
         @checklist = Checklist.find(params[:id])
      end

      def checklist_params
           params.require(:checklist).permit(
               :item,
              :user_id
             )
          end
    end 
```

**jQuery** is a **Document Object Model (DOM)** manipulation library. The DOM is a tree-structure representation of all the elements of a Web page. jQuery simplifies the syntax for finding, selecting, and manipulating these DOM elements.


<a href="https://imgur.com/1Nk3qhc"><img src="https://i.imgur.com/1Nk3qhc.jpg" title="source: imgur.com" /></a>

When I started the javascript coding, I have to admit, I was bit frightened and felt limited with what I was comfortable with generating from my own brain.  However, Dalia, the wonderful javascript coach provided with me with these three videos for reference and tutorial help.  They pretty much saved my project. The videos are extremely helpful, easy to follow and are faithful to the labs we have done previously in the curriculum. 

* [https://www.youtube.com/watch?v=oHPM0ekV7zQ](http://) (javascript console help)
* 
* [https://www.youtube.com/watch?v=Yd0nH9CWWfo&amp=&feature=youtu.be](http://) (project tutorial one)
* 
* [https://learn.co/tracks/full-stack-web-development-v6/rails-and-javascript/building-apis/receiving-api-posts](http://) (project tutorial two)

I followed along on the tutorial videos and checked my work on the javascript console with the help of the first video. These videos were invaluable in helping me to complete my javascript along with reviewing the previous labs. Then I was able to work through each of the errors I had in the javascript console by clicking through, which highlighted each one. 

Here is my checklist.js :

```
$(document).ready(() => {
  alert("Loaded")
  indexChecklists()
  showChecklist()
})

// using fetch get request indexChecklists(), we get all checklists and send a get request as soon as the page loads.
//using JQuery, each checklist object is created for each node and rendered to the page.

function indexChecklists(){
  $('.all_checklists').on('click', function (event){
    event.preventDefault()
    history.pushState(null, null, 'checklists')
    //get back promise parsing the data on the response.
    fetch('/checklists.json')
      .then(res => res.json())
      .then(checklists => {
        $('#checklist_container').html('')

        checklists.forEach(checklist => {
          let newChecklist = new Checklist(checklist)
          let checklistHtml = newChecklist.formatIndex()
  //Inject the HTML to the body of the page using append
        $('#checklist_container').append(checklistHtml)
       })
    })
  })
}
//sends a GET request to the application

function showChecklist(){
  $(document).on('click','.show_checklists', function(event){
    event.preventDefault()
    let item = $(this).attr('data-item')

      fetch('/checklists/${item}.json')
       .then(resp => resp.json())
       .then(checklist => {
         $('#checklist_container').html('')
           let newChecklist = new Checklist(checklist)
           let checklistHtml = newChecklist.newChecklistForm()
           $('#checklist_container').append(checklistHtml)
        })
     })
  }

//New Form requirement:

//The newChecklistForm prototype template is rendered using this object’s attributes and injected into the page.

$(function() {
  $('form#new_checklist').on('submit',function(event) {
    event.preventDefault()

    const values = $(this).serialize()
    $.post('/checklists', values).done(function(data) {
      //console.log(data)
    $('#checklist_container').html(" ")

    const newChecklist = new Checklist(data)
    const htmltoAdd = newChecklist.newChecklistForm()
    $('#checklist_container').html(htmltoAdd)
    })
  })
})

//constructor - this is executing the checklist function

function Checklist(checklist) {
  this.item = checklist.item
  this.user_id = checklist.user_id
}

//Used the object on prototype to format Index Page through JSON

Checklist.prototype.formatIndex = function() {
  return (`
     <tr>
     <td><a href="/checklists/${this.item}" data-item="{this.item}"
        class="show_checklists"><h1>${this.item}</h1></a></td>
    </tr>
  `)

}

Checklist.prototype.newChecklistForm = function() {
   let checklistHtml = `
     <h2>Checklist Created</h2>
       <h3>${this.item}</h3><br>
       `
   return checklistHtml

}
```


<a href="https://imgur.com/G6efNpA"><img src="https://i.imgur.com/G6efNpA.png" title="source: imgur.com" /></a>

<a href="https://imgur.com/hLHd0Oi"><img src="https://i.imgur.com/hLHd0Oi.png" title="source: imgur.com" /></a>

<a href="https://imgur.com/8xrPeH7"><img src="https://i.imgur.com/8xrPeH7.png" title="source: imgur.com" /></a>


Well, it goes to show that we got this ......

<a href="https://imgur.com/CQhm6s3"><img src="https://i.imgur.com/CQhm6s3.jpg" title="source: imgur.com" /></a>


Git Repo 
[https://github.com/ChristinaXT/BabyGuide_JS](http://)



		
		



