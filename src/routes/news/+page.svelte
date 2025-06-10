<!--Next week by api-->
<script>
    import {
        onMount
    } from "svelte";
    import {
        get
    } from "svelte/store";

    const API_KEY = "d3c445383dfe48cc950fa190942d75af"

    const categories = ["business", "entertainment", "general", "health", "science", "sports", "technology"]

    let data = []
    let news = []
    let topheadline = []
    let countryNews = []
    let categoryNews = {}
    let response
    let category = ""
    let totalResults = 0
    let bitcoinNews = {}

    let pageSize = 10;
    let currentPage = 1;
    let loading = false;


    async function getBtcNews() {
        response = await fetch(`https://newsapi.org/v2/everything?q=bitcoin&apiKey=${API_KEY}`)
        bitcoinNews = await response.json()
        console.log(`BTC News update : ${bitcoinNews}`);
        
    }

    async function getAllNews() {
        response = await fetch(`https://newsapi.org/v2/everything?q=indonesia&apiKey=${API_KEY}`)
        news = await response.json()
    }

    async function getTopHeadlineNews() {
        response = await fetch(`https://newsapi.org/v2/top-headlines?country=id&apiKey=${API_KEY}`)
        topheadline = await response.json()
    }

    async function getNewsCategory(category) {
        response = await fetch(`https://newsapi.org/v2/top-headlines?category=${category}&apiKey=${API_KEY}`)
        categoryNews = await response.json()
        console.log(categoryNews);
        
    }

    async function loadMoreNews(category){
        loading = true
        currentPage++
        const response = await fetch(`https://newsapi.org/v2/top-headlines?category=${category}&pageSize=${pageSize}&page=${currentPage}&apiKey=${API_KEY}`)
        const moreNews = await response.json()

        categoryNews[category].articles = [...categoryNews[category].articles, ...moreNews,articles]
        loading = false
    }
    onMount(async () => {
        getAllNews()
        getTopHeadlineNews()
        getNewsCategory()
        // categories.forEach(category => getNewsCategory(category,pageSize))
        getBtcNews()
    })
</script>

<div class="container-fluid mt-4">
    <div class="row mb-4">
        <div class="col-12 text-center">
            {#each categories as category}
                <button type="button" class="btn btn-success me-2 fw-bold" on:click={()=>getNewsCategory(category)}>#{category}</button>  
            {/each }
        </div>
    </div>
     <!--Buat categories button , tampilin news by category disini-->
    <div class="row">
        <div class="col-lg-12 col-md-6 col-sm-6">
            {#if categoryNews.totalResults > 0}
                <h5>Total Result : {categoryNews.totalResults}</h5>
                {#each categoryNews.articles as article}
                    <h2>{article.title}</h2>
                    <p>{article.description}</p>
                    <p>{article.content} <a href={article.url} target="_blank" class="btn btn-primary btn-sm">Read More</a></p>
                    
                {/each }
            {:else}
            <p class="text-center">No news available</p>
            <p class="text-center">{totalResults}</p>
            {/if}
        </div>
        <!-- <h1>Berita top headline disini</h1>
        {#each categories  as category}         
        <div class="col-lg-12 col-md-12">
            {#if categoryNews[category] && categoryNews[category].totalResults > 0}
                <h5>Total News : {categoryNews[category].totalResults}</h5>
                {#each categoryNews[category].articles as article}
                    <h2>{article.content}</h2>
                    <p>{article.description}</p>
                    <p>{article.author}</p>
                {/each}
            {#if categoryNews[category].totalResults > categoryNews[category].articles.length }
                <button class="btn btn-primary mt-3" disabled={loading} on:click={() => loadMoreNews(category)}>
                    {loading ? 'Loading...' : 'Load More'}
                </button>
                
            {/if }

            {:else}
                <p>Empty news</p>
            {/if}
        </div>
        {/each} -->
    </div>
    <h1>Berita btc disini</h1>
        <div class="row">
        <div class="col-lg-12 col-sm-12">
            {#if bitcoinNews.totalResults > 0}
                <h5>Total berita BTC : {bitcoinNews.totalResults}</h5>
                {#each bitcoinNews.articles as article}
                    <h1>{article.content}<span class="badge text-bg-primary">{article.author} - {article.source.name} </span></h1>
                    <p>{article.description}</p>
                {/each}
            {:else}
            <p>Berita BTC tidak ada</p>
            {/if}
        </div>
    </div>

</div>