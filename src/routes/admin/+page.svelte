<script>
  import {onMount} from 'svelte'

  let data = []
  let user = {}
  //  Function untuk hit api
  onMount(async()=>{
    const response = await fetch('json/data.json')
    const fetchUser = await fetch('json/user.json')
    data = await response.json()
    user = await fetchUser.json()
    
  })
</script>

<div class="container-fluid">
  <div class="row">
      <div class="col-lg-12">
        <h1 class="fw-semibold text-center">My Tech Blog</h1>

        {#each data as item}
            <h2 class="fw-semibold">{item.title}</h2> <span class="badge text-bg-secondary">{item.category}</span>
            <p class="fw-light">{item.content}</p>
            <img src="{item.thumbnail_url}" alt="" class="img-thumbnail w-25">
          <p class="fw-bold center">Author : {user.username}</p>
        {/each}
        
      </div>
  </div>
</div>