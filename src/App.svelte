<script>
  //Calendar?
  //Animation of stick figure per reload to signify day
  //Uses graphic of calendar (either img or canvas)
  //Use date function?

  //Plan
  //Create Calendar
  //Create stickfigure
  //Create move cycle
  //Create "openDoor" 
  //Create end points per date
  //Create "doorpoints" (probably boolean)
  


import P5 from 'p5-svelte';

let width = 1000;
let height = 1000;

let sketch = (p5) => {
  p5.setup = () => {
    p5.createCanvas(1000, 725);
  };
  p5.draw = () => {
  p5.background(100);
  p5.noStroke();
  for (let i = 0; i < height; i += 143) {
    p5.rect(0, i, width, 10);
    p5.fill(500);
    p5.rect(i, 0, 10, height);
  }
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

<main>
  <P5 {sketch} />
</main>

<style>

</style>
