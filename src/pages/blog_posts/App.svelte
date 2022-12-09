<script>
  import { onMount } from 'svelte';
  import axios from 'axios';
	import List from './components/List.svelte';
  
	let postsInfo=[];
	let postsInfo2=[];
  onMount(async () => {
    
    const { data2 } = await axios.get('https://sponsors.vuejs.org/data.json');
    postsInfo2 = data2;
  });
  
</script>

<List postsArray={postsInfo}/>