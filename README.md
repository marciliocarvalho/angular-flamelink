# AngularFlamelink

An angular wrapper service for Flamelink SDK.
(Currently tested with Could Firestore only.)

## Dependencies

#### Firebase:
Run `npm i -s firebase`. 

#### AngularFire:
Run `npm i -s @angular/fire`. 

#### Flamelink:
Run `npm i -s flamelink@next`. 


## Installation

Run `npm i -s angular-flamelink`. 

Then, import Flamelink and AngularFire in your app.module.ts:

```
@NgModule({
	imports: [
		AngularFireModule.initializeApp({
			apiKey: 'YOUR_API_KEY_FROM_FIREBASE',
			authDomain: '...',
			databaseURL: '...',
			projectId: '...',
			storageBucket: '...',
			messagingSenderId: '...'
		}),
		AngularFirestoreModule,
		AngularFlamelinkModule,
		
		// Import other services you're using...
		// AngularFireAuthModule,
		// AngularFireStorageModule,
		// ...
	]
})

```

## Usage

**page.component.ts**
```
@Component({
	// ...
})
export class PageComponent {

	public projects = this.flamelink.valueChanges({
		schemaKey: 'Projects',
		filters: [['category', '==', 'web']]
		// ... other settings
	});

	constructor(
		private flamelink: AngularFlamelink
	) { }

}
```

**page.component.html**
```
<div *ngFor="let project of projects | async">
	{{ project.title }}
</div>
```

## Api

Angular Flamelink extends the same api used in Flamelink SDK:

### Properties:

##### Extended Properties and Methods

**AngularFlamelink.auth**: returns AngularFire authentication service https://firebase.google.com/docs/reference/js/firebase.auth.Auth.

**AngularFlamelink.ref(id: string)**: return a Firestore DocumentReference. 

**AngularFlamelink.valueChanges(options: GetOptions)**: Takes the same options used in flamelink.content.subscribe(options) but returns an observable of an Array of the results.

##### From native Flamelink SDK:

**AngularFlamelink.content**: https://flamelink.github.io/flamelink-js-sdk/#/content

**AngularFlamelink.nav**: https://flamelink.github.io/flamelink-js-sdk/#/navigation

**AngularFlamelink.schemas**: https://flamelink.github.io/flamelink-js-sdk/#/schemas

**AngularFlamelink.settings**: https://flamelink.github.io/flamelink-js-sdk/#/settings

**AngularFlamelink.storage**: https://flamelink.github.io/flamelink-js-sdk/#/storage

**AngularFlamelink.users**: https://flamelink.github.io/flamelink-js-sdk/#/users

