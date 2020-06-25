<style>
  /* unread message count */
  .badge {
    display: inline-block;
    position: absolute;
    top: 0;
    background-color: #4285f4;
    color: #d7e6fd;
    right: 0;
    border-radius: 9999px;
    font-size: 12px;
    min-width: 18px;
    line-height: 18px;
    min-height: 18px;
    text-align: center;
  }
  /* custom width for message popup */
  .messages {
    min-width: 400px;
  }
</style>

<script>
  // import the custom store
  import { center } from './notifications';
  // open-close state
  let show = false;

  const handleDismiss = message => {
    center.dismiss(message);

    // guard to close popup when there are no more messages
    if ($center.length === 0) {
      show = false;
    }
  };

  const handlePopup = () => {
    // don't show popup when no messages
    if ($center.length === 0) {
      show = false;
    } else {
      show = !show;
    }
  };

  const clearAll = () => {
    center.clear();
    // close popup
    show = false;
  };

  // limit the number of displayed messages to 5
  export let count = 5;

  // create a list of messages to display
  $: messages = $center.slice(0, count);
</script>

<button class="relative p-1" on:click={handlePopup}>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    width="24"
    height="24"
    viewBox="0 0 24 24"
    fill="none"
    stroke="currentColor"
    stroke-width="2"
    stroke-linecap="round"
    stroke-linejoin="round"
    class="w-6 h-6"
  >
    <path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9" />
    <path d="M13.73 21a2 2 0 0 1-3.46 0" />
  </svg>

  <!-- show number of messages or hide if zero -->
  {#if $center.length}
    <span class="badge">{$center.length}</span>
  {/if}

</button>

<!-- show only if there are messages -->
{#if show && $center.length}
  <!-- clicking anywhere on the page will close the popup -->
  <button
    tabindex="-1"
    class="fixed inset-0 w-full h-full cursor-default focus:outline-none"
    on:click|preventDefault={() => (show = false)}
  />

  <div
    class="absolute right-0 p-3 mt-1 text-gray-600 bg-white bg-gray-100 rounded
    shadow-md messages"
  >
    <ul class="space-y-3">
      <!-- loop through the message list -->
      {#each messages as message}
        <li class="p-3 border rounded">
          <p>{message}</p>
          <div class="mt-1">
            <!-- add dismiss handler -->
            <button
              class="px-2 text-sm text-blue-200 bg-blue-700 rounded-sm"
              on:click={() => handleDismiss(message)}
            >
              dismiss
            </button>
          </div>
        </li>
      {/each}
    </ul>
    <div class="flex justify-end mt-3">
      <!-- add clear all handler -->
      <button
        class="px-2 text-sm text-blue-200 bg-blue-700 rounded-sm"
        on:click={clearAll}
      >
        clear all
      </button>
    </div>
  </div>
{/if}
