# Modal

A modal in is a temporary overlay that appears on top of the main content of a webpage. 
It is used to present important information, prompt for input, or require the user to make a decision. 

Modals create a focused and isolated interaction, often with a darker background overlay, to draw attention and prevent interactions with the underlying page until the modal is dismissed. 

## Example

<div class="featured-demo">

```gjs live preview no-shadow
import { Modal, /* or Dialog (alias) */ } from 'ember-primitives';
import { on } from '@ember/modifier';
import { loremIpsum } from 'lorem-ipsum';

<template>
  <Modal as |m|>
    <button {{on 'click' m.open}}>Open Modal</button>

    <br><br>
    isOpen: {{m.isOpen}}

    <m.Dialog>
      <div>
        <header>
          <h2>Example Modal</h2>

          <button {{on 'click' m.close}}>Close</button>
        </header>

        <main>
          Modal content here
          <br>

         {{loremIpsum 1}}
        </main>
      </div>
    </m.Dialog>
  </Modal>


  <link rel="stylesheet" href="https://unpkg.com/open-props/easings.min.css"/>
  <link rel="stylesheet" href="https://unpkg.com/open-props/animations.min.css"/>
  <style>
    dialog {
      border-radius: 0.25rem;
      animation: var(--animation-slide-in-up), var(--animation-fade-in);
      animation-timing-function: var(--ease-out-5);
      animation-duration: 0.2s;
    }
    dialog > div {
      display: grid;
      gap: 1rem;
    }
    dialog::backdrop {
      backdrop-filter: blur(1px);
    }
    dialog header { 
      display: flex;
      justify-content: space-between;
    }
    dialog h2 {
      margin: 0;
    }

    dialog main {
      max-width: 300px;
    }
  </style>
</template>
```

</div>

Note that animations on `<dialog>` elements do not work within a [Shadow Dom](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM).

## Anatomy

```js 
import { Modal, Dialog /* alias */ } from 'ember-primitives';
```

or for non-tree-shaking environments:
```js 
import { Modal, Dialog /* alias */ } from 'ember-primitives/components/dialog';
```


```gjs 
import { Modal } from 'ember-primitives';

<template>
  <Modal as |m|>

    m.isOpen
    m.open
    m.close

    <m.Dialog ...attributes>
      this is just the HTMLDialogElement
    </m.Dialog>
  </Modal>
</template>
```

## API Reference

```gjs live no-shadow
import { ComponentSignature } from 'docs-app/docs-support';

<template>
  <ComponentSignature @module="components/dialog" @name="Signature" />
</template>
```

### State Attributes

There is no root element for this component, so there are no state attributes to use.
Since the this component uses the `<dialog>` element, it will still use the `open` attribute.

## Accessibility

Once the dialog is open, the browser will focus on the first button (in this case, it's our close button on the dialog header) or any button with the autofocus attribute within the dialog. When you close the dialog, the browser restores the focus on the button we used to open it.

### Keyboard Interactions

The dialog element handles ESC (escape) key events automatically, hence reducing the burdens and efforts required to provide an effortless experience for users while working with dialogs.

However, if you want to add an animation effect on _closing_ and opening dialog programmatically, note that you will lose this built-in feature support and have to implement the tab navigation focus yourself.


## References

- [MDN HTMLDialogElement](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dialog)
- [web.dev : Building a dialog component](https://web.dev/building-a-dialog-component/)
- [Exploring the HTML Dialog element](https://mayashavin.com/articles/build-a-dialog-with-dialog-element)[^a11y]
- [Open Props](https://open-props.style)[^animations]

<hr>

[^a11y]: The Accessibility text was copied from this blog. 
[^animations]: Animations in the examples are provided by Open Props 