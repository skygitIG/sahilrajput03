# 🤺︎ Hi there 👋

Find me on terminal via `npx sahilrajput03` command.

## Become root user

`sudo su`

_Missing beauty:_ `isBoolean = (a) => typeof a === 'boolean'`

_Recall last n commits in git:_ `git log -n 1`, `git log -n2` works well similarly, i.e., showing last two logs.

## Setup your cli to work with different github accounts

`vi ~/.ssh/config`

and enter code like below:

```
HOST github.com
 HostName github.com
 IdentityFile "C:\Users\Array\Documents\ssh-keys\sahil-account-1"

HOST github.com-sahilrajput03
 HostName github.com
 IdentityFile "C:\Users\Array\Documents\ssh-keys\sahil-account-2"
```

## Get ur ip address

```
curl -s https://checkip.amazonaws.com
# Below works too.
curl checkip.amazonaws.com
```

## I love Promise.allSettled more that I hate `try{}catch(e){}` syntax

read more @ https://javascript.info/promise-api#summary

```
let b = () => Promise.reject(20)

await Promise.allSettled([b()])
// ouput: keyPoint: It never throws error(i.e., `reject("someErrorMessage")`. Yikes!
[
    {
        "status": "rejected",
        "reason": 20
    }
]
So, now you would be tempting to re-write all your previous `try{}catch(e){}` flavoured in a more if/else like manner, don't you .?

// I mean instead of writing:

try{
    const res = await fetch('ss')
    await res.json()
}catch(e){
    console.log('Caught program control thief :LOL: ~sahil~\n', e)
}
// ouput:
Caught program control thief :LOL: ~sahil~
 SyntaxError: Unexpected token < in JSON at position 0
 
// you can write more synchronouse looking code, e.g.,

let res = await fetch('ss')
let [settledRequest] = await Promise.allSettled([res.json()]) 
if(settledRequest.status === 'fulfilled') console.log('yikes, got value', settledRequest.value)
if(settledRequest.status === 'rejected') console.log('shit, got reason', settledRequest.reason)
// isn't that the way you wanted code to be written like from a long time...?
```

## `Promsise.all` vs. `Promise.allSettled` (i.e., either `resolved` or `rejected`)

```js
let a = () => Promise.resolve(10)
let b = () => Promise.reject(20)

// Promise.allSettled
await Promise.allSettled([a(), b()])
// output: keyPoint: It never throws error so we can use it without try and catch(what a godly thing, isn't it ?).
[
    {
        "status": "fulfilled",
        "value": 10
    },
    {
        "status": "rejected",
        "reason": 20
    }
]

// Promise.all
try{
    await Promise.all([a(), b()])
}catch(e){
    console.log('boom', e)
}

// output:
boom 20
```

## Nodemon clear on restart

Windows:

`code ~/nodemon.json`

```json
{
    "events": {
        "start": "reset || cls"
    }
}
```

### Modules

