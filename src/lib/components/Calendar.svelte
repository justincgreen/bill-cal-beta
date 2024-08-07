<script lang="ts">
  import { onMount } from 'svelte';
  import Modal from "$lib/components/Modal.svelte";   
  
  // Build Calendar
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
  
  // Logic for dynamic .current-day class on calendar
  const currentDate = new Date();
  const currentDayOfMonth = currentDate.getDate();
  let totalCalendarDays: Array<number> = []; 
  //-----------------------------------------------
  
  // Modal logic
  let displayModal = {
    show: false
  }; 
  
  // let panelDate: { date: string; } = {
  //   date: 'placeholder'
  // }
  
  interface panelObject {
    date?: string,
    blockClass?: string
  }
  
  let panelInfo: panelObject = { 
    date: 'placeholder',
    blockClass: 'placeholder' 
  };
  //-----------------------------------------------
  
  // Handlers 
  const handleClick = (e: any) => {
    // alert(e.currentTarget.querySelector('.c-calendar__date-number').innerHTML);
    // document.querySelector('.c-modal').classList.add('is-active');
   panelInfo.date = e.currentTarget.querySelector('.c-calendar__date-number').innerHTML;
   let panelBlockClassList = e.currentTarget.querySelector('.c-calendar__date-number').classList;
   panelInfo.blockClass = panelBlockClassList[1];    
   displayModal.show = !displayModal.show
  }
  
  onMount(() => {
    const calendarDateBlocks = document.querySelectorAll('.c-calendar__date-block');
    calendarDateBlocks.forEach((block) => {
      let blockNumber = block.querySelector('.c-calendar__date-number');
      let blockText = blockNumber ? blockNumber.innerHTML : null;
      let convertedNumber = parseInt(blockText ?? '');
      totalCalendarDays.push(convertedNumber);
      
      // Add block class                   
      // if(blockText !== '') {
      //   block.classList.add(`c-calendar__block-${convertedNumber}`);
      // }
      
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
  
  {#each calendarDays as calendarDay, index}
    <div class="c-calendar__date-block" on:click={handleClick} role="button" tabindex="0">
      <span class={`c-calendar__date-number c-calendar__date-number--${index}`}>{calendarDay}</span>
    </div>
  {/each}
</div>

<Modal
  modalData={displayModal}
  panelBlockInfo={panelInfo}
/>

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
      cursor: pointer;
    }
    
    &__date-number {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      width: 20px;
      height: 20px;
      padding: 4px;
      border-radius: 50%;
    }
  }  
  
  :global(.current-day > .c-calendar__date-number) {       
    background: green;  
    color: white;  
  }  
  
  :global(.is-payday) {
    background: #ffb46d;
    color: white;
  }  
</style>