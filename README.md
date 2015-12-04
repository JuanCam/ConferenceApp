<h1> Conference Central - Version 1.0 02/12/2015</h1>

GENERAL USAGE NOTES
-------------------

-First of all, for using this webiste follow this steps:<br>
*Download or clone the source code.<br>
*Go to console.developers.google.com<br>
*Create a new project.<br>
*Run App Engine.<br>
*Deploy the project.<br>
*Introduce the url <your-project-id>.appspot.com<br>
-The Conference Central is an application that allows registered gmail accounts to create, view and register to conferences.<br>
-Create sessions for the conferences.<br>
-Add sessions to whislist.<br>
-You can filter the sessions by time and duration.<br>
-You can also filter the sessions by duration, searching by all the sessions with inferior or greater than the desired duration or also equal duration.<br>

The Session kind where implemented as descendent from the Conference kind
all the Session entities will require the parent key (Conference Key)
the Session fields are the following:
name: Corresponds to the Session name (String)<br>
highlights: The Higlights session(String)<br>
speaker: The name of the Session Speaker(String)<br>
duration: The duration of the session(Integer)<br>
sessionType: The session type (workshop, lecture, etc) (String)<br>
date: The date the session will happen. (DateProperty)<br>
startTime: The time where the session start (Float)<br>

The name session is a string field because this field could contain many kind of characters, also the highlights and the session type. The speaker name was assigned
a string because when you want to filter the sessions by speaker is more comfortable for the user to do it with the name rather than a key.
the most remarkable type I want to explain is the startTime y choose it float because I can convert with a simple algorithm in the backend code the string with this
format "HH:MM" so I will always handle this format by converting it to its double number equivalent, I.e. 3:30 = 3,5 also 14:45 = 14,75. 

You can Create Session in a conference only if you created that conference
These are the endpoints involving the Sessions:
createSession<br>
getConferenceSessions<br>
getConferenceSessionsByType<br>
getSessionsByStartTimeAndDuration New query!<br>
filterConferenceSessionsByDuration New query!<br>
getSessionsBySpeaker<br>
addSessionToWishlist<br>
removeSessionFromWishList<br>
getSessionsInWishlist<br>
<h2>New queries explanation</h2><br>
getSessionsByStartTimeAndDuration: input - time(string) and duration(integer), output - list of sessions. It looks for all session that corresponds to the Time and Duration inserted by the user
it should return a list of conferences which properties match the input criteria.<br>
filterConferenceSessionsByDuration: input - duration(integer), operator(string limited to: equal, less or great)and websafeConferenceKey(string), output - list of sessions. Once the query over the conference child sessions is performed 
then a filter is applied to the result taking into account the operator and the duration value, I.e duration = 40 and operator = 'less' the filter will show only sessions
that lasts less than 40 minutes. The output should be a list of the conference sessions that match the input criteria.<br>
<h2>The Query Problem</h2><br>
By creating this endpoint method filterByTypeAndTime I tried to filter first by Type, returning the types different from the type requested, and then filter that result by startTime, but I get this error:<b> Cannot have inequality filters on multiple properties</b>.
For a solution I think the filter could be done manually by performing the following steps: <br>
1)define an empty list<br>
sessions_filtered_list = []<br>
2)inside a for loop<br>

for session in qs:# qs is the filtered query<br>
3)using an if clause(inside the for loop) remove all the startTime that doesn't match the operator in the request<br>
if data['operator']=='<':<br>
  if session.starTime < data['startTime']:<br>
   sessions_filtered_list.append(session)<br>
elif data['operator']=='>':<br>
  if session.starTime > data['startTime']:<br>
   sessions_filtered_list.append(session)<br>
elif data['operator']=='==':<br>
  if session.starTime == data['startTime']:<br>
   sessions_filtered_list.append(session)<br>
 this should perform the time filter.<br>
4) return the sessions_filtered_list<br>

PULLING REQUEST
------------------
You can clone the project with this url https://github.com/JuanCam/ConferenceApp
feel free to improve the project and push your changes

CONTACT INFO
------------------
Author : Juan Camilo Gutierrez Ruiz<br>
Voice : 6262751<br>
Website : www.juan-latino.com<br>
e-mail : juacgr_4@hotmail.com<br>

Copyright 2015 Juan Corporation All rights reserved.
ConferenceApp application and its use are subject to license agreement and are also subject to copyright trademark/pattent and/or other laws. 
