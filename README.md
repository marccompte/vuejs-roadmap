# Vue.js Teacher's Roadmap

## Day 1

There should not be a big step between the previous module and the Vue.js module. So, this first day should be used to transition from the old style stand-alone JS/HTML/CSS to a Vue.js build setup.

The first session will start by using Vue.js as a CDN resource and we'll finish the day by deploying a build setup very similar to the one used througout the rest of the module (Vue3 + Vite + Pinia + Router.)

###  Session 1 (~120 minutes, with a break or two)

Redo the Ironhack Cart lab in front of the students using Vue.js as a CDN. Use this exercise to introduce the basic features of Vue.js.

Explanations in some cases should be pretty shallow, later on we'll go more in depth on most of them.

#### Iteration 1

##### Step 1. Loading Vue.js as a CDN

Explain the difference between using Vue.js as an addition to a live website and using Vue.js to build an SPA site. A general explanation should suffice for now. It's enough to say that we can use Vue in a live website on some of its parts only or use it to create a new site entirely managed by Vue (SPA).

Clone the [original repositoy from week 5](https://github.com/Conforcat-Frontend-PT-Jul/WEEK-5-lab-dom-ironhack-cart).

Add the Vue's CDN, then the `index.html` file.

`<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>`

Start a new Vue app in the `main.js` file:

```
new Vue({
    el: '#app'
})
```

Explain the template concept.

##### Step 2 - Directives and reactivity

Explain directives. What are they? Everything (on the HTML side) is done with directives.

**How to manipulate the content of the HTML elements?**

Explain `v-text` and `data()`.

    Use it on the item name to display it's name from the JS.
    Explain the mustache as a shortcut to `v-text`

Explain `v-html`.

    Use it on the item name as an example (then, can be removed)

Do the same with the rest of the fields except the input field.

    Replace the item name, price and total with Vue.js data.

Make emphasis, the content of the directives is JS interpretable code. Show operations can be done in the template.

    As an example, do some string concatenation, boolean expressions and mathematical expressions inside the mustache.

**How to manipulate the attributes of the HTML elements**

Explain the `v-bind` directive to modify attributes of the HTML elements.

    Use it on the input field to bind the `value` of the units. Make sure the variable contains some
    units (other than 0).

Explain the `v-bind` shortcut `:`.

**How to capture events**

Show `v-on` and `methods:`.

    Use it on the button to calculate the totals. Link it to a new method with a simple `console.log`
    to make sure it gets called.
    Notice the method will get the event by default as an argument.

**Reactivity**

Show reactivity. Explain how to access the data from the methods in Vue.js.

    Refactor the content of the funcion `calculate` to overwrite the total of the item (just for this item).

Explain the problem. If we change the number of units, it still calculates the total based on the initial number of units.

Explain two-way data bindings.

Show `@input`.

    Use it on the input field to call a new method that updates the item's units. Use the `event`
    object passed by Vue to get the value entered by the user.

Explain how to pass other variables to our methods (will be needed in the first bonus).

Show `v-model` as a shortcut to `:value @input`.

    Do it, and remove the now unsued method.

Show `v-if` and `v-show`.

    Only show the `calculate prices` button if the amount is greater than 0.

Pay attention to the DOM. With `v-if` the element will be removed from the DOM and the HTML. With `v-show` it simply uses a `display: none`. Explain when to use each one.

Show `v-else` and `v-else-if`.

    Add another button that simply has a message "Select some units" and the `v-else`. Notice how the
    button shows up and disappears as we input different values.
    Then add another button saying "thank you" and the `v-else-if`. Add a flag in the `data()` to store
    a boolean indicating if the operation has finished. Update the calculate prices method to set this
    variable to true. The button should have 3 states: when units is 0, it should show the "Select
    units" message, otherwise it should show the "calculate" button, and once this is clicked, it
    should show the "Thank you" button.

#### Iteration 2

Before proceeding into doing the actual iteration, explain and show how we can use objects in the data and interpolate them in the template.

    Refactor all the item variables into an object item with properties.

Show the same, but with lists.

    Refactor the code to work with a list of a single item.

    Then, add the new item and add it also to the template by accessing it directly (i.e. `items[1].name`, ...).

    Refactor the calculate method to loop through all the items int the list. Notice, it works.

Notice the problem, we can't know how many items there will be, we can't keep manually adding them to the HTML.

Explain the `v-for`. Explain `:key` briefly. Explain `index`.

    Refactor the code into using `v-for`.

Notice, everything works out of the box.

#### Iteration 3

Updating the overall total. They already know how to do it, ask them to guide you.

    Just add a new data() variable `total` and link it in the template. Then, refactor the calculate
    method to calculate the overall price and update that variable.

#### Iteration 4: BONUS

Removing an item. They should know how to, ask them.

    Create a new method, link it to the `@click` passing the item index (not the object). Hint: use splice.

#### Iteration 5: BONUS

Adding an item. They should know how to, ask them.

#### Iteration 6: VUE BONUS

Show the `@submit.prevent` modifier.

    Add a form tag. Make the calculate button a submit.

#### Iteration 7: VUE BONUS

Explain the problem. The user has to manually hit "Calculate" after each change to see the new total. If an item is removed, they also need to hit the button again. If they forget, they may get confused.

Show them the computed properties.

    Remove the calculate button, the `total` data() attribute and refactor the calculate method
    into a computed property (the same, but named total and returning the total). Now the calculation
    happens at every change in the data. Try removing an item when there was units selected and see
    the overall total change.

#### Iteration 8: VUE BONUS

Explain the problem. The data is now hard-coded in the app, but this usually will come from external sources. We can't be changing the code every time the data changes. Plus, this is a cart and should be different for each user, if we put the data in the code it will be the same for all users.

Explain the life-cycle hooks briefly. No need to mention them all, just that we can tap into various states of the component rendering process.

    Set the `items` from the data() to an empty list `[]`. Place them in a json file on the file
    system. Use `mounted()` to fetch the file and load the data into the `items` object.

### Session 2 (~50 minutes)

In this session we will understand what are components. Then, we will also see what are ESModules.

Explain Web Components as customized HTML elements.

Explain Web Components as a way to organize and reuse code. In this session we will only see them as
a way to orgnize the code and prevent it from being all in one single big file.

#### Step 1. Vue Components

Define the Ironhack Cart as a component and use it on the main page.

    Use `Vue.component('ironhack-cart', object)` and move all the Vue JS into that component.
    Copy all the HTML content into the `template:` key.

    Define a main app where the component will be rendered.

    Add the `components:` key to the app object.

Add a second cart and see how they are compeltely contained and do not interfere with each other. Doing this with vanilla JS/HTML/CSS means a lot more work.

### Step 2. Javascript Modules

Explain the problem.

    We want to remove the script tags in the HTML.

    When we load non-module script files, we are actually putting in the global scope all the variables
    and functions of that file (security risk).

Mention CommonJS, but ESModules is more modern and we will only see these.

Define the main script as a module in the HTML file.

    Use type="module" on the script tag.

    Try declaring a variable without let/const. (All modules use strict mode).

    Declare a variable in the module and then check the window object in the console.

> Everything inside a module is hidden from the global scope and can't be accessed from other scripts.

**How do we load other files, then?**

Import the funcions in the main file.

    Use `import {}` to import the function from strings.js

Notice it does not work. Export the function.

    Use `export` on the strings.js

Explain the {}. Import multiple functions from the same file.

Explain default exports (vs named imports).

    Import/export the default and compare to named imports

    Import combined default and named exports

Explain new problem (methods with the same name in different modules). Solutions:

    Rename exports (AS)

    Rename imports (AS)

    Namesped imports (asterisc)

Check the browser's console and notice all the JS files are being loaded separately. That is still not optimal.

Explain app bundling, minifying, obfuscating. Explain there are tools to do this.

> https://www.freecodecamp.org/news/modules-in-javascript/
>
> https://javascript.info/modules-intro

### Session 3 (~30 minutes)

Install Vue with a build setup.

`npm init vue@latest`

Pick Vue3 & Vite. No need for Pinia or Router, yet.

Explore `package.json`. Explain the main keys. What is devDependencies?

Explain `npm install`. Explore `node_modules`.

Explain `npm run dev`.

Explore the source code briefly.

Explain `npm run build`. Explore the `dist` folder. Run the dist folder in a live server.

### Session 4: LAB

Option A. Do the contact form in the mid-term project with Vue (using the CDN).

Option B. Do the Ironhack Cart.

## Day 2

### Session 1 (~120)

Explore the source code. Explain the things we have already seen. Don't rush into router, yet.

Explore the files and folders in the Vue3 build setup. Review what we have already seen on Session 1 in the new setup. Explain the differences (skip router and things we did not see).

    What are SFC?

    Explain data(), methods, computed, lifecycle hooks in the composition API.

    Explain ref and reactive. Explain RefImpl & value.

    Option API vs. Composition API. Differences, benefits.

    Scoped styles.

### Session 2: LAB

Using a build setup and SFC (should we prepare a basic Vue3 setup, clean of sample components?).

Option A. Set up a new project and create a general layout with 3 components (header, main and footer).

Option B. Redo the Week 2 lab about a recipe web app, using a component for each section.