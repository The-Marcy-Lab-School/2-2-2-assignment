# 2.2.2 Assignment - Forms

- [2.2.2 Assignment - Forms](#222-assignment---forms)
  - [Before You Start](#before-you-start)
- [Short answers](#short-answers)
- [Question 1 - Setting up the basic page](#question-1---setting-up-the-basic-page)
- [Question 2 - Setting up our form as a landmark](#question-2---setting-up-our-form-as-a-landmark)
- [Setting up the HTML of the form](#setting-up-the-html-of-the-form)
- [Question 3 - Adding username input and label](#question-3---adding-username-input-and-label)
  - [Lowdown on Labels](#lowdown-on-labels)
  - [Back to the question](#back-to-the-question)
- [Question 4 - Adding a fieldset and legend](#question-4---adding-a-fieldset-and-legend)
- [Question 5 - Adding our radio group](#question-5---adding-our-radio-group)
- [Question 6 - Adding a drop down](#question-6---adding-a-drop-down)
- [Question 7 - Adding a checkbox](#question-7---adding-a-checkbox)
- [Question 8 - submit button](#question-8---submit-button)
- [Part 2 - The submit event](#part-2---the-submit-event)
- [Question 9 - Adding a listener to prevent the default behavior](#question-9---adding-a-listener-to-prevent-the-default-behavior)
- [Question 10 - Getting our values](#question-10---getting-our-values)
- [Question 11 - Resetting our form](#question-11---resetting-our-form)
- [Wrap up](#wrap-up)

## Before You Start
Here it is, building a full page and form from scratch! Remember, there are a *lot* of specifics here with attributes and text content, *be careful*. When all else fails, check the tests to see exactly what it's expecting and then do that. No extra trailing or leading spaces and watch our for colons in labels! We never *try* to add mistakes in the README, but as always if the tests say one thing, and the README says another, **do what the test is asking for.**

# Short answers
Don't forget to do them! The cover some important things about forms.

# Question 1 - Setting up the basic page
So as you can see, there's an empty `index.html` and an empty `index.js`.
Here's everything you have to do:
- Add a `head` tag with a `title` tag
- The `title` of your page should be `Forms Practice`
- Add a `body` tag and a `main` tag inside of it
  - There's no `header` or `footer` so all subsequent work will be inside of `main`
- Add an `h1` tag with the text `Forms Practice`
- Add a blank `form` with an `id` of `new-user-form`
- Link your blank js file to your `index.html`

Now here's a `section` you can just copy directly (this assignment is just about forms after all). Since we aren't hitting a server with our form, we'll want to render the results on the page. Copy this html snippet as the last child of `main`.

```html
<section id="results" aria-labelledby="results-heading">
  <h2 id="results-heading">Results</h2>
  <p>Username: <span id="results-username"></span></p>
  <p>Coding level: <span id="results-coding-level"></span></p>
  <p>Location: <span id="results-location"></span></p>
  <p>Did you like this assignment? <span id="results-did-like-assignment"></span></p>
</section>
```

Copy it exactly, the tests are going to be using those spans to check the form submissions! You will know that you did everything right if the first test in `from-scratch.spec.js` passes.

By the way, if you want a *little* css just so your form doesn't look like hot garbage, you can just add this `style` tag to your `head` tag:

```html
<style>
  select, fieldset { display: block; margin: 1rem 0; }
  button { display: block; margin: 1rem auto; }
  form { width: 19rem; padding: 1rem; border: 0.1rem solid black; }
</style>
```

# Question 2 - Setting up our form as a landmark
Forms are important (or should be) to our page, so we need to tell assistive technologies that's the case! We want to make our form a proper "landmark." Don't worry too much about what that means, the good thing is that it's super easy to do!

- Add an `h2` tag to the `form`
- Give it an id of `form-heading`
- Give it a text content of `Create A New User`

Ok, that's going to help our sighted users. In general giving your form a heading just helps clarify what it does. But what about our screen reader users? To officially make the form a landmark we need to give it an "ARIA" label attribute, either `aria-label` or `aria-labelledby` (note the lowercase "by"). `aria-label` lets us label a form *without* using a visible heading. But since we have our `h2`, let's use that! We'll use `aria-labelledby` and give it the `id` of our `h2` tag.

Congratulations, your form is now more accessible than like 70% of the forms on the internet! *Killing it!*

# Setting up the HTML of the form
In order to fully understand how to create a form, we ask that you code it by hand in the html (so it's easy to instantly grade and see what you're doing). Once our form is fully built out and all the pure html tests are passing, then we'll worry about submission `JS` logic.

LET'S DO THIS!

# Question 3 - Adding username input and label
We nee to add our first input and label. But first a *quick* aside on labels.

## Lowdown on Labels
Labels are crucial for form inputs, as they make it easier to do things like click radio buttons (instead of only clicking the input, you can click the associated label), but it also tells screen readers what the heck they're looking at. To associate a label to an input you have 2 options, either nesting:

```html
<label>
  Username
  <input type="text" name="username" />
</label>
```

Or with the `for` attribute:

```html
<label for="username-input">Username</label>
<input id="username-input" type="text" name='username' />
```

Both are valid, but the `for` version, where you feed in the `id` of the associated input, is easier to test and a little better for accessibility. So we'll be using that one. On your real life forms you'll probably put the `label` and `input` into a `div` for styling, but we don't care about that here, **don't use any `div`s on this assignment it'll mess up the tests.**

And while `placeholders` are nice, they are no substitute for a label!

## Back to the question
Now that we know what we're doing, create the following:
- A `label` with a
  - `for` attribute of `username`
  - text content of `Username:` (no spaces!)
- An `input` with a:
  - `type` of `text`
  - `id` of `username`
  - `name` of `username`
  - `placeholder` of `Add your username` (no spaces!)

It's ok that our `id` and `name` match, but that won't always be the case! Also, note that order matters, if `label` comes after `input` it will render that way.

Fun fact, if we wanted a default value for our text input (not a `placeholder`), the we could add one by using the `value` attribute. But in this case we don't, so don't add a `value` to your input, it'll break the tests.

# Question 4 - Adding a fieldset and legend
Alright, you may not have seen these tags before, but we need a `fieldset` and `legend` to group our radio buttons together. `fieldset` is like a semantic `div`, it's useful for grouping similar elements together on a form. `legend` is like a label for all the inputs in the `fieldset` at once. `fieldset`s can be used for other inputs than radio buttons, but it's by far the most common use case. Here's an [article that shows how to build a radio group with a fieldset](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio)

For this question, lets's just focus on building the `fieldset` and `legend`
- inside your form create a `fieldset` tag (no need for an id here, it's the only one)
- inside your `fieldset` create a `legend` with text of `Coding Level`

That's it! Now let's add the radio buttons.

# Question 5 - Adding our radio group
Radio buttons are good when there's only a few options to choose from, it prevents things like spelling errors by users. Here we have 2 options: "Beginner" and "Proficient". We could add more, but it's tedious to do this by hand in HTML, so 2 is good enough. **Remember, you can only choose one input per group, and the way that works is that each radio input has the same `name`.** The name should be camelCase because we're using it with our JS. Don't forget to always add labels to your radio buttons!

- Our radiogroup has a `name` of `codingLevel`.
- Our first radio button should have:
  - a `type` of `radio` (That's important!!)
  - a `value` of `beginner`
  - an `id` of `beginner`
- Our first `label` should have:
  - a `for` attribute of `beginner`
  - text content of `Beginner`

- Our second radio button should have:
  - a `type` of `radio`
  - a `value` of `proficient`
  - an `id` of `proficient`
- Our second `label` should have:
  - a `for` attribute of `proficient`
  - text content of `Proficient`

Now, one last piece. By default, none of the buttons will be checked. Sometimes you want that if the information is optional. But let's give our form a default value by adding a `checked` attribute to our "beginner" radio `input`. It's just `checked` you don't have to make it equal anything:

```html
  <input type="radio" checked />
```

That's also how you would default a checkbox as well! Anyway, to check that you made your inputs correctly, click on them and make sure that only one input can be selected at a time. Then click the labels to ensure you associated them correctly as well. Clicking a label should check its input.

# Question 6 - Adding a drop down
Now, radio buttons are good to visually and quickly display a few options. But once you get past about 4, it's time to think about using a dropdown. Dropdowns are good when you want to limit the options to a predetermined set, but there are a *lot* of options. Here we're only using 3 options, but that's because we're hand coding and it's *super* tedious. Almost always in the real world you'll use JS to assemble all your options.

[Check out this `W3 schools` tutorial on select tags](https://www.w3schools.com/tags/tag_select.asp). Notice that the `label` tag goes outside, the `name` attribute goes on the `select` tag, and each nested option has the `value`.

Now that you know how to build one, let's do it!
- First, we need a `label` tag with:
  - a `for` attribute of `location`
  - text content of `Location:` (no space!)
- Then we need a `select` tag with:
  - a `name` attribute of `location`
  - an `id` attribute of `location`
- Then we need 3 `option` tags IN THIS EXACT ORDER
  - First `option` has a `value` of `brooklyn` and text of `Brooklyn`
  - Second `option` has a `value` of `other borough` and text of `Other Borough`
  - Third `option` has a `value` of `out of state` and text of `Out Of State`

The order matters. The first option will essentially be the default value of the select, and then when the drop down opens it will render the options in the same order as they are in the dom. That's almost always important as you'll want to list your options alphabetically or by popularity or something.

Seriously, make sure the order matches or the tests will fail.

# Question 7 - Adding a checkbox
Last piece of data we want to collect is a boolean, so a checkbox is perfect! Checkboxes are good for either unrelated booleans, or if you have a bunch of options that a user can select 1 or more of. Basically to decide if you want radio buttons or checkboxes, just ask yourself how many options they can pick. If it's 0-1, use radio buttons, if it's 0-many, use checkboxes.

Check out the [W3 schools tutorial on checkboxes](https://www.w3schools.com/tags/att_input_type_checkbox.asp)

Alright, lets add our own
- Add the `input` with:
  - A `type` of `checkbox`
  - An `id` of `did-like-assignment`
  - A `name` of `didLikeAssignment`
- Add a label with:
  - A `for` attribute of `did-like-assignment`
  - Text content of `Did you enjoy this assignment?`

By default, our checkboxes start off unchecked, and that's fine for us.

# Question 8 - submit button
Finally, *finally*, let's add a submit button. By default all `buttons` have a `type='submit'`, so since that's actually what we want, we don't need any attributes for this button. Just add a `button` tag with text content of `Submit`. This is the only button on the form, so no need for an `id`. You'll almost never need an `id` for the submit button because you'll never need to select it. Our form event `submit` fires on click automatically, no need to listen for a `click` on that *specific* button.

Fun fact: if you wanted a button that *did not* submit, then you would need a type of `button` and then you would need to add an event listener to it to do something. But we don't need that here. And a `type` of `reset` would clear out the form. We will do that later, but not with a button!

# Part 2 - The submit event
OK so all your HTML-only tests should be passing at this point. If they are, then you can move on to actually writing some `JS` to handle our submission. But I want to make sure you can grab the information from the form easily. You do not need query selectors if you built your form right!

You can either just grab each input from the form by its name:

```js
const form = e.target;
console.log("The actual input element (or node list if it's a radio group)", form.username)
console.log('The final computed value', form.username.value)
```

Of course you can destructure, but don't forget the difference between the element and the value. This is really nice because using the input name and value saves you from having to check things like `checked` existing.

The other option that works well is converting your data into an object using [the FormData API](https://developer.mozilla.org/en-US/docs/Web/API/FormData). FormData does a *lot* more than this, but it's honestly all we need right now.

```js
const formData = new FormData(e.target);
const { username } = Object.fromEntries(formData);

console.log('The final computed value', username)
```

If you don't know what [`Object.fromEntries`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/fromEntries) does it basically just takes a structure like this:

```js
[['username', 'tom'], ['codingLevel', 'beginner']]
```
And converts it into this:

```js
{ username: 'tom', codingLevel: 'beginner' }
```

Oh, one *last* little gotcha: checkboxes. With `FormData`, if a checkbox is clicked, it's value will be `on`. If it isn't checked, then the name and value simply won't be in the object. So think about how you might convert that into a boolean!

Alright, now you're off to the races!

# Question 9 - Adding a listener to prevent the default behavior
In `index.js` attach a `submit` event listener to the form and make sure to prevent the default behavior. If you don't know how to do that, check out the [MDN docs on preventing default behavior](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault). Remember, the default behavior of the form is to reload the page (we didn't provide an `action` attribute, so there's nowhere but the current page to navigate, hence the reload), and we don't want that!

# Question 10 - Getting our values
Remember those `spans` from the opening? You need to take the data on form submission and then update the text content of those spans with the `value` of the inputs. The only exception is the checkbox. If the checkbox value is `on` that means it's clicked, so you should set the text content of that span to `yes`, otherwise set it to `no`.

The text content is the `value` directly from the forms other than that, so just the lowercase `value`s that you added, not the formatted labels or text contents.

# Question 11 - Resetting our form
After we submit our form, let's clear it! If you don't know how to do that in `JS`, [check out the reset method on forms](https://www.w3schools.com/jsref/met_form_reset.asp). Remember, clear the form *after* you get all the data you need from it!

# Wrap up
Whew! That's an exhaustive little run through. But if you can do all this, you'll be able to create pretty much any form you need by just using different inputs. Great job!
