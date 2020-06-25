<script>
  import { center } from './notifications';

  let value = '';

  const addMessage = () => {
    if (!value) return;

    center.add(value);
    value = '';
  };
</script>

<h2 class="text-2xl font-medium">Add new message</h2>
<form class="mt-3" on:submit|preventDefault={addMessage}>
  <input
    type="text"
    class="p-2 w-1/2"
    bind:value
    placeholder="Enter your message"
  />
  <button class="px-5 py-2 text-gray-200 bg-gray-700">new message</button>
</form>