```js
import defaultExport, * as name from "module-name";
import defaultExport, { export1 } from "module-name";
const { default: myDefault, foo, bar } = await import('/modules/my-module.js');



// Anonymous
let myObject = {
  field1: value1,
  field2: value2
};
export {myObject as default};

// above export is equivalent to below:
export default {
  field1: value1,
  field2: value2
};
```
src: [Import in js | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#dynamic_imports)

### Enable ecma modues with nodejs

Desirable way: `node --input-type=module test.js`. Refer here for all ways to do this: [Enabling ESM | Official Docs](https://nodejs.org/dist/latest-v14.x/docs/api/esm.html#esm_enabling). Also, tho use `node test.mjs` if the former seems to much. And do read about the [awesomeness of convention of file extensions standard](https://nodejs.org/dist/latest-v14.x/docs/api/esm.html#esm_mandatory_file_extensions) which is also followed in browsers as well and thus actualy good for real.

### Save some of keystrokes with logs

```js
// commonjs
const { log: l } = require("console");
l("i love commonjs modules.");

//esm
import { log as l } from "console";
l("i love esm modules");
```

### Make async/await cleaner with simple if checks

```js
async function fetchData({ isBad }) {
  try {
    if (isBad) throw "The request is not good...";

    const data = "result data..."; // for e.g., `return await anyPromsieHere()`
    return [data, null];
  } catch (error) {
    return [null, error];
  }
}

async function main() {
  // src: https://youtu.be/ITogH7lJTyE
  const [data, error] = await fetchData({ isBad: true }); //toggle isBad to toggle different behaviour of the api.
  if (data) {
    console.log("got data..");
  }
  if (error) {
    console.log("there is some error with the api...");
  }
}

main();
```

**This might look like a overkill for any simple api but if you have only two three api's and you need to check add try/catch for each of them in a single scope it all becomes whole messy to look at ... but if you use something like..**

```
  const [userData, userError] = await fetchUserData({ isBad: true });
  const [locationData, locationError] = await fetchLocationData({ isBad: true });
  const [friendsData, friendsError] = await fetchFriendsData({ isBad: true });
  // now you can simly put 6 if checks to check for what is actually error and you code actually gets out of control (i.e., *program control) LITERALLY.
```

### Get used to javascript objects(works good in both node and browser both, tested):

```js
var cron = require("node-cron");
let cron1 = "30 * * * * *";

cron.schedule(cron1, () => {
  var d = new Date();
  var h = d.getHours();
  var m = d.getMinutes();
  var s = d.getSeconds();

  console.log("==1>", new Date().toLocaleString());
  console.log("==2>", h); // 20 that means 8pm.
  console.log("==3>", m); // 32 that means 32 minutes past.
  console.log("==4>", s); // 30 that means 30 seconds past.
  console.log("==5>", d); // this is not readable at all :lol:
});

```

- You can always use ?. operator in browser and react projects irrespective of if you are using typescript or not. Yes, its fun, isn't it.!

*You need to press y for first time though.

- Super charge your windows bash experience with my aliases and functions:

```bash
curl -o ~/.bashrc https://raw.githubusercontent.com/sahilrajput03/my_bin/master/files/.bashrc-windows/.bashrc
# This command simply adds/updates your existing `~/.bashrc file`. Too much fun, isn't it :)
```

- Add `prettier-write` script to your package.json file using command
```bash
npm set-script prettier-write "prettier --write ."
curl -O https://raw.githubusercontent.com/sahilrajput03/my_bin/master/files/.prettierrc.js
curl -O https://raw.githubusercontent.com/sahilrajput03/my_bin/master/files/.prettierignore
```

- Make emmet work on your jsx files as well

Enable Setting: `Emmet: Trigger Expand On Tab` and set `ctrl+e` as key binding for `Emmet: Expand Abbreviation`. Enjoy emmet in JSX with ctrl+e now for the rest of life.

- Want Husky? [VERIFIED] : 

```bash
npx husky-init && npm install
```

Now edit the `.husky/pre-commit` file and add desired command i.e., `npm run prettier-write` there in place of command `npm test`. And don't forget to tell other contributors to use below command to get their husky setup on rocket for their future commits.

```
npm i
```

Help: [Src1](https://typicode.github.io/husky/#/), [Src2](https://www.youtube.com/watch?v=oWty0Nw1ydk), [Src3: CRA](https://create-react-app.dev/docs/setting-up-your-editor/#formatting-code-automatically).

- **Got time**
0. Read and test whole official [cra docs](https://create-react-app.dev/).
1. Learn [story book or styleguidist](https://create-react-app.dev/docs/developing-components-in-isolation) , either one and do some good tutorial from their site or youtube. :D GOOD LUCK!!
2. Leanr pre-rendering from cra docs [here](https://create-react-app.dev/docs/pre-rendering-into-static-html-files).

## My favourite drawing app

Browse at https://asciiflow.com/#/ .

## 🤠︎ Write data to a new/existing file directly with the terminal

Copy data to clipboard, and in terminal use 

`$ cat > myFile.txt` and hit enter, and now paste data in the terminal itself and press `ctrl+d` to save the file. Thats it 🤠︎.

### Techonologies 

<img src="https://img.shields.io/badge/react%20-%2320232a.svg?&style=for-the-badge&logo=react&logoColor=%2361DAFB"/> <img src="https://img.shields.io/badge/react_native%20-%2320232a.svg?&style=for-the-badge&logo=react&logoColor=%2361DAFB"/>
<img src="https://img.shields.io/badge/express.js%20-%23404d59.svg?&style=for-the-badge"/>
<img src="https://img.shields.io/badge/material%20ui%20-%230081CB.svg?&style=for-the-badge&logo=material-ui&logoColor=white"/>
<img src="https://img.shields.io/badge/git%20-%23F05033.svg?&style=for-the-badge&logo=git&logoColor=white"/>
<img src="https://img.shields.io/badge/vercel%20-%23000000.svg?&style=for-the-badge&logo=vercel&logoColor=white"/>
<img src ="https://img.shields.io/badge/MongoDB-%234ea94b.svg?&style=for-the-badge&logo=mongodb&logoColor=white"/>
<img src="https://img.shields.io/badge/docker%20-%230db7ed.svg?&style=for-the-badge&logo=docker&logoColor=white"/> [![style: styled-components](https://img.shields.io/badge/style-%F0%9F%92%85%20styled--components-orange.svg?colorB=daa357&colorA=db748e)](https://github.com/styled-components/styled-components)
<img alt="CircleCI" src="https://img.shields.io/badge/CIRCLECI%20-%23161616.svg?&style=for-the-badge&logo=circleci&logoColor=white"/>
<img alt="GitHub Actions" src="https://img.shields.io/badge/github%20actions%20-%232671E5.svg?&style=for-the-badge&logo=github%20actions&logoColor=white"/>
<img alt="Debian" src="https://img.shields.io/badge/Debian-D70A53?style=for-the-badge&logo=debian&logoColor=white" />

### Social

[<img src="https://img.shields.io/badge/github%20-%23121011.svg?&style=for-the-badge&logo=github&logoColor=white"/>](https://github.com/sahilrajput03)
 [<img src="https://img.shields.io/badge/@freakstarrocks%20-%231DA1F2.svg?&style=for-the-badge&logo=Twitter&logoColor=white"/>](https://twitter.com/freakstarrocks)
[<img src="https://img.shields.io/badge/sahilrajputfreakstar%20-%23FF0000.svg?&style=for-the-badge&logo=YouTube&logoColor=white"/> ](https://www.youtube.com/user/sahilrajputfreakstar/playlists)
[<img src="https://img.shields.io/badge/linkedin%20-%230077B5.svg?&style=for-the-badge&logo=linkedin&logoColor=white"/>](https://www.linkedin.com/in/sahilrajput03/)

[<img alt="Telegram" src="https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white" />](https://t.me/sahilrajput03)
[<img alt="Discord" src="https://img.shields.io/badge/sahilrajput03%234631%20-%237289DA.svg?&style=for-the-badge&logo=discord&logoColor=white" />](#)
<i>[Badges?](https://github.com/Ileriayo/markdown-badges)</i>

### Codesandboxes/Codepens/etc

[Sahil Rajput @codesandbox](https://codesandbox.io/u/sahilrajput03)

[Tanner Linsley @ codesandbox](https://codesandbox.io/u/tannerlinsley/sandboxes)

[Kevin Powell @ codepen](https://codepen.io/kevinpowell)

### Packages published @ `npm.com`/`yarnpkg.com`

- [useWhat](https://www.npmjs.com/package/usewhat)

- [useStateM](https://www.npmjs.com/package/usestatem)

- [mongo-quick](https://www.npmjs.com/package/mongo-quick)

- [jsonbackend - A true object database server.](https://www.npmjs.com/package/jsonbackend)

- [react-fetch2](https://www.npmjs.com/package/react-fetch2)

- [useEffectFactory](https://www.npmjs.com/package/useeffect-factory)

- [r_global](http://npmjs.org/package/r_global)

- [Pagelist React Component - Test/Create apps made easy](https://www.npmjs.com/package/pagelist-react)


### Services

- [Axios playground](http://axiosplayground.ml/)
- [Json backendserver](https://jsonbackendserver.herokuapp.com/)
- [Graphql Playground - Query with power](https://abstraction.ml)
- [Fly 🚀︎ a codesandbox](https://flycodesandbox.netlify.app/)

## Blogs

- [Jaadujinn.ml](https://jaadujinn.ml)

- [Reverberate.ml](https://reverberate.ml)

- [SahilRaput.ml](https://sahilrajput.ml)

- [Docs](https://reverberate.ml/docs)

- [Uses](https://reverberate.ml/uses) (Sofwares stack for windows 🥝︎ users)

- [Linux Setup 💓︎](github.com/sahilrajput03/my_bin)

## Codesandbox and github integrations work 

[Link to Article docs](https://codesandbox.io/docs/git), [Massive different guides for importing to codesandbox directly](https://codesandbox.io/docs/importing#import-from-github)

### Comments

- I'm a yarn fan though.
- Use https://picsum.photos/ (https://unsplash.it/) for using placeholder images 🚀︎.
- Use https://uifaces.co/browse-avatars/ for person images/avatars.
- Use https://imgur.com/upload for hosting your gifs very fast🚀︎.
- Use gist for sharing code blazing fast: https://gist.github.com/
- Software is like sex: it's better when it's free. - Linus Torvalds
- Learning is a algorithm, you stop it, you're gonna see errors. ~unknown

## Priority1: Center element using simple margin auto

Q. Does margin auto center vertically?
Ans. If the display of your parent container is flex , then yes, margin: auto auto (also known as margin: auto ) will work to center it both horizontally and vertically, regardless if it is an inline or block element.


## Priority2:  Center element like a pro

```css
.myElement{
    position: absolute/relative;
    transform: translate(-50%, -50%);
    top: 50%;
    left: 50%;
}
```

## Priority3: Center element like a master

```css
.myEl{
 position: absolute;
 top: 0;
 left: 0;
 right: 0;
 bottom: 0;

 width: 50%;
 height: 50%;
 margin: auto;
 <!-- ^ this does the centering magic when complemented with all the above settings and don't forget to make the container of current element as ''position: relative'' -->
}

.container{
 position: relative;
}

```

## css selector

```css
p ~ ul {
  background: #ff0000;
/*This will apply to all ul's that are anywhere(not just next to it) after the p tag.*/
}
```

## Practical example of both of above complementary usage

src: https://codepen.io/sahil-blulabs/pen/jOmrGXg?editors=1010

## Issue: `grid-gap: 0` is not working ??

See fix  at @ [codepen](https://codepen.io/sahil-blulabs/pen/zYwKKwL).

## Using grid-area names in grid

Article at https://css-tricks.com/simple-named-grid-areas/ .

## Use native browser history api instead of react-routed-dom api everytime


```jsx

const history = (path) => window.history.pushState("", "", path);

const jsx = () => {

return <div>
         <button
           onClick={() => {
             history("/boom");
           }}
         >
           Click me to go to /boom
         </button>

         <button
           onClick={() => {
             history("/bamm");
           }}
         >
           Click me to go to /bamm
         </button>
       </div>
}
```

## React eslint + prettier settings

1. Ensure that `package.json` file has below content: 

```json
{
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
}

```

2. Use below commands to install some dependencies, add `.eslintrc.js`, `.prettierrc.js` and `.prettierignore` in a CRA project's root directory:

```
npm i -D eslint-config-prettier eslint-plugin-prettier
curl -O https://raw.githubusercontent.com/sahilrajput03/my_bin/master/files/eslint-config-react/.eslintrc.js
curl -O https://raw.githubusercontent.com/sahilrajput03/my_bin/master/files/.prettierrc.js
curl -O https://raw.githubusercontent.com/sahilrajput03/my_bin/master/files/.prettierignore
npm set-script prettier-write "prettier --write ."
npm run prettier-write
```

Thats all it takes and don't forget to restart your react server.

## Debugging made easy in vscode itself (src: CRA documentation

src: https://create-react-app.dev/docs/setting-up-your-editor/#visual-studio-code

## What is `initial`, `inherit`, `unset`, `all:initial/inherit/unset` ??

Src: [Kyle's youtube video](https://www.youtube.com/watch?v=N8tFrMZp_wA)

E.g., 1:

Below code will make these divs appear as side by side coz initial value for `display` property is `iniline`.

```txt
<div>div1</div>
<div>div2</div>

div{
  display: initial;
}
```

E.g., 2:

Below code demonstrates that some properties are always inherited like [`font-size`](https://developer.mozilla.org/en-US/docs/Web/CSS/display#formal_definition), [`font-family`](https://developer.mozilla.org/en-US/docs/Web/CSS/font-family#formal_definition) whereas some are never inherited like [`border`](https://developer.mozilla.org/en-US/docs/Web/CSS/border#formal_definition), [`outline`](https://developer.mozilla.org/en-US/docs/Web/CSS/outline#formal_definition), 

```txt
<div>
  I am a div.
  <p>I am a paragraph.</p>
</div>
<p class="imp">I am paragraph imp.</p>

div{
  font-size: 2rem;
/*   ^ font-size is inherited in p tag as well. */
  border: 1px solid blue;
/*   ^ border is not inherited unless you specifically explicitly inherit it. */
}

p{
/*   border: inherit; */
}
```

E.g., 3

```txt
button{
 all: unset;
<!--  ^^ This will remove all the browser's and other user defined css for this element, and now all the shit things are purged automatically(and thats what you want mostly for buttons). Yikes!!  -->
 background-color: red; 
}
```

E.g., 4: In below example the padding and border property values are set to browser's style sheet for chrome/firefox/etc and below code does nothing coz all the values for all the properties are set to rever by default. `revert` is only useful in cases when you just need to undo your own style property sometimes(which is very rare though).

```
button{
 padding: revert;
 border: revert;
}
```

More information:

```txt
- CSS Property values: initial, inherited, 

- You can find default values of each css properties @ mdn in the "Formal definition" section. 


- For a ``div`` in all browsers the value for `div` is set as `display: block` but by the css specifications's ``initial`` value for property of ``display`` is ``inline`` as you can read [here](https://developer.mozilla.org/en-US/docs/Web/CSS/display#formal_definition).

You should always use ``font-family: inherit`` in buttons (so they can actually get your custom font) coz otherwise they get font-family property as `Arial` from browser's ``User Agent Stylesheet``.

``display`` property has default value for inherited as false. [Src](https://developer.mozilla.org/en-US/docs/Web/CSS/display#formal_definition).
``border`` property has defaut value for inherited as false. [Src](https://developer.mozilla.org/en-US/docs/Web/CSS/border#formal_definition)
``font-size`` property has default value for inherited as true. (this means any nested child will have the same font-size coz they inherit the font-size of the parent. [Src](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size#formal_definition)

``unset`` as value for a property will make that property to either set as ``inherit`` or ``initial`` where inherit means exactly what it means and ``initial`` means 

- Magic: If you set ``all: unset`` in any element in css then all css properties of that selected element will be seet to ``inherit`` or ``initial``,
```

### Some selectors (src: kyle's css selector cheatsheet, find it in your `CSS Resources` telegram group.

#### `:first-child` selector

```
<div>
  <span>I am span 1.</span>
  <span>I am span 2.</span>
  <span>I am span 3.</span>
</div>

span:first-child{
  color: red;
/* Only "I am span 1" will be coloured red. */
}
```

#### `:last-child` selector

```
<div>
  <span>I am span 1.</span>
  <span>I am span 2.</span>
  <span>I am span 3.</span>
</div>

span:last-child{
  color: red;
/* Only "I am span 3" will be coloured red. */
}
```

#### `:nth-child(2n)` selector

```
<div>
  <span>I am span 1.</span>
  <span>I am span 2.</span>
  <span>I am span 3.</span>
  <span>I am span 4.</span>
  <span>I am span 5.</span>
</div>


span:nth-child(2n){
  color: red;
/* Only "I am span 2" and "I am span 4" will be coloured red. */
}

```

#### `:nth-last-child(1)`

```
<div>
  <span>I am span 1.</span>
  <span>I am span 2.</span>
  <span>I am span 3.</span>
</div>

span:nth-last-child(1){
  color: red;
/* Only "I am span 3" will be coloured red. */
}
```

#### `:only-child`

```
<div>
  <span>I am span 1.</span>
  <span>I am span 2.</span>
  <span>I am span 3.</span>
</div>

<div><span>I am single span.</span></div>

span:only-child{
  color: red;
/* Only "I am single span." will be coloured red. */
}
```

#### `a:first-of-type`

```
<div>
  <span>I am span 1.</span>
  <span>I am span 2.</span>
  <span>I am span 3.</span>
</div>

<div>
  <div>I am simple div.</div>
  <span>I am simple span.</span>
</div>

span:first-of-type{
  color: red;
/* Only "I am single span." and "I am span 1." will be coloured red. */
}
```

#### `a:last-of-type`

```
<div>
  <span>I am span 1.</span>
  <span>I am span 2.</span>
  <span>I am span 3.</span>
</div>

<div>
  <div>I am simple div.</div>
  <span>I am simple span.</span>
</div>

span:last-of-type{
  color: red;
/* Only "I am span3." and "I am simple span." will be coloured red. */
}
```

#### `a:nth-of-type(2n)`

```
<div>
  <div>I am span 1.</div>
  <span>I am span 2.</span>
  <span>I am span 3.</span>
</div>

<div>
  <div>I am simple div1.</div>
  <div>I am simple div2.</div>
  <span>I am simple span1.</span>
  <span>I am simple span2.</span>
</div>


span:nth-of-type(2n){
  color: red;
/* Only "I am span3." and "I am simple span2." will be coloured red. */
}
```

#### `:nth-last-of-type(2)`

```
<div>
  <div>I am span 1.</div>
  <span>I am span 2.</span>
  <span>I am span 3.</span>
</div>

<div>
  <div>I am simple div1.</div>
  <div>I am simple div2.</div>
  <span>I am simple span1.</span>
  <span>I am simple span2.</span>
</div>

span:nth-last-of-type(2){
  color: red;
/* Only "I am span2." and "I am simple span1." will be coloured red. */
}
```

#### `a:only-of-type`

```
<div>
  <div>I am div 1.</div>
  <div>I am div 2.</div>
  <span>I am span 1.</span>
  <div>I am div 3.</div>
</div>

<div>
  <div>I am simple div1.</div>
  <div>I am simple div2.</div>
  <span>I am simple span1.</span>
  <span>I am simple span2.</span>
</div>

span:only-of-type{
  color: red;
/* Only "I am span1." will be coloured red. */
}
```

#### `a:not(.c)`

```
<div>
  <span class='c1'>I am span 1.</span>
  <span class='c2'>I am span 2.</span>
  <span class='c3'>I am span 3.</span>
  <span class='c2 c3'>I am span 4.</span>
</div>

span:not(.c2){
  color: red;
/* Only "I am span1." will be coloured red. */
}
```

### Ease with Dates

Date() and Date.now() gives you:

```
"Mon Aug 23 2021 18:49:44 GMT+0530 (India Standard Time)" and 1629724786923 respectively.
```
