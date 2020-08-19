# Firebase Project Using Firestore, Authentication and Functions

> A simple game guide list displayed only to logged in users using Google Firebase

A small project that displays the use of Firebase Authentication in action. The application explores auth claims, admin roles, and user data storage using the Firebase Firestore. The project consists of a list of game guides that can be displayed only once the user has logged in. The user with an admin role can create new guides as well as set other users as admins.


## Table of Contents


> Try `clicking` on each of the `anchor links` below so you can get redirected to the appropriate section.


- [Google Firebase](#google-firebase)
- [Create New Guide](#create-new-guide)
- [Setup Guides](#setup-guides)
- [Real-time Listeners](#real-time-listeners)
- [Contact Details](#contact-details)
- [Inspiration](#inspiration)


## Google Firebase


<br/>
<img src="https://www.gstatic.com/devrel-devsite/prod/v1241c04ebcb2127897d6c18221acbd64e7ed5c46e5217fd83dd808e592c47bf6/firebase/images/lockup.png" title="Google Firebase" alt="Google Firebase">

Firebase is a mobile-backend-as-a-service that provides powerful features for building mobile apps. Firebase has three core services: a realtime database, user authentication and hosting. With the Firebase iOS SDK, you can use these services to create apps without writing any server code.

- :link: [Google Firebase](https://firebase.google.com/)


## Create New Guide


```javascript
const createForm = document.querySelector('#create-form');

createForm.addEventListener('submit', (e) => {
	e.preventDefault();

	db.collection('guides').add({
		title: createForm['title'].value,
		content: createForm['content'].value
	}).then(() => {
		// Close the modal and reset the form
		const modal = document.querySelector('#modal-create');
		M.Modal.getInstance(modal).close();
		createForm.reset();
	}).catch(err => {
		console.log(err.message);
	});
});
```


## Setup Guides


```javascript
const setupGuides = (data) => {

	if(data.length) {
		let html = '';
		data.forEach(doc => {
			const guide = doc.data();
			const li = `
			<li>
				<div class="collapsible-header grey lighten-4">${guide.title}</div>
		        <div class="collapsible-body white"><span>${guide.content}</span></div>
	        </li>`;
	        html += li;
		});
		guideList.innerHTML = html;
	} else {
		guideList.innerHTML = '<h5 class="center-align">Login to view guides</h5>';
	}
	
};
```


## Real-time Listeners


> Refresh guides list with onSnapshot()


```javascript
auth.onAuthStateChanged(user => {
	if(user) {
		// check if user is an admin
		user.getIdTokenResult().then(idTokenResult => {
			//console.log(idTokenResult.claims);
			user.admin = idTokenResult.claims.admin;
			setupUI(user);
		});
		// get data
		db.collection('guides').onSnapshot(snapshot => {
			setupGuides(snapshot.docs);
		}, err => console.log(err.message));
	} else {
		setupUI();
		setupGuides([]);
	}
});
```


## Contact Details


> :computer: [https://pagapiou.com](https://pagapiou.com)

> :email: [hello@pagapiou.com](mailto:hello@pagapiou.com)

> :iphone: [LinkedIn](https://www.linkedin.com/in/agapiou/)

> :iphone: [Instagram](https://www.instagram.com/panos_agapiou/)

> :iphone: [Facebook](https://www.facebook.com/panagiotis.agapiou)


## Inspiration


- **[The Net Ninja](https://www.youtube.com/channel/UCW5YeuERMmlnqo4oq8vwUpg)**
