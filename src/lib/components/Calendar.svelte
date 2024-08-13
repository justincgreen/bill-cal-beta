<script lang="ts">
  import { onMount } from 'svelte';
  import { setContext } from 'svelte';
  import { writable } from 'svelte/store';
  import Modal from "$lib/components/Modal.svelte";   
  import Toast from "$lib/components/Toast.svelte";   
  
  const toastValue = writable('Testing');
  setContext('toastContext', toastValue);
  
  const isToastVisible = writable(false);
  setContext('toastToggle', isToastVisible);
  
  // Build Calendar
  const months = [
    "January", "February", "March", "April", "May", "June",
    "July", "August", "September", "October", "November", "December"
  ];
  
  let daysTitle = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
  let date = new Date();
  let currentYear = date.getFullYear();
  let currentMonth = date.getMonth();
  let calendarDayNumbers: Array<any> = [];
  
  const generateCalendarData = (year: number, month: any) => {
    const daysOfWeek = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
    const calendarDayNumbers = [];
    
    // Get the first day of the month (0 = Sunday, 1 = Monday, ..., 6 = Saturday)
    const firstDay = new Date(year, month, 1).getDay();
  
    // Get the number of days in the month
    const daysInMonth = new Date(year, month + 1, 0).getDate();
    
    // Fill the blank spaces for days before the first day of the month
    for (let i = 0; i < firstDay; i++) {
      calendarDayNumbers.push('');
    }
  
    // Fill the days of the month
    for (let i = 1; i <= daysInMonth; i++) {
      // Create a new date object for each day in the month
      const date = new Date(year, month, i);
      calendarDayNumbers.push({ date: i, dayName: daysOfWeek[date.getDay()] });
    }
  
    return calendarDayNumbers;
  };
  
  const calendarData = generateCalendarData(currentYear, currentMonth);
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
  
  interface panelObject {
    date?: string,
    dayName?: string,
    currentYear: number,
    blockClass?: string,
    buttonText?: string
  }
  
  let panelInfo: panelObject = { 
    date: 'placeholder',
    dayName: 'placeholder',
    currentMonth: months[currentMonth],
    currentYear: currentYear,
    blockClass: 'placeholder',
    buttonText: 'Mark Pay Day' 
  };
  //-----------------------------------------------
  
  // Toast logic 
  let toastMessage = 'Testing';
  //---------------------
  
  // Handlers 
  const handleClick = (e: any) => {
    let panelBlockEmpty = e.currentTarget.innerHTML.trim() === '';
    
    if(!panelBlockEmpty) {
      let panelBlockClassList = e.currentTarget.querySelector('.c-calendar__date-number').classList;    
      panelInfo.dayName = e.currentTarget.querySelector('.c-calendar__date-day').innerHTML;      
      panelInfo.date = e.currentTarget.querySelector('.c-calendar__date-number').innerHTML;      
      panelInfo.blockClass = panelBlockClassList[1];    
      displayModal.show = !displayModal.show;
      
      // Control button text from calendar component side based on block .is-payday class
      if(e.currentTarget.firstElementChild.classList.contains(`is-payday`)) {
      panelInfo.buttonText = 'Remove Pay Day';
      }else {
      panelInfo.buttonText = 'Mark Pay Day';
      } 
    }else {
      alert('Please select a day within the current month');
    }   
  }
  
  onMount(() => {
    const calendarDateBlocks = document.querySelectorAll('.c-calendar__date-block');
    
    calendarDateBlocks.forEach((block) => {
      let blockNumber = block.querySelector('.c-calendar__date-number');
      let blockText = blockNumber ? blockNumber.innerHTML : null;
      let convertedNumber = parseInt(blockText ?? '');
      totalCalendarDays.push(convertedNumber);
      
      if(convertedNumber === currentDayOfMonth) {
        block.classList.add('current-day');
      }
    });        
  });
</script>

<div class="c-calendar">
  {#each daysTitle as day}
    <div class="c-calendar__day-title">{day}</div>
  {/each}
  
  {#each calendarData as calendarDay, index}
    <div class="c-calendar__date-block" on:click={handleClick} role="button" tabindex="0">
      {#if calendarDay.date !== undefined}        
        <span class={`c-calendar__date-number c-calendar__date-number--${index}`}>{calendarDay.date}</span>
        <span class="c-calendar__date-day">{calendarDay.dayName}</span>
      {/if}      
    </div>
  {/each}
</div>

<Modal
  modalData={displayModal}
  panelBlockInfo={panelInfo}
/>
<Toast />

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
    
    &__date-day {
      display: none;
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