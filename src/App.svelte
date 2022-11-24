<script>
  import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';
  import { fade, fly } from 'svelte/transition';

  let day = [];
  let months = ["January", "Febuary", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
  let time = new Date()
  let currentDay = time.getDate()
  let currentMonth = 0
  let currentYear = time.getFullYear()
  
//tasks:
//weekday formatting fix
//put in active class
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
  }
}

function subrtractMonth() {
  currentMonth--
  if(currentMonth < 0){
    currentMonth = 11;
    currentYear--
  }
}

</script>

<main>
  <progress value={$progress} max="<time datetime='12-31'>" in:fly="{{ y: -200, duration: 2000}}" out:fly="{{ y: 200, duration: 2000}}"></progress>
  
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
    <li>Mon</li>
    <li>Tus</li>
    <li>Wed</li>
    <li>Thu</li>
    <li>Fri</li>
    <li>Sat</li>
    <li>Sun</li>
  </ul>
  
  <ul class="days" >  
    {#each day as d}
      <li>{d}</li>
    {/each}
  </ul>
</main>
