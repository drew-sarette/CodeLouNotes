# Web Components
Regular elements have default styles (consider h1, buttons), and even methods(button behaviour). Custom web components are just a specially designed html tag, in which you specify its properties and methods in an ES6 class. That class can extend HTMLElement class, or a specific element's class like HTMLHeadElement. 
A few things to note:
- the custom element's name must include a hyphen. That avoids conflict with regular elements.
- the file is linked in a script tag, without the defer attribute. It must be run before the element is added to the html.

## Shadow DOM
The shadow DOM API allows you to attach a hidden, second DOM tree to any node in the light DOM. The shadow root is the root element of the shadow dom. This allows you to encapsulate styles and functionality in your custom components, without them spilling out to the rest of the page. 

## Basic code outline
`
class ClassName extends HTMLElement {
    constructor() {
        //Super is always called first to include the parent class.
        super();
        //the shadow root is attached to the custom element. 
        //attachShadow() takes a settings object, either open or closed.
        //Open means query selectors can see into the custom component, closed means they can't. Closed is the recommended option, but it is not always supported.
        const shadowRoot = this.attachShadow({ mode: "closed" });
        //You can then create whatever you want and append it to the shadow root.
        const div = document.createElement("div");
        div.textContent = "whatever";
        shadowRoot.apend(div);  
    }
}
// After the class, you must register the new element:
document.customElements.define("class-name", ClassName);
`

## Using Templates
Templates provide a better way to visualize and write the inner content of the custom element.
`
const template = document.createElement("template");
template.innerHTML = `
   <!-- whatever html you want here! -->
    <div>
        <!-- more html -->
    </div>
`;

class ClassName extends HTMLElement {
    constructor() {
        super();
        const shadowRoot = this.attachShadow({ mode: "open" });
        //You must pass true to cloneNode to get everything contained within your template.
        const clone = template.content.cloneNode(true);
        shadowRoot.appendChild(clone);
    }
}
`

## Using Slots with Templates
When you actually create a custom element, you can insert variable content into your template using slots. The HTML:
`
<class-name>
    <h1 slot="slot1">specific content for the page</h1>
<\class-name>
`
the JS: 
`
const template = document.createElement("template");
template.innerHTML = `
   <!-- whatever html you want here! -->
    <div class="custom-h1-container">
        <slot name="slot1">  
    </div>
`;

class ClassName .....
`

With this setup, an h1 with "specific content for the page" will appear in the custom element.

# Styling custom components
Certain, but not all, styles will cascade from the page into a custom element. Things such as font-family, color, font-size etc... that relate to the text will cascade in. Others may not.

To style just the component, you can create a style tag inside the template, and those styles will not affect anything else on the page because they are encapsulated in the shadow DOM.

`
template.innerHTML = `
    <style>
      div {
        <!-- rules here -->
      }

      :host {
        <!-- these styles for the shadow root. The default is display: inline, so you will not see any styles you put here unless you change that. The content you see is spilling out of the shadow root. -->
        display: block;
        background: lilac;
      }

      :host(class-name) {
        <!-- these styles only apply if the host is a <class-name> element -->
      }

      :host-context(main) {
        <!-- these styles only apply if the host is inside a <main> -->
      }

      ::slotted(img) {
        <!-- style any slotted image. These styles are applied when the element is created, so they will be overwritten by anything in the regular css files. May need to use !important here if it is a text style. -->
        ::part() {
            <!-- part doesnt go here, but in the main css file. that way a part of the component with part="thing" can be styled externally by using ::part(thing) -->
        }
      }
    </style>
    <div>
        <button class="decrement"><img src="img/decrement.png"></button>
        <slot name="icon"></slot>
        <button class="increment"><img src="img/increment.png"></button>
    </div>`;
`

# Attributes and Properties
You can allow your element to have custom attributes using the static method get observedAttributes();
`
class FoodGroup extends HTMLElement {
  constructor() {
    super();
    const shadowRoot = this.attachShadow({ mode: "open" });
    const clone = template.content.cloneNode(true);
    shadowRoot.appendChild(clone);
  }

  static get observedAttributes() {
    return ["counts", "step", "current", "goal"]
  }
`

