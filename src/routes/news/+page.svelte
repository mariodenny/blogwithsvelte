<!--Next week by api-->
<script>
  import { onMount } from "svelte";
  import { get } from "svelte/store";

    const API_KEY ="d3c445383dfe48cc950fa190942d75af"
    const BASE_URL = "https://newsapi.org/v2/everything"

    let news = []
    async function getAllNews() {
        response = await fetch(`${BASE_URL}&apiKey=${API_KEY}`)
        news = await response.json()
        console.log(news);
    }

    onMount(async()=>{
        getAllNews()
    })
</script>

<div class="container mt-4">
    <h1>Page news</h1>
</div>