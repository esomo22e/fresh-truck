<script>
	import { onMount } from 'svelte';
	import GraphicTitle from './components/GraphicTitle.svelte'
	// import GraphicFooter from './components/GraphicFooter.svelte'
	import * as colors from './helpers/colors.js'

	import Map from './charts/Map.svelte'

	import Map2 from './charts/Map2.svelte'
	import List from './charts/List.svelte';


	// import * as jsondata from '../public/datasets/data.json'
	import * as jsondata from '../public/datasets/route.json'



	const dataset = jsondata.default
	console.log(dataset[0])

	let src;
src = "//news.northeastern.edu/interactive/2020/10/campus-construction-2020/photos/"+dataset[10].id+".jpg";


	// export let width = Math.min(
	// 	document.getElementById('interactive').getBoundingClientRect().width,
	// 	1000
	// );


	// console.log(waffledata.default[0])

	// export let height = 350;
	//
	// function getorientation(w) {
	// 	if (w > 750) {
	// 		return "vertical"
	// 	} else {
	// 		return "horizontal"
	// 	}
	// }

	// $: active = {
	// 	name: "",
	// 	description: "",
	// 	id: ""
	// }
	// console.log(active)
	//
	// function handleClick(place) {
	// 	active = place;
	// 	active = active;
	// 	console.log(active);
	//
	// }



</script>

<style>
.container {
  height: 100vh;
  display: flex;
  flex-flow: wrap-reverse;
  overflow-y: hidden;
   margin: 0;
   max-width: 100%;
   padding: 0;
}

.pane {
  display: flex;
  overflow-y: hidden;
}

.left {
  align-items: center;
  width: 60%;
  justify-content: center;
  z-index:1000;
  max-height: 100vh;
  flex-direction: column;


}

.right {
  justify-content: space-between;
  width: 40%;
  display: block;
  /* margin-left: 50%; */

  /* z-index: -1; */
  max-height: 100vh;

}
.map-legend{
position: absolute;
z-index: 1;

/* color: #fff; */
/* text-shadow: 2px 2px 8px #000; */

color: #fff;
background: rgba(0, 0, 0, 0.3);
text-shadow: 2px 2px 8px #000;
width: 100%;
/* margin: 50px; */
}

.map-content{
	display:flex;
	flex-flow: wrap;
	font-family: akkurat,sans-serif;
	margin: 0 auto;
	opacity: 1;
	justify-content: center;
}

.legendCells{
	display: flex;
/* margin: 0 4px 0 0; */
margin: 10px 10px 0;
}

.cell-label{
	margin: 0 4px;
}

#cell-square{
  width: 10px;
  height: 10px;
  margin: 10px 0;
}
.cell1{
	/* width: 100%; */


           background-color:#F7455D;

}

.cell2{
	/* width: 100%; */
	/* width: 10px;
	height: 10px; */
        background-color: #33C9EB;


}

.cell3{
	/* width: 100%; */
	/* width: 10px;
	height: 10px; */

           background-color:green;

}

.cell4{
	/* width: 100%; */
	/* width: 10px;
	height: 10px; */
        background-color: purple;


}

.cell5{
	/* width: 100%; */
	/* width: 10px;
	height: 10px; */

           background-color:magenta;

}

.cell6{
	/* width: 100%; */
	/* width: 10px;
	height: 10px; */
        background-color: #DAA520;


}
/*
  :global(.marker) {
	display: block;
	transform: rotateZ(-135deg);
	   -webkit-transform: rotateZ(-135deg);
} */

