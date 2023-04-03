## Connect to firebase

### Initialize Firebase app

That code can be access from the webpage of firebase console.
First need to create Firebase web app.

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

const googleProvider = new GoogleAuthProvider()

googleProvider.setCustomParameters({
    prompt: "select_account"
})

export const auth = getAuth();
```

- ```firebaseConfig```: the firebase config
- ```firebaseApp```: initialized firebase app
- ```googleProvider```: google auth provider (there are mulitple, ex.: facebook, githube etc...)
- ```auth```: keeping track the user is authenticated or not

### Sign in with Popup window
```js
// src/utils/firebase/firebase.utils.js

export const signInWithGooglePopUp = () => signInWithPopup(auth, googleProvider);
```

```jsx
// src/routes/signin/signin.component.jsx

import { signInWithGooglePopUp, createUserDocumentFromAuth } from '../../utils/firebase/firebase.utils'

const SignIn = () => {

    const logGoogleUser = async () => {
        const { user } = await signInWithGooglePopUp();
        const userDocRef = await createUserDocumentFromAuth(user);
    }

    return (
        <div>
            <h1>Sign IN</h1>
            <button onClick={logGoogleUser}>Sign in with Google PopUp</button>
        </div>

    )
}

export default SignIn
```

### Sign in with redirect 

```js
// src/utils/firebase/firebase.utils.js

export const signinWithGoogleRedirect = () => signInWithRedirect(auth, googleProvider)
```

```jsx
// src/routes/signin/signin.component.jsx

import { useEffect } from 'react';
import { getRedirectResult } from 'firebase/auth';

import { auth, createUserDocumentFromAuth, signinWithGoogleRedirect } from '../../utils/firebase/firebase.utils'

const SignIn = () => {

    useEffect(() => {
        getRedirectResult(auth).then(async (response) => {
            if (response) {
                const userDocRef = await createUserDocumentFromAuth(response.user)
                console.log(userDocRef)
            }
        })
    }, [])

    return (
        <div>
            <h1>Sign IN</h1>
            <button onClick={signinWithGoogleRedirect}>Sign in with Google PopUp</button>
        </div>

    )
}

export default SignIn
```

### Create user document
```js
// src/utils/firebase/firebase.utils.js

export const db = getFirestore();

export const createUserDocumentFromAuth = async (userAuth) => {
    const userDocRef = doc(db, 'users', userAuth.uid)

    console.log(userDocRef)

    const userSnapshot = await getDoc(userDocRef);
    console.log(userSnapshot.exists())

    if (!userSnapshot.exists()) {
        const { displayName, email } = userAuth;
        const createdAt = new Date()

        try {
            await setDoc(userDocRef, {
                displayName,
                email,
                createdAt
            })
        } catch (error) {
            console.log('error createing the user', error.message)
        }
    }

    return userDocRef;
}
```



