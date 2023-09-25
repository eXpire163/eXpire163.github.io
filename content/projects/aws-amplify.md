---
title: "AWS Amplify Intro"
date: 2023-09-18T09:38:31+02:00
draft: false

cascade:
  featured_image: 'https://gohugo-ananke-theme-demo.netlify.app/images/gohugo-default-sample-hero-image.jpg'

---

## Whay should i care about it

If you are a developer or an UX designer wanting to build a public website dealing with data and users and don't want to learn all trillien tecks needed for. Or you are just sick of writing boiler plate code.

## Goal

Have a simple data structure that allows via a Website to CRUD (Create, Read, update and delete) items in a visually not to ugly way and secure everything with a user management.

## Requirements

- AWS account
- Google account (for a free login to figma - ui editor)
- 60-180 minutes time

- installed locally: git and a code editor (e.g. vs-code)
- some coffee/tee


## Create an app

1. Go to aws amplify and click on `create new app -> build an app -> choose a name -> get a coffee`.
2. Select the app and the backend tab and " Launch Studio"

## Usefull links

1. To the learning section https://docs.amplify.aws/console/
2. To the libraries https://docs.amplify.aws/lib/q/platform/js/

## Get the data structure

1. Go to `Set Up -> Data` on the left
2. create your first table
> latest version of amplify finaly relational data, but we don't today

> WARNING: Go to GraphQL API Settings and enable versioning and conflict resolution, otherwise it will not work

3. Hit `Save and Deploy`

![data table](/aws-amplify/data.png)

## Design the ui

1. Go to the learning sestion link -> UI with Figma and grab the Figma link (https://www.figma.com/community/file/1047600760128127424)
2. Open it an clone it
3. then insert it in amplify



4. Accept everything two times
5. Explore in Figma the Item Card in My Components

### Lets build a view with real data

1. Insert dummy data via `Content -> Select our table -> Action -> Aut-generate`

![generating data dialog](/aws-amplify/data_generator.png)

2. Via  UI Libraray -> Components -> ItemCard -> Configure you can map the proteries
    1. select t-shirt on the left and `bind to data -> superstoreitem.name`
    2. Classic long sleve to `superstoritem.details`
    3. $99 to `superitem.prive`

Now you can shuffle the data if you like to test your UI

3. Create a collection on the top right

![create collection](/aws-amplify/collection.png)

4. Now enable search an pagination for our collections

## Create a react app

You can use angular vew or react native or many more but this should make it clear

1. Create an app

```
npx create-react-app superstore
cd superstore
npm start
```

2. add aws amplify

> you can go to the docs or at anytime in amplify to the top right and get the `local setup instructions`

`amplify pull --appId your_id --envName staging`

Acceppt the secret login page


Setup the amplify cli and include react stuff
```
npm install -g @aws-amplify/cli
npm install aws-amplify @aws-amplify/ui-react
```

Import amplify into your react app in `src/index.js`

```
import {ThemeProvider} from "@aws-amplify/ui-react";
import { Amplify } from 'aws-amplify';
import awsconfig from './aws-exports';
import "@aws-amplify/ui-react/styles.css";
import studioTheme from './ui-components/studioTheme';
Amplify.configure(awsconfig);
```

And use it by replacing the `strict react with`:

```
<ThemeProvider theme={studioTheme}>
    <App />
</ThemeProvider>
```

> run `npm start` as often as possible to see where it breaks

## Show our items

In the `App.js` import our collection

> If you go back to the collection editor you can grab the code from "get component" at bottom

```
import {
 ItemCardCollection
} from './ui-components';
```

```
<ItemCardCollection />
```

> run `npm start` as often as possible to see where it breaks

## Summery ONE

We have designed our datastructure, filled it with data and stored it in dynamo db
We have build an UI with everything you need nower days


## Get authenticated

Go to Authentication on the left and then deploy (or explore lots of cool things on this page first)

Go to your App.js and add the auth stuff (code is from the Library link -> Authentication)

```
import { Amplify } from 'aws-amplify';

import { withAuthenticator } from '@aws-amplify/ui-react';
import '@aws-amplify/ui-react/styles.css';

import awsExports from './aws-exports';
Amplify.configure(awsExports);

function App({ signOut, user }) {
  return (
    <>
      <h1>Hello {user.username}</h1>
      <ItemCardCollection />
      <button onClick={signOut}>Sign out</button>
    </>
  );
}

export default withAuthenticator(App);
```

This would create an error now, so lets fix it:

Run `amplify pull` and you should have all components ready to go

> run `npm start` as often as possible to see where it breaks

Click on register, then sign in and you are logged in!!!

## Summery TWO

We have create a congito user pool, a sign in mechnism that also support google/facebook ....
We have added all needed user dialogs


## Fazit

Amplifly has still a long way to go but i you just want to kickstart something - use it.
