<style>
#list-items-container{
    display: flex;
    flex-wrap: wrap;
    overflow-y: auto;
    /* width: 50%; */
/* margin-left: 50%; */
  }

#list-items-container .hed{
    margin: 0;
    padding: 0;
    display: none;
}

#list-item-10 .list-content{
    max-width: 31rem;

}

  img {
    width: 100%;
    height: 100%;

    object-fit: cover;
    position: absolute;

    /* width: 100%; */
    top: 0;
    left: 0;
  }

  .list-content{
    padding: 40px;
    max-width: 58rem;
    margin: 80px auto !important;
    color: #fff;
    background: rgba(0, 0, 0, 0.4); /* Black see-through */
    text-shadow: 2px 2px 8px #000;
    /* margin: 40px 30px;
     */
  }


  .list-item{
    font-size: 1.2em;
line-height: 1.5em;
width: 100%;
padding: 132px;
color: #000;
margin-top: 0;
min-height: 676px;
display: flex;
justify-content: center;
align-items: center;
  }
  /* .head {
    margin: 30px 40px 0 40px;
  } */

  .intro{
    margin: 40px 40px 0;
      padding-bottom: 30px;
      font-size: 1.2em;

  }

  /* h1 {
    font-size: 3.4em;
    font-family: Arial, Helvetica, sans-serif;
  } */

video{
  object-fit: cover;
  position: absolute; height: 500px;
  width: 100%;
  /* height: 100%; */
  top: 0;
  left: 0;
}
  .videoAdd{
    width:100%;
     height:100%;
     margin: 0;
  }

.list-title{
      font-family: trim-poster,sans-serif;
      font-weight: 600;
      font-size: 2.5em;
      line-height: 1.25em;
      margin: 10px 0;

  }

  .list-day{
    font-family: akkurat,sans-serif;
    font-weight: 600;
    font-size: 1.75rem;
    line-height: 1.35em;
    margin: 10px 0;

  }

.list-desc{
      /* font-family: Georgia, 'Times New Roman', Times, serif; */
      font-family: akkurat,sans-serif;
      font-size: 1.35rem;

  }
  /* .tail-content{
    height: 50px;
  } */

.list-item:last-child{
    /* margin-bottom: 80px; */
    border-bottom: none;
  }

  a{
    color: #ffd700;
  }

  /* .red-line {
  background:#FF4949;
  z-index:-1;
  width:5px;
  height:100%;
  position:absolute;
  left:15px;
}

.list-wrapper {
  position:relative;
  width: 100%;
}
.list-item-wrapper {
  margin-top:10px;
  position:relative;
}
.list-bullet {
  float:left;
  margin-right:20px;
  background:#FF4949;
  height:30px;
  width:30px;
  line-height:30px;
  border-radius:100px;
  font-weight:700;
  color:white;
  text-align:center;
}

.list-title {
    font-weight:700;
}
.list-text {
    font-weight:400;
} */

  /* .wrapper{
    padding: 0 40px;
  } */
  @media (max-width: 1250px) {
    .list-title{

          font-size: 1.9em;


      }

      .list-day{
          font-size: 1.45rem;

      }

    .list-desc{
          /* font-family: Georgia, 'Times New Roman', Times, serif; */
          font-family: akkurat,sans-serif;
          font-size: 1.15rem;

      }

    .list-content{
      padding: 20px;

      margin: 20px 30px;
    }

  }
  @media (max-width: 750px) {

    /* .intro{
      margin: 0;
      padding: 10px;
    } */
    .list-item:last-child{
        /* margin-bottom: 200px; */
        border-bottom: none;
      }

    .list-item{
      margin: 0;
      height: auto;
      /* margin: 40px 40px; */
      padding: 100px 10px;

/* padding: 20px 10px 50px; */
}

.videoAdd{
  width:100%;
  /* height: auto; */
   /* height:50%; */
   margin: 0;
}

.list-title{

    font-size: 1.7rem;

}

  .list-day{
      font-size: 1.2rem;
      line-height: 1.2em;
  }

.list-desc{
      /* font-family: Georgia, 'Times New Roman', Times, serif; */
font-size: 1.15rem;
line-height: 1.25em;

      /* font-size: 1.15rem; */

  }

  /* .tail-content{
    height: 300px;
  } */

  }


</style>

<script>
  import { onMount, onDestroy } from 'svelte';
  import inView from 'in-view';
  import { listItems} from './consts.js';
  import { activeListItem, activeMapItem } from './stores.js';
  import GraphicFooter from '../components/GraphicFooter.svelte'

  // Define the ref
  let listRef;

  onMount(async () => {
    // Set a nicer offset so it's not a hard cutoff
    inView.offset(100);

    window.addEventListener('scroll', function() {
      // Active list item is top-most fully-visible item
      const visibleListItems = Array.from(
        document.getElementsByClassName('list-item')
      ).map(inView.is);


      // If it's a new one, update active list item
      const topMostVisible = visibleListItems.indexOf(true);
      if (topMostVisible !== -1) {
        activeMapItem.set(topMostVisible);
      }

    });
  });

  // Update list scroll position when active list item is updated via map
  const unsubscribeActiveListItem = activeListItem.subscribe(
    newActiveListItem => {
      if (listRef) {
          listRef.scrollTop = document.getElementById(
          `list-item-${newActiveListItem}`
        ).offsetTop;
      }
    }
  );

  // Remove listener on unmount
  onDestroy(unsubscribeActiveListItem);
