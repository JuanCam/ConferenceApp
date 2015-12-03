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
date: The date the session will happen. (String)<br>
startTime: The time where the session start (String)<br>

You can Create Session in a conference only if you created that conference
These are the endpoints involving the Sessions:
createSession<br>
getConferenceSessions<br>
getConferenceSessionsByType<br>
getSessionsByStartTimeAndDuration<br>
filterConferenceSessionsByDuration<br>
getSessionsBySpeaker<br>
addSessionToWishlist<br>
removeSessionFromWishList<br>
getSessionsInWishlist<br>

<h2>The Query Problem</h2><br>
By creating this endpoint method filterByTypeAndTime I tried to filter first by Type, returning the types diferent from the type requested, and then filter that result by startTime, but I get this error:<b> Cannot have inequality filters on multiple properties</b>.
For a solution I think the filter could be done manually by performing the following steps: <br>
1)define an empty list<br>
sessions_filtered_list = []<br>
2)inside a for loop<br>

for session in qs:#qs is the filtered query<br>
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
