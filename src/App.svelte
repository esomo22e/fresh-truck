<script>
	import { onMount } from 'svelte';
	import GraphicTitle from './components/GraphicTitle.svelte'
	// import GraphicFooter from './components/GraphicFooter.svelte'
	import * as colors from './helpers/colors.js'


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
  /* height: 100vh; */
  display: flex;
  flex-wrap: wrap-reverse;
  /* overflow-y: hidden; */
   margin: 0;
   max-width: 100%;
   padding: 0;
}

.pane {
  display: flex;
  /* overflow-y: hidden; */
}

.left {
  align-items: center;
  width: 60%;
  justify-content: center;
  z-index:1000;
  /* max-height: 100vh; */
  flex-direction: column;


}

.right {
  justify-content: space-between;
  width: 40%;
  height: 100vh;
  /* max-height: 100vh; */
  /* display: block; */
  /* margin-left: 50%; */

  /* z-index: -1; */
  /* max-height: 100vh; */
  /* max-height: auto; */

  position: sticky;
  top:  var(--article-progress--height);

  align-self: flex-end;
  --article-progress--height: 30px;
    max-height: calc(100vh - var(--article-progress--height));
    /* align-self: flex-end; */
  /* --article-progress--width:62px;
   max-height: calc(100vh - var(--article-progress--width));
   position: sticky;
   top: var(--article-progress--width); */


}

/* Cover the map pane to prevent direct user intereaction. */
.pane.right::after {
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 10;
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

.container{
  flex-wrap: wrap;

}
  .legendCells{
    margin: 4px 4px 4px 0;
  }

	.left {
		width: 100%;
		z-index: 0;



	}

	.right{
		width: 100%;
		max-height: 25vh;
    bottom: 0;
	display: none;
	}

	.pane {
		/* max-height:50vh; */
	}

	.map-legend{
		bottom: 0;
	}
}

</style>
<div class="container">
  <div class="pane left" >

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

</div>
	</div>

	    <Map2 />
  </div>
</div>
