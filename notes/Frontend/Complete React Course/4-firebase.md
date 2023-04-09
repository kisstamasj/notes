# Connect to firebase

## Initialize Firebase app

That code can be access from the webpage of firebase console.
First need to create Firebase web app.

```js
// src/utils/firebase/firebase.utils.js

// Import the functions you need from the SDKs you need
import { initializeApp } from 'firebase/app';
import {
    getAuth,
    signInWithRedirect,
    signInWithPopup,
    GoogleAuthProvider,
    createUserWithEmailAndPassword,
    signInWithEmailAndPassword,
    signOut,
    onAuthStateChanged
} from 'firebase/auth';
import { getFirestore, doc, getDoc, setDoc } from 'firebase/firestore';

// Your web app's Firebase configuration
const firebaseConfig = {
    apiKey: 'AIzaSyA0NztZiEEtOWaPWIyzwIgF6zgjPCE3j8M',
    authDomain: 'crwn-clothing-db-bf968.firebaseapp.com',
    projectId: 'crwn-clothing-db-bf968',
    storageBucket: 'crwn-clothing-db-bf968.appspot.com',
    messagingSenderId: '794932963620',
    appId: '1:794932963620:web:642cb01fe465b9e57aebb1',
};

// Initialize Firebase
initializeApp(firebaseConfig);

const googleProvider = new GoogleAuthProvider();

googleProvider.setCustomParameters({
    prompt: 'select_account',
});

export const auth = getAuth();
export const signInWithGooglePopUp = () => signInWithPopup(auth, googleProvider);
export const signinWithGoogleRedirect = () => signInWithRedirect(auth, googleProvider);

export const db = getFirestore();

/**
 * Create user with google auth
 *
 * @param {obj} userAuth
 * @param {obj} additionalInformation
 * @returns
 */
export const createUserDocumentFromAuth = async (userAuth, additionalInformation = {}) => {
    if (!userAuth) return;
    const userDocRef = doc(db, 'users', userAuth.uid);
    const userSnapshot = await getDoc(userDocRef);

    if (!userSnapshot.exists()) {
        const { displayName, email } = userAuth;
        const createdAt = new Date();

        try {
            await setDoc(userDocRef, {
                displayName,
                email,
                createdAt,
              ...additionalInformation,
          });
      } catch (error) {
            console.log('error createing the user', error.message);
        }
    }

    return userDocRef;
};

/**
 * Create user with email and password
 *
 * @param {string} email
 * @param {string} password
 * @returns
 */
export const createAuthUserWithEmailAndPassword = async (email, password) => {
    if (!email || !password) return;
    return await createUserWithEmailAndPassword(auth, email, password);
};

/**
 * Sign in user with email and password
 *
 * @param {string} email
 * @param {string} password
 * @returns
 */
export const signInAuthUserWithEmailAndPassWord = async (email, password) => {
    if (!email || !password) return;

    return await signInWithEmailAndPassword(auth, email, password);
};

export const signOutUser = async () => await signOut(auth);

export const onAuthStateChangedListener = (callback) => onAuthStateChanged(auth, callback)
```

- ```firebaseConfig```: the firebase config
- ```firebaseApp```: initialized firebase app
- ```googleProvider```: google auth provider (there are mulitple, ex.: facebook, githube etc...)
- ```auth```: keeping track the user is authenticated or not
- ```signInWithGooglePopUp```: Sign in with google popup window
- ```signinWithGoogleRedirect```: Sign in user with a redirected page to google
- ```db```: Firebase store
- ```createUserDocumentFromAuth```: Craete user with google account
- ```createAuthUserWithEmailAndPassword```: Create user with email and password
- ```signInAuthUserWithEmailAndPassWord```: Sign in user with email and password
- ```signOutUser```: Sign Out the user
- ```onAuthStateChangedListener```: Auth state change listener

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

## Sign in with redirect 

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

## Create collection and document
```js
export const addCollectionAndDocuments = async (collectionKey, objectsToAdd) => {
    const collectionRef = collection(db, collectionKey);
    const batch = writeBatch(db);
    objectsToAdd.forEach((object) => {
        const docRef = doc(collectionRef, object.title.toLowerCase())
        batch.set(docRef, object)
    })

    await batch.commit();
    console.log('done')
}
```

## Get collections and documents
```js
export const getCatagoriesAndDocuments = async () => {
    const collectionRef = collection(db, 'categories');

    const q = query(collectionRef);

    const querySnapshot = await getDoc(q);
    const categoryMap = querySnapshot.docs.reduec((acc, docSnapshot) => {
        const {title, items} = docSnapshot.data();
        acc[title.toLowerCase()] = items;
        return acc;
    }, {})

    return categoryMap;
}
```


