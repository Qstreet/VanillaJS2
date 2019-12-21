# VanillaJS Academy Notes

; mdjs
; mdl

<h2>CSS Selectors</h2>
<ul>
<p><a href="https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors">MDN Selectors Ref</a></li>
<li><pre>var elemCarrots = document.querySelector('[data-snack="carrots"]');</pre></li>
</ul>

<h2>NodeList and .childNodes</h2>
<p>NodeList objects are collections of nodes, usually returned by properties such as Node.childNodes and methods such as document.querySelectorAll().</p>
<pre>nodeList.length</pre>
<p>querySelector()` and `querySelectorAll()</p>
<pre>element = document.querySelector(selectors);</pre>
<pre>elementList = parentNode.querySelectorAll("div.highlighted > p, li[data-active='1']");</pre>
if empty returns null and empty NodeList

<h2>Regex</h2>
<p>Count words. Discard blanks</p>
<pre>var words = text.value.split(/[\n\r\s]+/g).filter(function (word) {
return word.length > 0;
});
</pre>

<h2>Fetch</h2>
<p>Notes here</p>
<pre>
fetch('https://jsonplaceholder.typicode.com/postses')
.then(function (response) {
if (response.ok) {
return response.json();
} else {
return Promise.reject(response);
}
}).then(function (data) {
}).catch(function (err) {
console.warn('Something went wrong.', err);
});
</pre>

`Array.forEach()` and NodeLists

```javascript
var sandwiches = Array.prototype.slice.call(
  document.querySelectorAll(".sandwiches")
);
sandwiches.forEach(function(sandwich, index) {
  console.log(sandwich.textContent);
});
```

`matches()` _polyfill_

method checks to see if the Element would be selected by the provided selectorString -- ie checks if the element "is" the selector.

```javascript
function clickHandler(event) {
  if (!event.target.matches("#show-password")) return;
  event.target.checked
    ? passwordElem.setAttribute("type", "text")
    : passwordElem.setAttribute("type", "password");
}
```

`closest()`
closest goes up from the element and checks each of parents. If it matches the selector, then the search stops, and the ancestor is returned.

`forEach()` only way to exit loop is with return

```javascript
sandwiches.forEach(function(sandwich, index) {
  if (sandwich === "ham") return;
});
```

`getAttribute()`

`event.target.getAttribute('data-pw-toggle');`

## Event Handlers

`input`

event listener to the text element. Fires every time the value of the textarea element changes. Either by keyboard typing or cute and paste.

`charCount.textContent = text.value.length;`

<h2>Polyfill</h2>
<pre>https://polyfill.io/v3/polyfill.min.js?features=default%2Cfetch</pre>

---

## D1 Project: Toggle Password Visibility

```html
<body>
  <form>
    <div>
      <label for="username">Username</label>
      <input type="text" name="username" id="username" />
    </div>

    <div>
      <label for="password">Password</label>
      <input type="password" name="password" id="password" />
    </div>

    <div>
      <label for="show-password">
        <input type="checkbox" name="show-passwords" id="show-password" /> Show
        password
      </label>
    </div>

    <p>
      <button type="submit">Log In</button>
    </p>
  </form>

  <script>
    (function() {
      "use strict";

      var passwordElem = document.querySelector("#password");
      var inputElems = document.querySelectorAll('input[type="checkbox"]');

      /**
       * Clear all checkboxes on refresh. Especially Firefox
       */
      Array.prototype.slice.call(inputElems).forEach(function(item, idx) {
        item.checked = false;
      });

      function clickHandler(event) {
        if (!event.target.matches("#show-password")) return;
        event.target.checked
          ? passwordElem.setAttribute("type", "text")
          : passwordElem.setAttribute("type", "password");
      }

      document.addEventListener("click", clickHandler, false);

      var sandwiches = Array.prototype.slice.call(
        document.querySelectorAll(".sandwiches")
      );
      sandwiches.forEach(function(sandwich, index) {});
    })();
  </script>
</body>
```

---

## D3 Project: Toggling multiple password fields

by adding `data-pw-toggle="#password"` to each input checkbox elem I have a common target to apply to.

remember you can have multiple css selectors in `querySelectorAll('.myClass, #myId')`

---

## D7 Adding text to an element

`anyObject.constructor.name` // _Array, Number, String, Object, Boolean_

`document.body instanceof HTMLBodyElement`; // _true_

## innerHTML

The innerHTML property is only valid for **element** nodes.

Other node types, such as text nodes, have their counterpart: `nodeValue` and `data` properties. These two are almost the same so we use `data` as it is shorter

**Beware:** “innerHTML+=” does a full overwrite

`elem.innerHTML +=` removes all content and re-writes. All images, etc are reloaded fields are cleared and mouse selected text will unselect.

## textContent

The textContent provides access to the text inside the element: only text, minus all `<tags>`.

## value

the value for `<input>, <select>, <textarea>` (HTMLInputElement, HTMLSelectElement…)

## hidden and display:none

When set to true, does the same as CSS display:none.
