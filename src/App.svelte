<script>
  import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';
  import { fade, fly } from 'svelte/transition';
  import { each } from 'svelte/internal';

  let day = [];
  let months = ["January", "Febuary", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
  let weekday = ["Sun", "Mon", "Tus", "Wed", "Thu", "Fri", "Sat"]
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

for(let i = 1; i <= 31; i++){
  day.push(i);
}
day=day

function addMonth(){
  currentMonth++
  if(currentMonth > 11){
    currentMonth = 0;
    currentYear++
  }if((currentMonth + 1)%2 == 0){
    day = [];
    for(let i = 1; i <= 30; i++){
      day.push(i);
    }
  }if((currentMonth + 1)%2 == 1){
    day = [];
    for(let i = 1; i <= 31; i++){
      day.push(i);
    }
  }if(currentMonth == 1){
    day = [];
    for(let i = 1; i <= 28; i++){
      day.push(i);
    }
  }
    if((currentMonth + 1)%2 == 0){ 
    day = [];
    for(let i = 1; i <= 30; i++){
      day.push(i);}
    }
if((currentMonth + 1)%2 == 1){ 
    day = [];
    for(let i = 1; i <= 31; i++){
      day.push(i);}
    }day=day
  if(currentMonth == 1){
    day = [];
    for(let i = 1; i <= 28; i++){
      day.push(i);
    }day=day
  }
}

function subrtractMonth(){
  currentMonth--
  if(currentMonth < 0){
    currentMonth = 11;
    currentYear--
  }
    if((currentMonth + 1)%2 == 0){ 
    day = [];
    for(let i = 1; i <= 30; i++){
      day.push(i);}
    }if((currentMonth + 1)%2 == 1){ 
    day = [];
    for(let i = 1; i <= 31; i++){
      day.push(i);}
    }day=day
    if(currentMonth == 1){
    day = [];
    for(let i = 1; i <= 28; i++){
      day.push(i);
    }day=day
  }
}
</script>

<main>
  <h1>{time}</h1>
  
  <div class="month">      
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
  
  <progress value={$progress} min=1 max=31></progress>
</main>
