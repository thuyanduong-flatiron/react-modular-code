<!-- Couple things:
  - first off, this is looking great. you do a good job communicating the topic!
  - I made smaller grammar corrections in line
  - I added larger thoughts/suggestions in comments
  - components should be capitalized in file names as well. Notice how App.js is by default
  - what's going on with every function being an arrow function? I saw it used as the constructor below as well. Not sure if that behavior works in react, but review the first paragraph: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions
  (Arrow functions have a use and a purpose, but they aren't a replace all functions solution. They should be used where appropriate [i.e. implicit binding of this, inline for better comprehension, etc.]. If a JS developer sees an arrow function, its either because it makes the code easier to read OR you are using it for binding.) consider:
```
function poop() {
  console.log('wot?')
}

const poop = () => {
  console.log('wot?')
}

what is the arrow function bringing us here other than 3 more chars?
plus, no `let` assigned to arrow functions please (see down a ways). it implies we will be re-assigning a variable pointing to a function, which is a bad recipe no no. 
```
 -->

## Introduction
<!-- today, we are talking about x. short and sweet. -->

## Objectives
<!-- what does this readme aim to communicate -->


## Modular Code
<!-- remove reference to 'discussed before'. We are trying to make our curric as non-referential to other curriculum as possible. If we offered a react course for professionals alone, for example, those individuals will not have had discussed that with us. Still make the point that its important, and why. -->
As we've discussed before, maintaining single-responsibility is key to writing clean and DRY code <!-- why? -->, and React was built to support this practice.

In React, we work with components. 
<!-- ...we work with components, which can be expressed in code multiple ways. The most common is via the React class component syntax:
```
class Hogwarts extends React.Component {
  
  render() {
    return (
      <div className="Hogwarts">
        Harry. Did you put your name in the Goblet of Fire?
      </div>
    )
  }
  
}
```

 -->


<!-- Since React applications can grow to significant sizes, we want to make sure we keep it organized. In an effort to do just this, it's standard practice to give each of these components their own file. it is not uncommon to see a React program file tree that looks something like this:

├── README.md
├── public
└── src
    ├── App.js
    ├── Hogwarts.js
    └── SortingHat.js
    
In the example above, each file in src could contain code for a single component.
  -->
  
This empowers the creation of modular code, where units of our programs are clearly labeled and organized by being sectioned off into their own files.

<!-- this transition needs a rework. You set yourself up well in the above statement, then didn't link it well in the next. 

above: "components are modular, this is good."

previously below: "but what I was just telling you about components isn't the important point ('however'), aside from the above point, they are reusable and relatable"

problem: in the below, we discredit the above. instead, go for something along the lines of "Alright, we see that they are modular (they have their own files), and that we can keep them organized this way. Now, all we have to do is figure out how to make use of the code defined in one file within another. Well, this is dirt easy to do in React! Introducing IMPORT EXPORT! <insert dank import export meme... lotsa options>

https://memegenerator.net/img/instances/54479067.jpg
https://memegenerator.net/instance/11027875/yo-dawg-yo-dawg-we-heard-you-like-to-import-data-so-we-put-an-export-feature-into-your-data-import-m
https://cdn.memegenerator.es/descargar/23367796
https://pics.onsizzle.com/file-new-import-export-deport-ctrl-d-trumps-new-favorite-shortcut-3095530.png

"
 -->

What's great about components, however, is that they are reusable and relatable. This means that we'll want to make use of one component inside another file. So how do we do this? With importing and exporting!

## Import Export

<!-- start with what it does instead of the technical relative path line and node referencing etc. In its simplest sense, what does importing/exporting allow us, as react programmers to do? Use modules in other modules. After saying this, give an example, a la:

Let's look at an example of how importing/exporting can be used from a high level. Circling back on our hogwarts file tree:

├── README.md
├── public
└── src
    ├── App.js
    ├── Hogwarts.js
    └── houses
        ├── Gryffindor.js
        ├── Slytherin.js
        ├── Hufflepuff.js
        └── Ravenclaw.js

(Since some of them might not know) Hogwarts School of Magic and Whatever has four houses that make up its student and teacher population. If we were making a react App, we might want to have the `Hogwarts` component make use of every house component. To do this, we would need to make sure to _export_ the house components so they are available for _import_ in the rest of our react application. The code might look like this:

first, export:

```
code snippet export for one house
```

...and then, import!:

```
code snippet importing all houses and throwing them in a render function
```

 -->
We `import` and `export` files by declaring their relative path to the file that we are currently in. We do this so that Node knows we are referencing a local module, as opposed to one found in `node_modules`, or in the global modules.

<!-- ok, here is an important one for you. Above you reference Node. Technically this is right because webpack is bundling via node. Unfortunately, we are so far from students really grasping this, and it risks them convoluting that its the browsers, and not node, that is running the client ready react code in the end. I would just avoid referencing node in general. for most, its a mythical being, and its much easier to have them keep using it totally unaware IMO, but I'll leave that up to you.   -->

### Named exports
<!-- this is a jarring transition. ease them into it. "So far, we were importing whole x. We can also import specific functions from a file like so!" -->
Named exports allow us to export several things at once. This is useful for utility modules or libraries. This is particularly helpful when we have a function or object that we want to reuse across components.

<!-- this example needs a rework. point of named exports is that you can extract specific ones. here this might as well be a default. Simplify the function too.  -->

```js
// In a file called `sortingHat.js`

export let sortingHat = (student) => {
  if (student.name === 'Hermione') {
    return 'Gryffindor'
  } else if (student.name === 'Luna') {
    return 'Ravenclaw'
  } else if (student.name === 'Draco') {
    return 'Slytherin'
  } else {
    return 'Hufflepuff'
  }
}
```
```js
// In a file in the same directory

import {sortingHat} from './sortingHat'
console.log(sortingHat('Hermione')) // prints 'Gryffindor'
```
<!-- show what console would log directly beneath it -->

### Default export

<!-- id start with default exports before going to named exports -->

A default export means that we're exporting only one thing from a file. We use `export default` to move components from their respective files and access them from other locations in our program.

To do this, we call `export default` on a reference to what we want to export. This can be done when defining the class itself such as `export default class Hogwarts extends React.Component {}` or by calling `export default Hogwarts` at the end of the file.
  
<!-- I would suggest keeping it simple to start: 
```js
function poop() {
  console.log('u no it')
}

export default poop
```

OR

```js
export default function poop() {
  console.log('u no it')
}
```

OR

```js
export default function() {
  console.log('u no it')
}
```

all accomplish the same thing. a default export we can import an name whatever we want, i.e.

```js
import noThankYou from './dankMemes/poop.js'

noThankYou()
// > 'u no it'
```
-->

```js
// file: `hogwarts.js`

import React from 'react';

class Hogwarts extends React.Component {
  
  // does react allow this?
  constructor = (props) => {
    super(props)
  }
  
  
  // avoid the interpolation of values below. let's stay focused on import export.
  render() {
    return (
      <div className="Hogwarts">
        <div className="students-list">
          <p>{student.name}</p>
          <img src={student.img} alt="student image"></img>
        </div>
      </div>
    );
  }
  
}

export default Hogwarts;
```
We can then use `import Hogwarts from './hogwarts'` to access the component throughout our program.
<!-- this is sweet. good transition. I would suggest showing it at some point above with plain, non react components too! helps demystify that this is not specific to react.  -->
```js
// In a file in the same directory

import Hogwarts from './hogwarts.js';
import ReactDOM from 'react-dom';
ReactDOM.render(
  <Hogwarts />,
  document.getElementById('root')
);

```

<!-- This is looking awesome guys! -->
