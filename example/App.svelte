<script>
  import { slide } from 'svelte/transition'
  import {
    Confirm
  } from '../src'

  let items = new Array(5)
    .fill(null)
    .map((value, index) => ({
      id: index,
      title: `Item ${index + 1}`
    }))

  function deleteItem (itemId) {
    items = items.filter(item => item.id !== itemId)
  }
</script>

<main>
  <div class="items">
    {#each items as item (item.id)}
      <div
        class="item"
        transition:slide
      >
        <span class="title">
          {item.title}
        </span>
        <Confirm
          confirmTitle="Delete"
          cancelTitle="Cancel"
          let:confirm="{confirmThis}"
        >
          <svg
            style="width:24px;height:24px"
            viewBox="0 0 24 24"
            class="delete-icon"
            on:click="{() => confirmThis(deleteItem, item.id)}"
          >
            <path
              fill="hsl(200, 40%, 20%)"
              d="M19,4H15.5L14.5,3H9.5L8.5,4H5V6H19M6,19A2,2 0 0,0 8,21H16A2,2 0 0,0 18,19V7H6V19Z"
            />
          </svg>
          <span slot="title">
            Delete this item?
          </span>
          <span slot="description">
            You won't be able to revert this!
          </span>
        </Confirm>
      </div>
    {/each}
  </div>
</main>

<style>
  main {
    max-width: 400px;
    width: calc(100% - 20px);
    margin: 0 auto;
  }

  .items {
    display: flex;
    flex-direction: column;
    background: #FFF;
    border-radius: 3px;
    margin-top: 50px;
    box-shadow: 0 2px 4px hsla(200, 80%, 10%, 20%)
  }

  .item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
  }

  .delete-icon {
    cursor: pointer;
    transition: all 0.3s ease-out;
  }

  .delete-icon:hover path {
    fill: hsl(200, 40%, 25%);
  }
</style>