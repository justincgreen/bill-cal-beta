<script lang="ts">
import { onMount } from 'svelte';
import CalBlock from "$lib/components/CalBlock.svelte";
import Calendar from "$lib/components/Calendar.svelte";

// Month, Day, Year
//-----------------------------
const months = [
    "January", "February", "March", "April", "May", "June",
    "July", "August", "September", "October", "November", "December"
];
const currentDate = new Date();
const currentDayOfMonth = currentDate.getDate();
const currentYear = currentDate.getFullYear();
const currentMonthIndex = currentDate.getMonth();
const currentMonth = months[currentMonthIndex];

// const daysOfWeek = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
// const today = new Date();
// const dayIndex = today.getDay();
// const dayName = daysOfWeek[dayIndex];  
//---------------------------------------    

// # of days in a month (the total count)
//--------------------------
function getDaysInMonth(month: number, year: number) {
  return new Date(year, month, 0).getDate();
}

let daysInMonth = getDaysInMonth(currentMonthIndex, currentYear);
let totalCalendarDays: Array<number>= []; // NOTE: May not need this

// Functions (Handlers)
const handleBlockClick = (e: any) => {
  alert();
  // document.querySelector('.c-panel').classList.add('is-active');
  // panelData = e.currentTarget.textContent;
}   

onMount(() => {
  const calBlocks = document.querySelectorAll('.c-cal-block');
  calBlocks.forEach((block) => {
    let text = block.firstChild.innerHTML;
    let converted = parseInt(text);
    totalCalendarDays.push(converted); // NOTE: May not need this
    
    if(converted === currentDayOfMonth) {
      block.classList.add('current-day');
    }
  });        
});
</script>

<div class="c-chip__group">
  <span class="c-chip c-chip--red"></span> Payday
  <span class="c-chip c-chip--green"></span>Current Day
</div>

<h2>{ currentMonth } { currentYear }</h2>
<h2>Current Day: { currentDayOfMonth }</h2>

<Calendar />

<style lang="scss">
  .c-chip {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    
    &__group {
      display: inline-flex;
      align-items: center;
      gap: 5px;
      padding: 10px;
    }
    
    &--red {
      display: inline-flex;
      background: orangered;
    }
    
    &--green {
      display: inline-flex;
      background: green;
    }
  }
  
  h2 {
    text-align: center;
  }
  
  .c-grid {
    max-width: 900px;
    margin: auto;
    display: grid;
    grid-template-columns: repeat(7, minmax(0, 1fr));
  }
</style>