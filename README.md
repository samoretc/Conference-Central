App Engine application for the Udacity training course.

## Products
- [App Engine][1]

## Language
- [Python][2]

## APIs
- [Google Cloud Endpoints][3]

## Setup Instructions
1. Update the value of `application` in `app.yaml` to the app ID you
   have registered in the App Engine admin console and would like to use to host
   your instance of this sample.
1. Update the values at the top of `settings.py` to
   reflect the respective client IDs you have registered in the
   [Developer Console][4].
1. Update the value of CLIENT_ID in `static/js/app.js` to the Web client ID
1. (Optional) Mark the configuration files as unchanged as follows:
   `$ git update-index --assume-unchanged app.yaml settings.py static/js/app.js`
1. Run the app with the devserver using `dev_appserver.py DIR`, and ensure it's running by visiting your local server's address (by default [localhost:8080][5].)
1. (Optional) Generate your client library(ies) with [the endpoints tool][6].
1. Deploy your application.


[1]: https://developers.google.com/appengine
[2]: http://python.org
[3]: https://developers.google.com/appengine/docs/python/endpoints/
[4]: https://console.developers.google.com/
[5]: https://localhost:8080/
[6]: https://developers.google.com/appengine/docs/python/endpoints/endpoints_tool

Questions concering the project submission

Task 1: 
To model Session, a Session kind was created. The Session kind has the following properties:
-  name as a required StringProperty.
-  highlights as a StringPropety. 
-  duration as a IntegerProperty
-  typeOfSession as a StringProperty.
-  startTime as a TimeProperty. 
-  conferenceName as a StringProperty.

To get data from the client, the SessionForm class was created. All of the above data is sent in with the SessionForm class, as well as the websafeurl key for the particular conference that the session is a part of. The conference is used as a parent for the particular session, so that queries are faster and easier. 

Task 3: 

Question: How would you handle a query for all non-workshop sessions before 7 pm? What is the problem for implementing this query?

Answer: The problem with this query is that it would apply two inequality filters, and app engine does not allow more than one inequality filter for a query. To implement this query, I would first apply the one of the inequalities filter. I would then iterate over the objects and determine individually if the other inequality filter was satisfied. I decided to implement this function. It's called getSessionsBeforeTimeNotOfType.

Question: Implement two additional queries and describe why that are useful. 

First Query: As a conference attendee, I might want to see a particular speaker very badly. However, my time is limited, and I would only like to see her presentation if its shorter than a certain length. Because of this, I decided to implement an endpoint that returns all sessions by a particular speaker that are shorter than a certain length. 

Second Query: Let's say I'm not interested in a particular conference, but rather certain speaker. I want to see this speaker, but I can only see them in my hometown. For example, I know that Sebastian Thrun is going to have a few sesssions in San Francisco at few different conferences. I live in San Francisco, and I would like to compare these sessions. Because of this, I decided to implement a query that returns all sessions by a particular speaker in a particular city. 


