<script>
  import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';
  import { each, loop_guard } from 'svelte/internal';

  let day = [];
  let months = ["January", "Febuary", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
  let time = new Date()
  let currentDay = 0
  let currentMonth = 0
  let currentYear = 0
  

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

currentYear = time.getFullYear()

</script>

<main>
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
    <!-- <li><span class="active">10</span></li> -->
  </ul>
</main>

<style>
  * {box-sizing: border-box;}
ul {list-style-type: none;}
main {font-family: Verdana, sans-serif;}
.month {
  padding: 70px 25px;
  width: 100%;
  background: #1abc9c;
  text-align: center;
}

.month ul {
  margin: 0;
  padding: 0;
}

.month ul li {
  color: white;
  font-size: 20px;
  text-transform: uppercase;
  letter-spacing: 3px;
}

.month .prev {
  float: left;
  padding-top: 10px;
}

.month .next {
  float: right;
  padding-top: 10px;
}

.weekdays {
  margin: 0;
  padding: 10px 0;
  background-color: #ddd;
}

.weekdays li {
  display: inline-block;
  width: 13.6%;
  color: #666;
  text-align: center;
}

.days {
  padding: 10px 0;
  background: #eee;
  margin: 0;
}

.days li {
  align-items: center;
  list-style-type: none;
  display: inline-block;
  width: 13.6%;
  text-align: center;
  margin-left: 5px;
  margin-right: 5px;
  margin-bottom: 5px;
  font-size:12px;
  color: #777;
}

.days li .active {
  padding: 5px;
  background: #1abc9c;
  color: white !important
}

/* Add media queries for smaller screens */
@media screen and (max-width:720px) {
  .weekdays li, .days li {width: 13.1%;}
}

@media screen and (max-width: 420px) {
  .weekdays li, .days li {width: 12.5%;}
  .days li .active {padding: 2px;}
}

@media screen and (max-width: 290px) {
  .weekdays li, .days li {width: 12.2%;}
}
</style>
