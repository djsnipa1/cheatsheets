# Javascript Notes

$$ `.addEventListener`

I needed this because I wanted the callback function to be more complex than a line or two:

```javascript
const makeHideHandler = (element) => { // higher order function
  return () => {                // event handler function
	    element.hidden = true;    / action to perform
	};
};

hider.addEventListener('click', makeHideHandler(hider));
```
> However, the real strength of the higher order function approach becomes visible if you have more than one element that should hide the same (or other!) element(s). Consider the following:

Let's say, you have multiple buttons that, when pressed, should hide the same element. It's easy peas with `makeHideHandler`:

```javascript
// grab all "button" elements
const hideButtons = document.querySelectorAll('.hide-button');
// grab the element to hide
const elemToHide = document.querySelector('.hide-me');

// make the handler, pass in the element that should be hidden
const hideHandler = makeHideHandler(elemToHide);

// add listeners to the buttons
hideButtons.forEach((button) => {
  button.addEventListener('click', hideHandler);
});
```
Or to create buttons that hide themself after pressing:

```javascript
const hideButtons = document.querySelectorAll('.hide-button');
hideButtons.forEach((button) => {
  button.addEventListener('click', makeHideHandler(button)); // <-- pass in the button element
});
---

## Javascript DOM Manipulation

tutorial: https://m.youtube.com/watch?v=y17RuWkWdn8
`innerText` returns plain text
`textContent` returns all text with formrtting

use `append` and not appendChild
append can take multiple items and also strings

`innerHtml` will let you use html in strings

remove() deletes from DOM

.id or .title will give the attribute for example

setAttribute('id', 'newId')

removeAttribute('id')

.classList does class stuff
.classList.toggle toggles on and off

.style is for css styles
example
.style.backgroundColor = "red";
.style.display = "block";

