<script>
  import { onMount } from 'svelte';
  import axios from 'axios';
	import List from './components/List.svelte';
  
	let postsInfo=[];
  onMount(async () => {
    const options = {method: 'GET', url: 'https://191.101.1.221:5678/api/show/post'};
  axios.request(options).then(function (response) {
    postsInfo = response.data.blogposts;
  }).catch(function (error) {
    console.error(error);
  });
  });
  
</script>
<List postsArray={postsInfo}/>