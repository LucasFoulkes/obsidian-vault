pwa, server (local serveer to avoid internet), voice control.
1. server client update (admin info for now shoudl store it in the indexdb thing. i should somehow know this) 
	1. tries to connect if connect good else offline mode , show available users for device.
		1. server python or node and mongodb database or other type of database
		2. client once program open it tries to connect once, 
			1. how to once a pwa program is open it test for connection for a bit until prompted again to try again. 
			2. server it should return the list of passwords and users user id. maybe the user keeps a token?.  if offline well the clients should have something to check. so ti should send the password to the client somehow . hash?
			3. i will use node for the server, mongodb
2. seems pwa react to landscape and like when i move the phone this is terrible. 
	1. seems for iphone cant prevent landscape rotation
	2. in android deos seem posible maybe t
	3. can pwa in some androids probably the cheapest ones wich are important for rural solutions. 