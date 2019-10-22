# svelte-confirm ([demo](https://svelte.dev/repl/56c729e10a1e4348809367eda9bdc0d3?version=3.12.1))

A reusable solution for showing confirm dialogs in Svelte.

So if you have a button that calls some function, you can wrap it with the `<Confirm/>` component and it will show the confirm dialog before proceeding.

## Installation

```bash
npm install -S svelte-confirm
```

## Usage

```html
<script>
  import { Confirm } from 'svelte-confirm'

  function deleteItem (itemId) {
    // ...
  }
</script>

<Confirm
  let:confirm="{confirmThis}"
>
  <button
    on:click="{() => confirmThis(deleteItem, item.id)}"
  >
    Delete
  </button>
</Confirm>
```

As shown in the example, instead of calling the `deleteItem` function directly, we pass it to `confirmThis`. The first argument is the function you want to call if the user clicks "Confirm". All arguments after it are the arguments you want to pass to the `deleteItem` function. So if without confirmation your function call looks like this: `doSomething(arg1, arg2, arg3, ...)`, it becomes like this with confirmation: `confirmThis(doSomething, arg1, arg2, arg3, ...)`.

## `confirmTitle` and `cancelTitle` props

```html
<Confirm
  confirmTitle="Delete"
  cancelTitle="Cancel"
  let:confirm="{confirmThis}"
>
  ...
</Confirm>
```

The `confirmTitle` prop is used to change the text inside the confirm button. The default value is "Confirm".

The `cancelTitle` prop is used to change the text inside the cancel button. The default value is "Cancel".

## `title` and `description` slots

You can change the title and the description of the confirm dialog using the `title` and `description` slots.

```html
<Confirm
  confirmTitle="Delete"
  cancelTitle="Cancel"
  let:confirm="{confirmThis}"
>

  <button
    on:click="{() => confirmThis(deleteItem, item.id)}"
  >
    Delete
  </button>

  <span slot="title">
    Delete this item?
  </span>
  <span slot="description">
    You won't be able to revert this!
  </span>
</Confirm>
```

## `themeColor` prop

```html
<Confirm
  themeColor="250"
  let:confirm="{confirmThis}"
>
  ...
</Confirm>
```

This prop specifies the hue value used for the dialog theme color. The default value is `200`.

## License

[MIT](http://opensource.org/licenses/MIT)