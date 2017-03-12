![ga](https://cloud.githubusercontent.com/assets/20629455/23824362/2c9817c2-066d-11e7-8988-7b1eefc6d628.jpg)
![wdi](https://cloud.githubusercontent.com/assets/20629455/23824363/2ddeaa7e-066d-11e7-8630-f7c890c9f1c1.png)

___
<br>

#Project 4 | MeetMe

##Overview
For my final project, I wanted to create an app that I would find useful in my actual life and that demonstrated a lot of what I had learned at General Assembly over my twelve weeks.

The idea for MeetMe came about when thinking about what me and my friends often struggle with - finding the time and the place to see each other amongst our very busy lives. It was built using a Ruby on Rails back-end and AngularJS front-end.

See the app here. (ADD LINK)

##The Idea
The premise of MeetMe is for one person (the organiser) to send invitations out to one (the invitee) or more of her friends suggesting a time to meet. The invitee receives the invitation when she logs into the app, and can decide to register as attending or not attending the get-together. When she clicks attending, the app stores the geographic location of where she is at that moment using the GoogleMaps API, and does this for every invitee.

Once the organiser is satsified that enough of her aquantainces are attending, she can close the event to future invites by clicking XXXXX. This launches a function in the background that calculates the average latitute and longitude of all attendees and inputs it into the Zomato API. The API returns a list of restaruants in the area, and the app automatically selects the highest ranked restaurant to attach to the event, and displays it to the organiser and all the attendess. Easy peasy.

##The Build
* Back-end: Ruby on Rails
* Front-end: AngularJS
* CSS framework: Skeleton
* Database: PostgreSQL
* Angular modules:
	* Simple HTTP requests: ngResource
	* Authentication: angular-jwt
	* Map display: ngMap
* Ruby gems:
	* HTTP requests: httparty
* External APIs:
	* GoogleMaps
	* Zomato

##The Process
I began the build for this app by pseudo-coding what exactly I wanted this app to do, which was to create events, create invitations, offer the option to attend or to not attend, and calculate the ideal location based on attendees' responses. This was my MVP. The decision to allow the app to decide the actual location using the Zomato API came later.

From here, I went to work on my models. I first needed to figure out how many models I would require, how they were structured and how they would interact. After much consideration and pencil drawing, I decided that one user could create many events, that any event could have many invitations and that any user could be either an event organiser, or owner as called in the model, or an invitee. I also decided that I had to store location information not against the user model but against the invitation model, as I didn't want the user to be tied to one singular location. Upon further review, I decided that invitations and events needed to both have a status field to allow the app to store the location information against the invitation and the event on click event.

While it seems pretty straightforward now, this process involved a lot of trial and error to get to a point where the models functioned together correctly, and was easily the most difficult portion of this project.

Once the back-end API was storing basic data for authentication, user, events and invitations, I focused on my front-end AngularJS build. I began by completing the authentication process with the front-end portion using AngularJS and angular-jwt. 

I then set about drafting the routes my app would require. I wanted the app to be very straight-forward to use, where the user could see the majority of their relevant information, such as events they've created or are attending and pending invitations, in one main view. Each individual event would also have one view where the user could see the date and time, the invited and attending guests, and, when completed, the destination. While I think this is great UX, it also saved me a lot of time and effort in creating more views than I thought necessary.

###Main view
The first thing the user sees when she logs in is her personlised homepage, which lists the events she's created and the invitations she's received, as long as they're pending or accepted. From this page, she can click to create a new event, and accept or reject any pending invitations. When she accepts the invitation, the app locks in the longitute and latitude of the user at the time of selection and stores it in the invitation model.

###New event view
Here, the user can create a new event. Once submitted, this page takes the user to the specific event page.

###Event view
Here, the user sees the event name and the date and time. This is also where the user can select who to invite to her event. I've implemented a search feature allowing the user to search other users' through their email addresses. This is done through a filter method in AngularJS. This page then lists everyone who is invited, who's invitation is pending or accepted. 

This page also allows the event's organiser to 'Lock In' the event. This then initiates the app to calculate the average location of everyone who has hit attending on an event. This information is then stored in the event model, which is then passed on to the Zomato API in the back-end to find the right spot for the event.

###Other views
Other views include event and profile edit views.

Once I had all this completed, I decided to add the Zomato API to actually select the restaurant for the event, and to add it to the event. 


##Key Challenges / Learnings
As this was my final project, there were a lot of challenges and — ultimately — learnings I gleamed for my effort.

Including:

- Figuring out the SQL model functionality was easily the most difficult part of this project. It took a lot of trial and error to find the right solution. Similar to the value of pseudo-code, it really cemented for me the need to create a detailed plan for what you want your app to accomplish.

- Storing and calculating the average location for each event. To calculate the average location, the app averages all attendee's latitudes and longitudes and passes that information into the model. While I understand that my method is not the most sophisticated, I think it does get the job done. Figuring out to use an array to list all the invitations and then taking the lat and lng of each one was highly satisfying.

- Writing the email search function. While it it's just a few lines of code, I struggled to figure out how to get this function to... function. In the end, I'm glad I persevered as it adds a nice professional touch.

- Using the GoogleMaps and Zomato APIs, along with ngMaps. It was a fun puzzle to figure out how to run the 3 apps (2 external, 1 interal) together and to include the ngMaps directive. 

- Creating a different view for the event organiser and the event attendee. After a lot of fingaggling with ng-ifs, ng-shows, and ng-hides, I finally got the app to display the relevant functions to the two users.

- Designing the look of the app and making sure the information is displayed properly.

##Future work
- In the future, I would like to have the app send email invitations to users. I started working on this functionality, but sadly ran out of time before it was fully functioning.

- I'd also like to be able to invite users who are not registered, and encourage them to register.

- It would be great to improve the algorithm for calculating the ideal location, perhaps including tube journey times.

- I would also like to allow the invited guests to input the location they'll be arriving from, instead of storing it automatically.

