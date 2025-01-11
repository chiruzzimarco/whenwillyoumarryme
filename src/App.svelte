<script>
  import { onMount } from 'svelte';
  import { differenceInDays, differenceInHours, differenceInMinutes, differenceInSeconds } from 'date-fns';

  const MARRIAGE_DATE = new Date('2038-04-09');
  
  let daysLeft = 0;
  let hoursLeft = 0;
  let minutesLeft = 0;
  let secondsLeft = 0;
  let millisecondsLeft = 0;
  let nanosecondsLeft = 0;

  function updateCountdown() {
    const now = new Date();
    daysLeft = differenceInDays(MARRIAGE_DATE, now);
    hoursLeft = differenceInHours(MARRIAGE_DATE, now) % 24;
    minutesLeft = differenceInMinutes(MARRIAGE_DATE, now) % 60;
    secondsLeft = differenceInSeconds(MARRIAGE_DATE, now) % 60;
    millisecondsLeft = now.getMilliseconds();
    
    // Simulate nanoseconds with a rapidly changing number
    nanosecondsLeft = Math.floor(Math.random() * 1000);
  }

  onMount(() => {
    updateCountdown();
    const interval = setInterval(updateCountdown, 1); // Update every millisecond
    return () => clearInterval(interval);
  });
</script>

<main>
  <h1>When Will You Marry Me?</h1>
  <div class="countdown">
    <div class="time-block">
      <span class="number">{daysLeft}</span>
      <span class="label">Days</span>
    </div>
    <div class="time-block">
      <span class="number">{hoursLeft}</span>
      <span class="label">Hours</span>
    </div>
    <div class="time-block">
      <span class="number">{minutesLeft}</span>
      <span class="label">Minutes</span>
    </div>
    <div class="time-block">
      <span class="number">{secondsLeft}</span>
      <span class="label">Seconds</span>
    </div>
    <div class="time-block">
      <span class="number">{millisecondsLeft}</span>
      <span class="label">Milliseconds</span>
    </div>
    <div class="time-block">
      <span class="number">{nanosecondsLeft}</span>
      <span class="label">Nanoseconds*</span>
    </div>
  </div>
  <p>Until our special day on April 9th, 2038!</p>
  <small>* Simulated nanosecond display</small>
</main>

<style>
  main {
    text-align: center;
    padding: 20px;
    font-family: Arial, sans-serif;
  }
  .countdown {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin: 20px 0;
    flex-wrap: wrap;
  }
  .time-block {
    display: flex;
    flex-direction: column;
    align-items: center;
    min-width: 100px;
  }
  .number {
    font-size: 36px;
    font-weight: bold;
  }
  .label {
    font-size: 14px;
    color: #666;
  }
</style>
