## Connect to firebase

### Initialize Firebase app

That code can be access from the webpage of firebase console.

Step:
- Create firebase web app
- then copy the code below

```js
// src/utils/firebase/firebase.utils.js

// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
import { getAuth, signInWithRedirect, signInWithPopup, GoogleAuthProvider } from 'firebase/auth'

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
const firebaseApp = initializeApp(firebaseConfig);

const provider = new GoogleAuthProvider()

provider.setCustomParameters({
    prompt: "select_account"
})

export const auth = getAuth();
export const signInWithGooglePopUp = () => signInWithPopup(auth, provider);
```
