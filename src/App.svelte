<script>
  //Calander?
  //Animation of stick figure per reload to signify day
  //Uses graphic of calander (either img or canvas)
  //Use date function?

import P5 from 'p5-svelte';

let width = 55;
let height = 55;

let sketch = (p5) => {
  p5.setup = () => {
    p5.createCanvas(400, 400);
  };
  p5.draw = () => {
    p5.ellipse(p5.width / 2, p5.height / 2, width, height);
  };
};

function stickFigure() {
//creates stickfigure  
}

function calander() {
//creates calander
}

function move(date) {
//indicates date for stickfigure to move towards
}

function openDoor() {
//allows stickfigure to move from each week/month
}



</script>

<label>
	Width
	<input type="range" bind:value={width} min="100" max="1000" step="0.01" />
	{width}
</label>

<label>
	Height
	<input type="range" bind:value={height} min="100" max="1000" step="0.01" />
	{height}
</label>

<main>
  <P5 {sketch} />
</main>

<style>

</style>
