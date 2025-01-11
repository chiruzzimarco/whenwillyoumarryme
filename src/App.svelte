<script>
  import { onMount } from 'svelte';
  import { differenceInDays, differenceInHours, differenceInMinutes, differenceInSeconds } from 'date-fns';

  const MARRIAGE_DATE = new Date('2038-04-09');
  
  let daysLeft = 0;
  let hoursLeft = 0;
  let minutesLeft = 0;
  let secondsLeft = 0;
  let millisecondsLeft = 0;

  function updateCountdown() {
    const now = new Date();
    daysLeft = differenceInDays(MARRIAGE_DATE, now);
    hoursLeft = differenceInHours(MARRIAGE_DATE, now) % 24;
    minutesLeft = differenceInMinutes(MARRIAGE_DATE, now) % 60;
    secondsLeft = differenceInSeconds(MARRIAGE_DATE, now) % 60;
    millisecondsLeft = now.getMilliseconds();
  }

  onMount(() => {
    updateCountdown();
    const interval = setInterval(updateCountdown, 1); // Update every millisecond
    return () => clearInterval(interval);
  });
</script>

<main>
  <div class="container">
    <div class="heart-background">
      <h1>Our Love Story Continues...</h1>
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
      </div>
      <p class="wedding-date">Until Our Wedding Day 💍</p>
      <p class="wedding-location">April 9th, 2038</p>
    </div>
  </div>
</main>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Great+Vibes&family=Playfair+Display:wght@400;700&display=swap');

  :root {
    --primary-color: #8B4513;
    --secondary-color: #FFE4E1;
    --accent-color: #D2691E;
  }

  main {
    margin: 0;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: var(--secondary-color);
    font-family: 'Playfair Display', serif;
    color: var(--primary-color);
  }

  .container {
    width: 90%;
    max-width: 800px;
    background-color: white;
    border-radius: 20px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.1);
    overflow: hidden;
  }

  .heart-background {
    background: 
      linear-gradient(rgba(255,255,255,0.8), rgba(255,255,255,0.8)),
      url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 80 80" width="80" height="80"><path d="M0 0 Q40 40 80 0 Q40 40 0 80 Q40 40 0 0" fill="%23FFB6C1" opacity="0.1"/></svg>');
    padding: 40px;
    text-align: center;
  }

  h1 {
    font-family: 'Great Vibes', cursive;
    font-size: 3rem;
    color: var(--accent-color);
    margin-bottom: 30px;
  }

  .countdown {
    display: flex;
    justify-content: center;
    gap: 30px;
    margin: 30px 0;
  }

  .time-block {
    display: flex;
    flex-direction: column;
    align-items: center;
    min-width: 100px;
    background-color: rgba(139, 69, 19, 0.05);
    padding: 15px;
    border-radius: 10px;
    transition: transform 0.3s ease;
  }

  .time-block:hover {
    transform: scale(1.05);
  }

  .number {
    font-size: 48px;
    font-weight: bold;
    color: var(--primary-color);
  }

  .label {
    font-size: 16px;
    color: var(--accent-color);
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  .wedding-date {
    font-size: 1.5rem;
    margin-top: 20px;
    color: var(--accent-color);
  }

  .wedding-location {
    font-family: 'Great Vibes', cursive;
    font-size: 2rem;
    color: var(--primary-color);
  }

  @media (max-width: 600px) {
    .countdown {
      flex-wrap: wrap;
      gap: 15px;
    }

    .time-block {
      min-width: 80px;
    }

    .number {
      font-size: 36px;
    }
  }
</style>
