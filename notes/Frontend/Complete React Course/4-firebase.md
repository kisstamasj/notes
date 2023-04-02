## Connect to firebase

### Initialize Firebase app

That code can be access from the webpage of firebase console.

Step:
- Create firebase web app
- then copy the code below

```js
// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: "AIzaSyA0NztZiEEtOWaPWIyzwIgF6zgjPCE3j8M",
  authDomain: "crwn-clothing-db-bf968.firebaseapp.com",
  projectId: "crwn-clothing-db-bf968",
  storageBucket: "crwn-clothing-db-bf968.appspot.com",
  messagingSenderId: "794932963620",
  appId: "1:794932963620:web:642cb01fe465b9e57aebb1"
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
```
