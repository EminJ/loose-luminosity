<script>
  import { onMount } from 'svelte';
  import axios from 'axios';
	import List from './components/List.svelte';
  
	let postsInfo=[];
  onMount(async () => {
    const { data } = await axios.get('http://3.87.32.105:5678/api/show/post');
    postsInfo = data.blogposts;
  });
  
</script>
<List postsArray={postsInfo}/>