@media (max-width: 750px) {

  .legendCells{
    margin: 4px 4px 4px 0;
  }

	.left {
		width: 100%;
		z-index: 0;
		max-height: 60vh;

	}

	.right{
		width: 100%;
		max-height: 40vh;

	}

	.pane {
		/* max-height:50vh; */
	}

	.map-legend{
		bottom: 0;
	}
}
/* #interactiveContainer {
		height:100vh;
		display: flex; */
		/* margin-bottom:50vh; */
		/* display: grid;
		grid-template-columns: 1fr;
		grid-template-rows: 40% 25% 35%;
		gap: 0px 0px;
		grid-template-areas:
		"map-map"
		"map-nav"
		"map-info"; */
	/* } */
	/* :global(#interactiveContainer div) {
		margin-top: 0;
	}
	.map-info {
		grid-area: map-info;
z-index: 100;
background-color: #fff;
width: 60%;
height: auto;
top: 40px;
left: 40px;
border-radius: 20px;


	}
	/* .map-nav { grid-area: map-nav; } */
	/* .map-map {

		grid-area: map-map;
		width: 40%;

	}

	.map-img{
		width: 100%;
		height: 100%;
		margin: 0;


	}

	.img-cont{
		margin: 0;
	}

	.map-content{
		position:absolute;
		color: #fff;
		z-index:100;
	} */
	/* .map-nav {
		padding-right:0;
	}
	.map-nav button {
		display:inline-block;
		width: 31%;
		height:44px;
		float:left;
		background-color: #efefef;
		border:1px solid #999;
		border-radius:2px;
		margin:0 0.2rem 0.2rem;
		cursor:pointer;
		padding:0.2rem;
		white-space: inherit;
	}
	.map-nav button:hover {
		background-color: #eaeaea;
	}
	.map-nav button:active, .map-nav button:focus {
		background-color: #ddd;
		border:2px solid #999;
	}
	.map-map {
		position: relative;
	  height: 100% !important;
	  width: 60% !important;
	  overflow:hidden;
	}
	span.map-item-title {
		font-size:1.15rem;
		font-weight:bold;
		display:block;
		text-transform:uppercase;
		margin:0.5rem 0 0.5rem 0;
	}
	p.map-item-desc {
		margin-top:0;
		font-size:0.85rem;
	} */
	/* @media screen and (min-width:600px) {
		#interactiveContainer {
			height: 100vh;
			margin-bottom:2rem;
			display: grid;
		   grid-template-columns: 25% 75%;
		   grid-template-rows: 3fr 1fr;
		   gap: 0px 0px;
		   grid-template-areas:
		    "map-nav map-map"
		    "map-info map-info";
		}
		span.map-item-title {
			font-size:1.5rem;
		}
		p.map-item-desc {
			font-size:1rem;
		}
		.map-nav button {
			display:block;
			width: 100%;
			height:unset;
			float:unset;
			text-align:left;
			margin:0 0 0.5rem 0;
			padding:0.25rem;
		}
	} */

</style>
<div class="container">
  <div class="pane left">

    <List />

  </div>

  <div class="pane right">


	<div class = "map-legend">

<div class = "map-content">
	<div class="legendCells">
	  <div id = "cell-square" class="cell1"></div>
	  <div class="cell-label">Monday</div>

  </div>
  <div class="legendCells">
	  <div id = "cell-square" class="cell2"></div>
	  <div class="cell-label">Tuesday</div>

  </div>
  <div class="legendCells">
	<div id = "cell-square" class="cell3"></div>
	<div class="cell-label">Wednesday</div>

  </div>
  <div class="legendCells">
	<div id = "cell-square" class="cell4"></div>
	<div class="cell-label">Thursday</div>

  </div>
  <div class="legendCells">
	<div id = "cell-square" class="cell5"></div>
	<div class="cell-label">Friday</div>

  </div>
  <div class="legendCells">
	<div id = "cell-square" class="cell6"></div>
	<div class="cell-label">Saturday</div>

  </div>
</div>
	</div>

	    <Map2 />
	<!-- <div class="marker mapboxgl-marker mapboxgl-marker-anchor-center" style="transform: translate(-50%, -50%) translate(277px, 486px) rotateX(0deg) rotateZ(0deg);"><span><b>1</b></span></div> -->
  </div>
</div>
<!-- {#if dataset.length > 0} -->
<!-- <div id="interactiveContainer"> -->

<!-- {#each dataset as books} -->


<!-- {active.id} -->

  <!-- <div class="map-info" >
  <div class = "map-content">
	  	<span class="map-item-title">{active.name}</span>
  		<p class="map-item-desc">{active.description}</p>
		</div>
		<div class = "map-img">
		<img src={"//news.northeastern.edu/interactive/2020/10/campus-construction-2020/photos/"+active.id+".jpg"} class = "img-cont" width = "100%" height = "100%" alt="red">

		</div>
  </div> -->
  <!-- <div class="map-nav">
	  {#each dataset as place}
		  <button
		  		data-place={place.id}
				on:click={() =>
					handleClick(place)
				}
			>
			  {place.name}
		  </button>
	  {/each}
  </div> -->
  <!-- <div class="map-map">
	  <Map
		  zoom={11.25}

		  centerlnglat={[-71.087433, 42.32061]}
		  pitch={0}
		  bearing={0}
		  data={dataset}
		  bind:active={active}
	  />
  </div> -->
	<!-- {/each} -->
	<!-- </div> -->

<!-- {/if} -->