</script>
<div id="list-items-container" bind:this="{listRef}">

<div class = "hed"></div>

  {#each listItems as listItem, index}
  {#if listItem.id <= 10}

    <section class="list-item" id="list-item-{index}">

    {#if listItem.video === ""}
    <!-- <img src="{listItem.image}" alt="{listItem.name}"  class = "img-list"/> -->
    <!-- <img src="//news.northeastern.edu/interactive/2021/09/fresh-truck/images/fresh_truck_img_1_web.jpg" alt="{listItem.name}"  class = "img-list"/> -->
    <!-- <img srcset="//news.northeastern.edu/interactive/2021/09/fresh-truck/images/fresh_truck_img_1_0.5x_web.jpg 600w,
                //news.northeastern.edu/interactive/2021/09/fresh-truck/images/fresh_truck_img_1_0.75x_web.jpg 900w"
                sizes="(max-width: 750px) 600px,
                900px"
                src="//news.northeastern.edu/interactive/2021/09/fresh-truck/images/fresh_truck_img_1_web.jpg"
    alt="{listItem.name}"  class = "img-list"/> -->

    <img srcset="{listItem.image_mobile} 600w,
                {listItem.image_desktop} 901w"
                sizes="(max-width: 750px) 600px,
                901px"
                src="{listItem.image_original}"
    alt="{listItem.name}"  class = "img-list"/>
    <div class = "list-content">
    <div class = "list-title">{listItem.name}</div>
    <div class = "list-day">{listItem.day}</div>
      <div class = "list-desc">{listItem.description}</div>
      </div>
      {:else}
      <!-- <video class = "videoAdd" controls autoplay> -->
      <video class = "videoAdd" controls autoplay muted playsinline loop >

       <source src="{listItem.video}" type="video/mp4">
      </video>
      <div class = "list-content">
      <div class = "list-title">{listItem.name}</div>
      <div class = "list-day">{listItem.day}</div>
        <div class = "list-desc">{listItem.description}</div>
        </div>
       {/if}
    </section>
    {:else}
    <!-- <section class="list-item" id="list-item-text-{index}" >
    <div class="red-line"></div>
    <div class="list-bullet">1</div>

    <div class = "list-content">
    <div class = "list-title">{listItem.name}</div>
    <div class = "list-day">{listItem.day}</div>
      <div class = "list-desc">{listItem.description}</div>
      </div>
    </section> -->
    <!-- <section class="list-item" id="list-item-text-{index}" > -->

    <!-- <section class="list-item-wrapper" id="list-item-{index}"> -->
  <section class="list-item" id="list-item-{index}">
  <!-- <img src="{listItem.image_original}" alt=""  class = "img-list"/> -->
  <img srcset="{listItem.image_mobile} 600w,
              {listItem.image_desktop} 901w"
              sizes="(max-width: 750px) 600px,
              901px"
              src="{listItem.image_original}"
  alt="{listItem.name}"  class = "img-list"/>


        <div class="list-content">

        <div class = "list-desc">For more information on Fresh Truck and the Mobile Market route schedule, visit  <a href="https://www.aboutfresh.org/fresh-truck/"> www.aboutfresh.org/fresh-truck</a>.</div>

        </div>
    </section>

<!-- </section> -->
   {/if}
    {/each}


  <!-- <GraphicFooter
  	source={'<a href="https://www.aboutfresh.org/fresh-truck/">Fresh Truck Mobile Market</a>'}
  	credit={'Eunice/Northeastern University'}
  /> -->

  <!-- <div class="tail">
  <div class = "tail-content"></div>
    <i>
    This was made as part of a <a href="https://svelte.dev/">Svelte</a>

    </i>
  </div> -->
</div>
<!-- <div id="list-items" bind:this="{listRef}">
<div class="intro">

  <h1>Fresh Truck Roundtrip</h1>
  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
</div>

  {#each listItems as listItem, index}

    <div class="list-item" id="list-item-{index}">

    {#if listItem.video === ""}
    <img src="{listItem.image}" alt="{listItem.name}" />

    <h2>{listItem.name}</h2>
    <h3>{listItem.day}</h3>

      {@html listItem.description}
       {:else}
       <video width="100%" height="70%" controls>
        <source src="{listItem.video}" type="video/mp4">
       </video>
       <h2>{listItem.name}</h2>
       <h3>{listItem.day}</h3>

       {@html listItem.description}
       	{/if}
    </div>
  {/each}
  <div class="tail">
    <i>
      This was made as part of a <a href="https://svelte.dev/">Svelte</a>
      tutorial on <a href="https://dev.to/bryce/an-interactive-scrolling-map-list-in-svelte-34c3">dev.to</a>.
      View source on <a href="https://gitlab.com/brycedorn/svelte-reactive-map-list">GitLab</a>.
    </i>
  </div>
</div> -->
