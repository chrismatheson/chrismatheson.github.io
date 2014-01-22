When designing an angular Single Page App in [angular](http://angularjs.org) one of the first things you will find is that angular is a runtime off its own. It has an internal event loop and its own configuration and run-time states [docs link](http://docs.angularjs.org/guide/module).

Im not going to comment on this, but one thing it definatley restricts / enforces, is that afer booting the angular framework, you can add modules.

For smaller apps this isnt too much of a problem, however for iVendi we wanted to be able to pull in modules which would define new routes, service, componenets etc only for the particular user setttings.

- admin moudle with route's for user mangament
- user specific enhancements SSO, custom UI etc

Our first approach was to seperate the login page into its own seperate html page and then use server side rendering to build the app to spec. For our usecase however the server side provides only an API interface and we wanted to keep it that way.

So this is what i came up with. **Angular Dual Boot**

the basic concept is simple, create two angular apps, the first will sign in the user and then based on that users information can request new modules and load then into angular in the usual way. After these modules have all been loaded it kicks off the seccond angular application which takes over and runs the main application.

lets walk through the process