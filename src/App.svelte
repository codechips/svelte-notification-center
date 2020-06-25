<script>
  // Main stylesheet. Snowpack will inject it in the head tag
  import './main.css';
  import Messages from './Messages.svelte';
  import { onMount } from 'svelte';
  import { center } from './notifications';
  import AddMessage from './AddMessage.svelte';

  // seed out notification store on component mount
  onMount(() => {
    center.init([
      'Suspicious login on your server less then a minute ago',
      'Successful login attempt by @johndoe',
      'Successful login attempt by @amy',
      'Suspicious login on your server 7 min',
      'Suspicious login on your server 11 min ago',
      'Successful login attempt by @horace',
      'Suspicious login on your server 14 min ago',
      'Successful login attempt by @jack'
    ]);
  });
</script>

<div class="container flex flex-col max-w-4xl min-h-screen mx-auto">
  <!-- top menu -->
  <header
    class="flex items-center justify-between px-5 py-3 text-gray-100 bg-gray-800"
  >
    <h1 class="text-2xl">Hooli</h1>
    <nav class="relative">
      <Messages count="3" />
    </nav>
  </header>

  <div class="flex-grow px-5 py-3 bg-gray-200">
    <AddMessage />
  </div>

</div>
