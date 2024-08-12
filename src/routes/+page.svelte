<script lang="ts">
import { onMount } from 'svelte';
import Calendar from "$lib/components/Calendar.svelte";

// Month, Day, Year logic
//-----------------------------
const months = [
    "January", "February", "March", "April", "May", "June",
    "July", "August", "September", "October", "November", "December"
];
const currentDate = new Date();
// const currentDayOfMonth = currentDate.getDate();
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
// function getDaysInMonth(month: number, year: number) {
//   return new Date(year, month, 0).getDate();
// }
// 
// let daysInMonth = getDaysInMonth(currentMonthIndex, currentYear);

</script>

<div class="c-chip__group">
  <span class="c-chip c-chip--red"></span> Payday
  <span class="c-chip c-chip--green"></span>Current Day
</div>

<h2>{ currentMonth } { currentYear }</h2>

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
      background: #ffb46d;
    }
    
    &--green {
      display: inline-flex;
      background: green;
    }
  }
  
  h2 {
    text-align: center;
  }
</style>