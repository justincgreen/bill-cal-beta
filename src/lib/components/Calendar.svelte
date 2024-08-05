<script lang="ts">
  import { onMount } from 'svelte';
  let daysOfWeek = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];

  let date = new Date();
  let year = date.getFullYear();
  let month = date.getMonth();

  let firstDay = new Date(year, month, 1).getDay();
  let daysInMonth = new Date(year, month + 1, 0).getDate();

  let calendarDays: Array<string | number> = [];

  // Fill the blank spaces for days before the first day of the month
  for (let i = 0; i < firstDay; i++) {
      calendarDays.push('');
  }

  // Fill the days of the month
  for (let i = 1; i <= daysInMonth; i++) {
      calendarDays.push(i);
  }
  
  //----------------------------------------------
  const currentDate = new Date();
  const currentDayOfMonth = currentDate.getDate();
  let totalCalendarDays: Array<number> = [];
  //-----------------------------------------------
  
  // Handlers 
  const handleClick = (e: any) => {
    alert(e.currentTarget.querySelector('.c-calendar__date-number').innerHTML);
  }
  
  onMount(() => {
    const calendarDateBlocks = document.querySelectorAll('.c-calendar__date-block');
    calendarDateBlocks.forEach((block) => {
      let blockNumber = block.querySelector('.c-calendar__date-number');
      let text = blockNumber ? blockNumber.innerHTML : null;
      let convertedNumber = parseInt(text ?? '');
      totalCalendarDays.push(convertedNumber);
      
      if(convertedNumber === currentDayOfMonth) {
        block.classList.add('current-day');
      }
    });        
  });
</script>

<div class="c-calendar">
  {#each daysOfWeek as day}
    <div class="c-calendar__day-title">{day}</div>
  {/each}
  
  {#each calendarDays as calendarDay}
    <div class="c-calendar__date-block" on:click={handleClick} role="button" tabindex="0">
      <span class="c-calendar__date-number">{calendarDay}</span>
    </div>
  {/each}
</div>

<style lang="scss">
  .c-calendar {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    max-width: 800px;
    margin: auto;
    
    &__day-title {
      text-align: center;
      padding: 10px;
      border: 1px solid #ccc;
      font-weight: bold;
    }
    
    &__date-block {
      padding: 10px 10px 60px 10px;
      border: 1px solid #ccc;
    }
  }  
  
  :global(.current-day > .c-calendar__date-number) {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    padding: 5px;
    background: green;
    color: white;
    border-radius: 50%;
  }  
</style>