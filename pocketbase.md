# Pocketbase
single file executable. creates a server? gives acces to a admin screen for the server. 
this is authn 
```javascript
import PocketBase from 'pocketbase';

const pb = new PocketBase('https://pocketbase.io');

const authData = await pb.collection('users').authWithPassword('YOUR_USERNAME_OR_EMAIL', '1234567890');

// after the above you can also access the auth data from the authStore

console.log(pb.authStore.isValid);

console.log(pb.authStore.token);

console.log(pb.authStore.model.id);

// "logout" the last authenticated model

pb.authStore.clear();
```