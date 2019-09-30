# React workshop

Les diapositives de la présentation sont disponibles [ici](https://github.com/ewendel/slidesets/raw/master/react-workshop-forwardjs.pdf)

## Instructions

Assurez-vous que Node.js est installé, sinon installez-le à partir de https://nodejs.org/.

Clonez ce repo :

```
git clone https://github.com/ewendel/react-workshop.git
cd react-workshop
```

Installer les dépendances du projet :

```
npm install
```

Démarrer le serveur web :

```
node app.js
```

## Les tâches

Ci-dessous, vous trouverez toutes les tâches que nous réaliserons dans le cadre de cet atelier.
Pour la première partie de cet atelier, nous avons déjà créé tous les fichiers dont vous aurez
besoin pour résoudre ces tâches, vous n'aurez donc pas à créer de nouveaux fichiers vous-même.
Vous pouvez trouver tous les fichiers nécessaires dans le dossier des tâches,
où vous devez également résoudre les tâches.

Dans ces fichiers, le code source de React.js et un JSX-transpiler sont déjà inclus afin que
vous n'ayez pas besoin de refaire à chaque fois le code front-end pendant le développement.
Certains des exercices incluent des CSS pré-écrits, donc vous n'aurez pas besoin d'écrire de CSS
(à moins que vous ne vouliez pimenter les choses, bien sûr).


Pour commencer, allez à : [`http://localhost:3000`](http://localhost:3000)

**N'oubliez pas de jeter un coup d'œil à la documentation de React 
[React's documentation](http://facebook.github.io/react/docs/)
pendant que vous travaillez sur les tâches.**

# Partie I : Se familiariser avec React

## Task 1 : Creating your first component

(Pour cette tâche, éditez les fichiers dans le répertoire `/tasks/1/`.
Les changements doivent être visibles dans  [http://localhost:3000/1](http://localhost:3000/1)) 

Créez un composant React simple qui affiche "Hello World".

Pour résoudre cette tâche, nous devons créer un composant React, implémenter un render
dans le composant, puis rendre le composant React dans le DOM.

#### Astuces

Liens utiles:

- [`Getting started`](https://reactjs.org/docs/hello-world.html)
- [`Components`](https://reactjs.org/docs/components-and-props.html)
- [`ReactDOM.render`](https://reactjs.org/docs/react-dom.html#render)

## Tâches 2 : Transmission des données et utilisation de JSX

Réutiliser le composent de la tâche 1 auquel on ajoute une propriété appelée `name`
à partir de son parent et écrivez "Hello, {name}".<br> Si le composant n'est pas passé
en argument, il affichera par défaut la valeur "World".

Ensuite, créez un composant appelé `Helloes` qui accepte une propriété `names` (tableau)
et utilise le composant précédent pour écrire "Hello, {name}" pour chacun des éléments
dans le tableau `names`.

#### Astuces

`props` sont utilisés pour passer les données des composants parents aux composants enfants - accessibles via
`this.props` et ils sont immuables.

`render()` doit retourner qu'un seul noeud

Rappelez-vous que vous pouvez utiliser le JavaScript standard dans JSX en utilisant `{ }` pour le protéger.

Méthodes utiles: `Array.prototype.map`

Liens utiles: [les listes et les clés en React](https://reactjs.org/docs/lists-and-keys.html)


## Têches 3 : Composants à état : Timer

Créer un composent qui se nomme `Timer` qui affiche le temps passé
depuis que le composant a été initialisé. Exemple :

`I was started 7.8 seconds ago`

Le composant doit se mettre à jour 10 fois par seconde, et le composant
devrait mettre à jour les secondes sans réécrire le timer en dessous.

#### Astuces

Nous utilisons `state` pour stocker nos données qui changent pendant la durée de vie d'un composant.
Il est accessible via `this.state`.

Méthodes utiles : `setInterval, clearInterval`.
Méthodes du cycle de vie : `componentDidMount, componentWillUnmount`
[Pour en savoir plus sur l'état et les méthodes du cycle de vie, consultez la documentation](https://reactjs.org/docs/state-and-lifecycle.html)

Pour démonter le composant, utilisez l'option
[`ReactDOM.unmountComponentAtNode`](https://reactjs.org/docs/react-dom.html#unmountcomponentatnode)
aide, par exemple

```js
setTimeout(function() {
    ReactDOM.unmountComponentAtNode(...);
}, 3000);
```

## Têche 4: Plus d'état : Recherche en temps réel

Créez un composant `Search` qui prend un tableau appelé `items` (a prop).
Le contenus dans le tableau auront le format suivant : `{ name: 'Some
string', url: 'www.somesite.com' }`

Le composant doit inclure un champ texte, et les éléments du tableau doivent être
filtrées en fonction de la valeur rentrée par l'utilisateur dans ce champ texte.
La structure HTML devrait ressembler à ceci :

```html
<div>
    <input />
    <ul>
        <li><a ...></a></li>
        <li><a ...></a></li>
        <li><a ...></a></li>
    </ul>
</div>
```

Aussi - assurez-vous que le champ de saisie a le focus après l'affichage du composant.

#### Astuces

Helpful methods: `String.prototype.match, Array.prototype.filter`

Useful attributes in JSX: `onChange`, `refs`, `className` (because `class` is a reserved keyword in JavaScript)

--

# Part II: Twitter Dashboard

In this task you will create a super-cool Twitter Dashboard.

## Setup

If you do this workshop _outside_ of a conference, you have to
get access to the Twitter API before you start working on the
tasks. Follow the guide in
[`twitter-setup.md`](twitter-setup.md) to get access and setup the correct files.

**NB!** If you're at a conference with us you DON'T have to
set up Twitter API access!

### Local setup

Go to the `case/task` folder, then start by installing dependencies and starting
the development tool:

```
cd case/task

npm install

npm start
```

Here we've run the bootstrapping tool [create-react-app](https://github.com/facebook/create-react-app), which sets up all the build
tools we'll need to create even advanced production apps. 

`npm start` starts a development server, which automatically recompiles your 
code on every change. Pretty neat, huh? It'll even open your browser window to 
the correct address!

Then, start the server in another terminal window (remember to go the the
`case/task` folder first) with `npm run server`.

You should see the text "Dashboard".

## Step-by-step guide

### Task 1: Rendering a single tweet

Create a component, `Tweet`, in `src/components` that accepts a
tweet object and renders this. For now, use this component from the
Dashboard component.

As we still haven't fetched tweets from Twitter, you can use
the example tweet object found in `case/task/example-tweet.json`.
As a hint, in Node you can actually require a json file directly:

```javascript
var jsObject = require('./some-file.json');
```

The `Tweet` component should have the following HTML structure
(which gives you some free CSS):

```html
<div class="tweet">
    <div class="tweet-header">
        <img class="tweet-image" src="some/url/image.jpg" />
        <div class="tweet-image-offset tweet-name">Knut Olav</div>
        <div class="tweet-image-offset tweet-screen-name">@VerdensKongen</div>
    </div>

    <div class="tweet-text">Hello, fellow developers!</div>
    <div class="tweet-stats">
        <span class="tweet-user-followers">
            <strong>12,058</strong>
            <span class="tweet-stats-desc">followers</span>
        </span>
    </div>
    <span class="tweet-flag flag-icon flag-icon-no"></span>
    <span class="tweet-country tweet-stats-desc">Norge</span>
    <div class="tweet-city tweet-stats-desc">Langesund, Telemark</div>
</div>
```

(Remember that `class` and `className` are not the same)

Take note of the element with the class `flag-icon-no`, where
the two last letters incide the country code of the tweet's
origin. (i.e. `no` for Norway).

### Task 2: Fetching real tweets

Afterwards, set up a WebSocket connection to the server in order to
receive tweets from the API. This should be done in the `Dashboard`
component when it is mounted. Pass the most recently received tweet to
the `Tweet` component. (For easier debugging we don't push that many
tweets yet, so it might take a few seconds between each new tweet.)

Here's a list of lifecycle methods available in React:

- https://reactjs.org/docs/state-and-lifecycle.html

This is the code needed to set up a WebSocket connection and receive tweets:

**NOTE!** If you haven't been through the Twitter API setup, remember to ask us
for the correct IP address to use instead of `localhost`!

```javascript
const ws = new WebSocket('ws://localhost:9999');
ws.onmessage = (ms) => {
    var newTweet = JSON.parse(ms.data);
    // TODO: Do something with this tweet data!
};
```

### Task 3: A list of tweets

Expand the `Dashboard` component to render a list of all
received tweets in a `<ul>`. This list should have the class
`tweetlist`.

Move all the code related to showing this list into a new component
`TweetList`, that receives a list of tweets to render. Only render the
last three received tweets.

Note: you should still use the `Tweet` component created
earlier to render each individual tweet.

### Task 4: Tweets on a map

Time to plot where on earth all these tweets are coming from!

We will use the component called [`react-google-maps`](https://www.npmjs.com/package/react-google-maps) 
(ensure that you choose the right package, as there are others with similar 
names).

Now run `npm install <package name>` to install this package.

Create a `TweetMap` component that you use from the `Dashboard`
component. This new component should `render` a top-level div with the
CSS class `tweet-map`. With the help of the `react-google-maps`
documentation, render a simple map into this div.

These settings are a good starting point for the map:

- `defaultZoom`: `3`
- `defaultCenter`: `{ lat: 30.675226, lng: -35.051272 }`

Here's a working example you can play with: https://codesandbox.io/s/2xyw6n4o9y

Each tweet has a geolocation. Use this to the place a marker on the map for
each tweet.

>(If you have set up the Twitter API access yourself, you can control the
>rate at which you receive tweets on the frontend.  In `task/twitter-ws.js`,
>change the value of the `currentSpeed` variable to some other value, then
>restart the backend, i.e. re-run `npm start`.)

It can be wise to only use, let's say, the last hundred received tweets
in order to avoid your computer from crashing due to the vast amounts
of data.

### Task 5: Influential tweets

Now that we are receiving more tweets, it is becoming harder to read the
tweets in our `TweetList`. Change this component to show the three tweets that
have the most followers amongst the tweets that are shown on the map.

### Task 6: Current tweet

We want to to be able to click on one of our map markers in order to
highlight and show that tweet. Make a new component `CurrentTweet` to
be used for displaying the selected tweet. It should use the `Tweet`
component to render the tweet, and for some free styling, you can use
the class `current-tweet`.

The selected tweet should have its own marker color. The `Marker`
component accepts a prop called `icon` that takes an image url. Here
are some suitable images that can be used:

```
http://maps.google.com/mapfiles/ms/icons/red-dot.png
http://maps.google.com/mapfiles/ms/icons/yellow-dot.png
http://maps.google.com/mapfiles/ms/icons/blue-dot.png
http://maps.google.com/mapfiles/ms/icons/green-dot.png
```

Hint: Remember that you can pass functions into a component as a prop,
e.g. as with `onChange` in [forms](https://reactjs.org/docs/forms.html).

Hint 2: It's possible to pass along all props to child components:
[docs](https://reactjs.org/docs/components-and-props.html).

### Task 7: shouldComponentUpdate

Considering the amount of incoming tweets, it could be wise to help React
understand whether it needs to check if a component has changes that should be
rendered to the DOM. (That is, when a call to `render()` would produce the same
output as the previous call).

By using `console.log` in the `render`-method of our `CurrentTweet`
component we can see how often it is called. Check this again after
having implemented the lifecycle method `shouldComponentUpdate`. See
the docs for how this method works.

### Task 8: App Header

Our app needs a header. In addition to showing the app name (which is yours to
decide), it should display the number of seconds that has passed since it
started running (sounds familiar?) and the number of tweets it has processed so
far.

The HTML could look something like this:

```html
<div class="app-header">
    <h1>Crazy-name, yo</h1>
    <div>
        <span class="tweet-stats-desc">seconds running</span>
        <strong>12</strong>
    </div>
    (similar for no. of tweets)
</div>
```

(Remember to reuse the `Timer` component you created in part 1!)

### Task 9: Country statistics

We would like to display which countries that create the most tweets. Create a
component `CountryList` that does this. It should take into account all tweets
ever received, not just the last hundred.

The HTML could look like this:

```html
<ul class="countrylist">
    <li>
       <span class="tweet-flag flag-icon flag-icon-no"></span>
       <span class="country-tweet-count">25</span>
    </li>
</ul>
```

Hint: You don't need to keep a record of all the tweets, only the
number of tweets per country.

### Task 10: Creating a "shared" component

We are now displaying small flag icons in two different places in our
app. It is not beneficial to have this code duplication, so refactor
this into a `Flag` component.

--

## Finished!

Now you should have quite a good grasp of how React works. If you want to
learn more about using React in large apps, you should take a look at Redux, the most recognized implementation of the Flux pattern.

The author, Dan Abramov, has created a brilliant online course on Redux [available on egghead.io](https://egghead.io/series/getting-started-with-redux).

### Articles

* [Removing User Interface Complexity, or Why React is Awesome] (http://jlongster.com/Removing-User-Interface-Complexity,-or-Why-React-is-Awesome)
* [Reacts diff algorithm](http://calendar.perfplanet.com/2013/diff/)
* [About ClojureScript and functional programming in React] (http://blog.getprismatic.com/om-sweet-om-high-functional-frontend-engineering-with-clojurescript-and-react/)

### Videos

* [The Secrets of React's Virtual DOM](https://www.youtube.com/watch?v=-DX3vJiqxm4)
* [Rethinking Best Practices](https://www.youtube.com/watch?v=x7cQ3mrcKaY)
* [Be Predictable, Not Correct](https://www.youtube.com/watch?v=h3KksH8gfcQ)
* [How Instagram.com Works](https://www.youtube.com/watch?v=VkTCL6Nqm6Y)
* [Hot Reloading with Time Travel](https://www.youtube.com/watch?v=xsSnOQynTHs)
* [High performance functional programming with React and Meteor](https://www.youtube.com/watch?v=qqVbr_LaCIo)

