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
  let monthLength = time.getMonth()

  
//tasks:
//weekday formatting update per month
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

// $: months,currentYear,initContent();

// function initContent() {
//   initMonth();
// }

// function initMonth() {
// 		let monthAbbrev = months[currentMonth].slice(0,3);
// 		let nextMonthAbbrev = months[(currentMonth+1)%12].slice(0,3);
// 		//	find the last Monday of the previous month
// 		var firstDay = new Date(currentYear, currentMonth, 1).getDay();
// 		//console.log('fd='+firstDay+' '+dayNames[firstDay]);
// 		var daysInThisMonth = new Date(currentYear, currentMonth+1, 0).getDate();
// 		var daysInLastMonth = new Date(currentYear, currentMonth, 0).getDate();
// 		var prevMonth = currentMonth==0 ? 11 : currentMonth-1;
		
// 		//	show the days before the start of this month (disabled) - always less than 7
// 		for (let i=daysInLastMonth-firstDay;i<daysInLastMonth;i++) {
// 			let d = new Date(prevMonth==11?currentYear-1:currentYear,prevMonth,i+1);
// 			day.push({name:''+(i+1),enabled:false,date:d,});
// 		}
// 		//	show the days in this month (enabled) - always 28 - 31
// 		for (let i=0;i<daysInThisMonth;i++) {
// 			let d = new Date(currentYear,currentMonth,i+1);
// 			if (i==0) day.push({name:monthAbbrev+' '+(i+1),enabled:true,date:d,});
// 			else day.push({name:''+(i+1),enabled:true,date:d,});
// 			//console.log('i='+i+'  dt is '+d+' date() is '+d.getDate());
// 		}
// 		//	show any days to fill up the last row (disabled) - always less than 7
// 		for (let i=0;day.length%7;i++) {
// 			let d = new Date((currentMonth==11?currentYear+1:currentYear),(currentMonth+1)%12,i+1);
// 			if (i==0) day.push({name:nextMonthAbbrev+' '+(i+1),enabled:false,date:d,});
// 			else day.push({name:''+(i+1),enabled:false,date:d,});
// 		}
// 	}

// function findRowCol(dt) {
// 	for (let i=0;i<day.length;i++) {
// 		let d = day[i].date;
// 		if (d.getYear() === dt.getYear()
// 			&& d.getMonth() === dt.getMonth()
// 			&& d.getDate() === dt.getDate())
// 			return {row:Math.floor(i/7)+2,col:i%7+1};
// 	}
// 	return null;	
// }

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
  <progress value={$progress} min={1} max="day" in:fly="{{ y: -200, duration: 2000}}" out:fly="{{ y: 200, duration: 2000}}"></progress>
  
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
</main>
