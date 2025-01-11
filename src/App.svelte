<script>
  import { onMount } from 'svelte';
  import { differenceInDays, differenceInHours, differenceInMinutes } from 'date-fns';

  const MARRIAGE_DATE = new Date('2038-04-09');
  
  let daysLeft = 0;
  let hoursLeft = 0;
  let minutesLeft = 0;

  // Store additional metadata in localStorage
  function saveCountdownData(data) {
    try {
      localStorage.setItem('marriageCountdownData', JSON.stringify(data));
    } catch (error) {
      console.error('Failed to save countdown data', error);
    }
  }

  function loadCountdownData() {
    try {
      const savedData = localStorage.getItem('marriageCountdownData');
      return savedData ? JSON.parse(savedData) : null;
    } catch (error) {
      console.error('Failed to load countdown data', error);
      return null;
    }
  }

  function updateCountdown() {
    const now = new Date();
    daysLeft = differenceInDays(MARRIAGE_DATE, now);
    hoursLeft = differenceInHours(MARRIAGE_DATE, now) % 24;
    minutesLeft = differenceInMinutes(MARRIAGE_DATE, now) % 60;

    // Optional: Save additional metadata
    saveCountdownData({
      daysLeft,
      hoursLeft,
      minutesLeft,
      lastUpdated: now.toISOString()
    });
  }

  onMount(() => {
    // Try to load saved data first
    const savedData = loadCountdownData();
    if (savedData) {
      daysLeft = savedData.daysLeft;
      hoursLeft = savedData.hoursLeft;
      minutesLeft = savedData.minutesLeft;
    }

    updateCountdown();
    const interval = setInterval(updateCountdown, 60000);
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
  </div>
  <p>Until our special day on April 9th, 2038!</p>
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
  }
  .time-block {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .number {
    font-size: 48px;
    font-weight: bold;
  }
  .label {
    font-size: 16px;
    color: #666;
  }
</style>
