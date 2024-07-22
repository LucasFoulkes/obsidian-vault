what does it do, feautures, overview, user stories.
the app comes in 3 forms;
- Admin
- Waiter
- Kitchen
 
**ADMIN**
- [x] see all tables 
- [x] selects tables to each waiter
- [x] vibrates whenever new table pings a waiter
- [ ] see how long it takes for waiter to reach table
- [ ] send messages to waiter
- [ ] send messages to kitchen
- [ ] set schedule 
- [ ] set alarm 
- [ ] can set messages to be sent at certain time/date the message can be repeated
- [ ]  can set schedules
- [ ] can write notes, checkmarks
- [ ] can change menu
user stories . there is use and there is config and there is initial config
. initial config. there are no tables , pressing the table buttons makes them show up. i can white list them and give them an alias. 
.map config . only the whitelisted tables show up. i can move the tables. i can use labels i can draw rectangles i can give diferent colors to the rectangles and the labels i can move tables by selectim them as a group. i can create multiple pages.
the map has an editing an a non editing mode. is togled by long press in one corner. the tables can also be edited in map mode, their alias , changed added or removed from the waiters list. the first mode you should see is the map view ( not the map edit) and if it is empty it shows the table edit view. 
 
**KITCHEN**
- [x] can send messages to waiter
- [ ]  can send messages to admin
- [ ]  manages stock
- [ ]  sends daily stock
 
**WAITER**
- [x]  recieves alert from selected tables
- [x]  recieves messages from kitchen and admin

# LOG
12:22/13/3/2023
I will begin by creating a simulator for the table clickers. By this i mean a simulator of the beheaveor the pseudo router will have. This will help to better define the database schema, the apps in the tablet will be non centralized or wathever that is called (serverless?) becouse im cheap and im not charging enough.
Maybe I will think the overview of the program and then come to the best database schema. 

client call waiter -> router sends message+tablecode to database

	waiter recieves message table changed ( can this alert include the change made? if yes waiter app checks if table in list if in list alert else waiter asks db for new db to check changes) 

## ENTITIES
- Admin
	- mesages 
- Kitchen
	- messages
	- reports
- Tables
	- tables
		- tableId
		- alias
		- messages
		- lastMessage
		- whitelist
- Waiter
	- waiter
		- id
		- name
		- lastname
		- messages
		- average speed
		- tables
