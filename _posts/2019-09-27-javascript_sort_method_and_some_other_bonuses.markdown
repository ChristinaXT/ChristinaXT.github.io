---
layout: post
title:      "javascript sort method and some other bonuses"
date:       2019-09-27 17:43:12 -0400
permalink:  javascript_sort_method_and_some_other_bonuses
---



In the first line of my javascript after the document ready function, I have 

```
function indexChecklists(){
  $('#all_checklists').on('click', function(event) {
```

Here, we are using JQuery. This is querying for the HTML elements on the DOM` ('#all_checklists')` 



My live coding challenge for my Javascript project was a sort method. I had never built one before, so it was fun and challenging to learn and I thought I would share it here. 

The purpose of the **Sort Method** is to sort the elements in your array and then return another array that is sorted in the way you specified. For example, I was asked to sort my checklist items alphabetically. 
 
 On the MDN website[ https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort](http://) is great for reference on everything Javascript !
 
*** One of the most important things to remember when you are adding new methods to your Javascript is to call the function for your event listener at the top of the page under your `$(document).ready` line. I added this:` sortChecklists()` because it is what I named the function. Whatever code we add inside our `$(document).ready()` method will then be able to run once the DOM is ready to execute the code. 

The next step is to create an HTML button in order to connect the backend to the javascript. I placed the code `<button class="sort_button">Sort Alphabetically</button>` in the views, checklists, index.html folder. By calling the `class="sort_button"`, we are connecting this button to the javascript. 
Next, I checked to make sure my button was working and returning an array in the javascript console by doing a console.log('click'). 
 
Look at the next line (the event listener) `$('.sort_button').on('click', function(event) {` . This literally means that on the click of the sort button a query is sent to our javascript looking for what happens next in the code.  Notice in this line there is a dot in front of the words `.sort_button`. 
** When do we use "." dot verses "#" in event listeners?** The dot "." shows a class selector, while the "#" hashtag shows the ID selector. This comes back around to the name of the class we called on in the html button code we added on the checklists index file. If we were searching for something by its ID, then we would have used the # hashtag, but we were connecting with the class name and therefore, a dot is necessary. 
 
 Fetch() makes a request to whichever url (network http or from your own root directory) request is made and returns a promise. The returned promise is given with a response object and in order to read the response body, we have to call on it with a response method `json()` and then another promise is returned with the value of the response body. `.then(checklists => {`

 The `fetch('/checklists.json')  `  is fetching the json data from the checklists index. We want to make sure the .json is at the end of our fetch request to ensure our returning data is json data. This particular fetch(url) is requesting data from the checklists as json data. 
 
 The next lines :
```
.then(resp => {
        resp.json()
      .then(checklists => {

```
 
When we have a successful fetch, the `.then(resp` lines above will parse the data using json. The next line .`then(checklists =>` shows that the object values have been read and they will be inserted into a list. 

This line `$('#checklist_container').html('')`clears out the previous checklist display so that we have a clean slate for a new display of our sorted data. 

This is our sort function :  

```
checklists.sort(function(a, b) {
      var itemA = a.item.toUpperCase(); // ignore upper and lowercase
      var itemB = b.item.toUpperCase(); // ignore upper and lowercase
      if (itemA < itemB) {
      return -1;
      }
      if (itemA > itemB) {
      return 1;
      }
  // items must be equal
       return 0;
       });
```

`the checklists.sort(function(a,b){ ` is saying we are going to compare the elements in this function to be able to sort them. 

The following lines are providing more importance to the items by making them uppercase.  The first if statement is saying that if the first item has a value less than the second item, then reduce down by one. The next if statement is saying the opposite, you go up by one. and if neither applies, then nothing is returned. 

The last part of the function `sortChecklists` is added to display the sorted data. First you need the iteration `checklists.forEach(checklist => { `  for each of the checklists objects that match the values we are saying, they will individually be listed in the `formatChecklist` .  The let statements that follow: the first one is saying that we will let the newChecklist equal to the new Checklist class with checklist objects. The second statement says that the new checklists will be displayed in our new format. The last line `$('#checklist_container').append(checklistHtml)` says we will inject the HTML into the body of the page using append and this will allow us to see the full, newly sorted array of checklists in alphabetical order.    

There are several ways to do the sort method, but since I am sorting objects, then this is the method I used:

```
function sortChecklists() {
   $('.sort_button').on('click', function(event) {
   // console.log('click')
    event.preventDefault()
    fetch(`/checklists.json`)
    .then(resp => resp.json())
    .then(checklists => {
       $('#checklist_container').html('')
      // console.log(checklists)
    checklists.sort(function(a, b) {
      var itemA = a.item.toUpperCase(); // ignore upper and lowercase
      var itemB = b.item.toUpperCase(); // ignore upper and lowercase
      if (itemA < itemB) {
      return -1;
      }
      if (itemA > itemB) {
      return 1;
      }
  // items must be equal
       return 0;
       });
       console.log(checklists)
 //Added this part to display the sorted data -
          // iteration
          //     for each(variable in object) object for which properties are iterated
       checklists.forEach(checklist => {
         //statement
        let newChecklist = new Checklist(checklist)
        let checklistHtml = newChecklist.formatChecklist()
        //Inject the HTML to the body of the page using append
        $('#checklist_container').append(checklistHtml)
       })
     })
   })

 }
```


**When are good opportunities to use `console.log()` and `debugger` when coding in JS? How are they different?**

**console.log method** -- will allow you to check your work to make sure the code is defined. The console log sends a message to the console and tests the purpose of what you are asking about.

**The debugger method** stops the code execution of the Javascript where you place debugger; in your code. It acts the same as the breakpoint method in the javascript console. 

You can see my entire project on Github [https://github.com/ChristinaXT/BabyGuide_JS](http://)

