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

  .img-list{
    max-width: 100%;
  }


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



window.onresize = displayWindowSize;
window.onload = displayWindowSize;
function displayWindowSize() {
    let myWidth = window.innerWidth;
    // let  myHeight = window.innerHeight;
    // your size calculation code here
    // document.getElementById("interactive").innerHTML = myWidth + "x" + myHeight;


// console.log(myWidth)
    if(myWidth > 750){
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
    }
    else{
        window.removeEventListener('scroll', function() {
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
    }
    };

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

    <picture>
     <!-- load webp in different sizes if browser supports it -->
      <source type = "image/webp" media="(max-width: 750px)" srcset="{listItem.image_mobile}">
      <source type = "image/webp" media="(min-width: 751px)" srcset="{listItem.image_desktop}">
      <!-- <source media="(min-width: 901px)" srcset="{listItem.image_original}"> -->

<!-- load jpg in different sizes if browser doesn't support webp -->
<source type = "image/jpeg" media="(max-width: 750px)" srcset="{listItem.image_mobile_jpg}">
<source type = "image/jpeg" media="(min-width: 751px)" srcset="{listItem.image_desktop_jpg}">

<!-- fallback in different sizes, as well as regular src. -->
<img srcset="{listItem.image_mobile_jpg} 600w,
            {listItem.image_desktop_jpg} 901w"
            sizes="(max-width: 750px) 600px,
            901px"
            src="{listItem.image_original_jpg}"
alt="{listItem.name}"  class = "img-list"/>
        <!-- <img src="{listItem.image_desktop}" alt="{listItem.name}" class = "img-list"> -->
    </picture>
    <!-- <img srcset="{listItem.image_mobile} 600w,
                {listItem.image_desktop} 901w"
                sizes="(max-width: 750px) 600px,
                901px"
                src="{listItem.image_original}"
    alt="{listItem.name}"  class = "img-list"/> -->
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

  <section class="list-item" id="list-item-{index}">
  <!-- <img src="{listItem.image_original}" alt=""  class = "img-list"/> -->
  <!-- <img srcset="{listItem.image_mobile} 600w,
              {listItem.image_desktop} 901w"
              sizes="(max-width: 750px) 600px,
              901px"
              src="{listItem.image_original}"
  alt="{listItem.name}"  class = "img-list"/> -->
  <picture>
   <!-- load webp in different sizes if browser supports it -->
    <source type = "image/webp" media="(max-width: 750px)" srcset="{listItem.image_mobile}">
    <source type = "image/webp" media="(min-width: 751px)" srcset="{listItem.image_desktop}">
    <!-- <source media="(min-width: 901px)" srcset="{listItem.image_original}"> -->

<!-- load jpg in different sizes if browser doesn't support webp -->
<source type = "image/jpeg" media="(max-width: 750px)" srcset="{listItem.image_mobile_jpg}">
<source type = "image/jpeg" media="(min-width: 751px)" srcset="{listItem.image_desktop_jpg}">

<!-- fallback in different sizes, as well as regular src. -->
<img srcset="{listItem.image_mobile_jpg} 600w,
          {listItem.image_desktop_jpg} 901w"
          sizes="(max-width: 750px) 600px,
          901px"
          src="{listItem.image_original_jpg}"
alt="{listItem.name}"  class = "img-list"/>
      <!-- <img src="{listItem.image_desktop}" alt="{listItem.name}" class = "img-list"> -->
  </picture>

        <div class="list-content">

        <div class = "list-desc">For more information on Fresh Truck and the Mobile Market route schedule, visit  <a href="https://www.aboutfresh.org/fresh-truck/"> www.aboutfresh.org/fresh-truck</a>.</div>

        </div>
    </section>

<!-- </section> -->
   {/if}
    {/each}



</div>
