<script>
  import { onMount } from 'svelte';
  import axios from 'axios';
	import List from './components/List.svelte';
  
	let postsInfo=[];
  onMount(async () => {
    const { data } = await axios.get('http://54.157.69.5:5678/api/show/post');
    postsInfo = data.blogposts;
  });
  
</script>
<List postsArray={postsInfo}/>