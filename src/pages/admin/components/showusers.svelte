<script>
    import { onMount } from 'svelte';
    import List from './userslist.svelte';
    let token;
    onMount(async () => {
      token = decodeURIComponent(document.cookie).split(';')[0].split('=')[1];
    });
  </script>
  {#if token}
    <List postsArray={token}/>
  {/if}