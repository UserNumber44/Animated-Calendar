<script>
  import P5 from 'p5-svelte';
  import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';

  let width = 1000;
  let height = 1000;
  
  //Calendar
  let sketch = (p5) => {
    p5.setup = () => {
      p5.createCanvas(1000, 725);
    };
    p5.draw = () => {
      p5.noStroke();
      p5.background(100);
      for (let i = 0; i < height; i += 143) {
        p5.rect(0, i, width, 10);
        p5.fill(500);
        p5.rect(i, 0, 10, height);
      };
    };
  };
  //Progress bar

</script>

<main>
  <P5 {sketch} />
</main>

<style>

</style>
