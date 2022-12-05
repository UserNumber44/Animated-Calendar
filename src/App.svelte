<script>
  import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';
  import { each } from 'svelte/internal';

  let day = [];
  const months = ["January", "Febuary", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
  const weekday = ["Sun", "Mon", "Tus", "Wed", "Thu", "Fri", "Sat"]
  let time = new Date()
  let currentDay = time.getDate()
  let currentMonth = 0
  let currentYear = time.getFullYear()
  
//tasks:
//weekday formatting update per month
//progress bar

const progress = tweened(0, {
  duration: 400,
  easing: cubicOut
});

progress.set(currentDay)

let d = new Date(currentYear, currentMonth + 1, 0).getDate()
for(let i = 1; i <= d; i++){
  day.push(i);
}
day=day

function addMonth(){
  currentMonth++
  if(currentMonth > 11){
    currentMonth = 0;
    currentYear++
  }let d = new Date(currentYear, currentMonth + 1, 0).getDate()
    day = [];
    for(let i = 1; i <= d; i++){
      day.push(i);
    }day=day
}

function subrtractMonth(){
  currentMonth--
  if(currentMonth < 0){
    currentMonth = 11;
    currentYear--
  }let d = new Date(currentYear, currentMonth + 1, 0).getDate()
    day = [];
    for(let i = 1; i <= d; i++){
      day.push(i);
    }day=day
}

</script>

<main>  
  <div class="month">      
    <h2>{time}</h2>
    <ul>
      <button class="prev" on:click= {subrtractMonth}>&#10094;</button>
      <button class="next" on:click= {addMonth}>&#10095;</button>
      {#each months as m, i}
      {#if currentMonth == i}
      <li>
        {m}<br>
        <span style="font-size:18px">{currentYear}</span>
      </li>
      {/if}
      {/each}
    </ul>
  </div>
  
  <ul class="weekdays">
    {#each weekday as w}
    <li>
      {w}
    </li>
    {/each}
  </ul>
  
  <ul class="days" > 
    {#each day as d}
    <li>{d}</li> 
    {/each}  
  </ul>
  
  <progress value={$progress} min=1 max={new Date(currentYear, currentMonth + 1, 0).getDate()}></progress>
</main>
