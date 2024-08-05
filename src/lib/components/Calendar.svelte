<script>
    let daysOfWeek = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];

    let date = new Date();
    let year = date.getFullYear();
    let month = date.getMonth();

    let firstDay = new Date(year, month, 1).getDay();
    let daysInMonth = new Date(year, month + 1, 0).getDate();

    let calendarDays = [];

    // Fill the blank spaces for days before the first day of the month
    for (let i = 0; i < firstDay; i++) {
        calendarDays.push('');
    }

    // Fill the days of the month
    for (let i = 1; i <= daysInMonth; i++) {
        calendarDays.push(i);
    }
</script>

<div class="calendar">
  {#each daysOfWeek as day}
    <div class="header day">{day}</div>
  {/each}
  
  {#each calendarDays as calendarDay}
    <div class="date">{calendarDay}</div>
  {/each}
</div>

<style lang="scss">
  .calendar {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    max-width: 800px;
    margin: auto;
  }
  .day, 
  .date {
    text-align: center;
    padding: 10px;
    border: 1px solid #ccc;
  }
  .date {
    padding: 40px;
  }
  .header {
    font-weight: bold;
  }
</style>