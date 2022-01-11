Truman Platform CSE 392 Independent Study Fall 2021 
=======================

The changes made in this repository include implementation for hashtags, username links ("@username"), and username profile popups.

Hashtags - Ryan Schmid
------
Summary: The process of populating now includes turning hashtags in posts and comments into links that show all posts with the hashtag when clicked. The files edited were app.js, main.js, populate.js, script.js, and Script.js.

The goal of this part is to add links to existing hashtags as they are populated. Most of the code is in the populate.js file where posts are populated. The code first tokenizes the post body. To make this possible, a "text" index was added to the body of the Script Schema in Script.js. The code then iterates through the string tokens and checks if any begin with a hashtag. 

It then ensures that the hashtag includes only valid characters A-Z, a-z, and 0-9. The reasoning for this is that it is how hashtags are formatted on sites like Twitter, and otherwise, URL encoding would be required for special characters. The algorithm checks each character individually and adds them to the valid “tag” variable until it reaches the end of the word or a non-alphanumeric character. This is to ensure that symbol characters can be included immediately following the hashtag without a space in between. One example of this occurrence is in a post that starts with “#breadoftheday:”. 

Finally, assuming the tag is not empty, the code replaces the text tag with a linked version of the same thing. The link contains a path “/search?search=…” as a query to show all posts with the queried hashtag. 

The associated route is implemented in app.js as the “app.get(‘search’…” route and calls the function “getScriptFeedSearch” in script.js, which is identical to “getScriptFeed” expect that it returns only the posts with the given hashtag. 

The code is applied to comments as well, so all hashtags written in comments will be turning into links the exact same way. 

In addition, a small amount of code was added to main.js for turning the post and comment text into html so that the “a” tags would correctly show up as hyperlinks. 


Username links - Lucas
------
Summary: The purpose of this part is to extract the username after @ sign and then substitute it to the link which is composed of profile, picture, and name. After that, when the users click the content like "@Lucas," they will be redirected to Lucas' profile. The file edited was populate.js.

Firstly, The string variable called theString stores the body of posters to and then split the content by each space. For example, if "See @Lucas" is the content, this string will be divided into "See" and "@Lucas."

After that, each substring  will be checked for whether it contains ‘@’ in it through For loop. If it does have @ in it, the content after ‘@’ sign will be extracted and stored in userName. 

Next, the code is to use the extracted username to check the user list to confirm. If the user exists, the user’s detailed information will be combined and eventually become an urllink to substitute the username in the post body. For instance, "@Lucas" will be substituted by the link that can show Lucas's profile. If the username does not exist in the user list, the code will do nothing and come to the next for loop cycle.  

Finally, when the users click the information in the comment area like “@Lucas,” they can see the user’s detailed information.


Profile popups - Coco
------
Summary: The goal of this part is to have a popup window when people @ other user in the comment block. The popup window only shows up until a user @ other people; the popup window will be hidden at other times. It will display the main information of the user being @. 
```
  userName
  userProfilePic
  userBio
  userUrl
```
To achieve this goal, this part is built based on Lucas' part. After it detects an @ sign, it will fetch the username. Based on the username, the rest of infor will be retrieved easily. To display the main information, the code is added in feed.pug. 
To figure out the whole structure of Truman's platform, a lot of time is spent on exploring the functionalities of semantics ui and pug. 
As the test.pug creates a testing page for Truman, the test code is implemented inside test.pug. 
```
Example:
.hide(style = "position:absolute; left:10px; top:-120px; height: 10px; width:100px;border: 3px ")
            b Noah
            p#bio  Hi, I am noah! 
            a.pro_name_link(href='/user/NoahM1121') 
            img(style='width:100px; height:70px' src='imgsrc')
```


December 2021 - January 2022 
=======================

Changes made during this time period were made by Jeremy Feng.

Hashtags in User Posts and Comments
------
File edited: ./controllers/script.js

Summary: This implementation uses Ryan Schmid's hashtag implementation. When a user creates a post or comment, the string of the post or comment is split by spaces, and each part of the string is stored into an array. Then, the array is iterated through to check if any words in the post begin with a "#". If so, change that index into a link by embedding it with the "app.get('/search'…" route. Finally, after iterating through the array, combine all the elements back into one string and return it as a post or comment.

Username Tags in User Posts and Comments
------
File edited: ./controllers/script.js

Summary: This implementation is similar to Ryan Schmid's hashtag implementation. The difference is that instead of checking for the "#" symbol, the "@" symbol is checked for. Another difference is that instead of using the "/search" route, the "/user" route is user.