<script>
  import { onMount } from 'svelte';
  import { differenceInYears, differenceInDays, differenceInHours, differenceInMinutes, differenceInSeconds } from 'date-fns';

  const MARRIAGE_DATE = new Date('2037-08-09');

  let yearsLeft = 0;
  let daysLeft = 0;
  let hoursLeft = 0;
  let minutesLeft = 0;
  let secondsLeft = 0;

  function updateCountdown() {
    const now = new Date();
    yearsLeft = differenceInYears(MARRIAGE_DATE, now);
    daysLeft = differenceInDays(MARRIAGE_DATE, now) % 365;
    hoursLeft = differenceInHours(MARRIAGE_DATE, now) % 24;
    minutesLeft = differenceInMinutes(MARRIAGE_DATE, now) % 60;
    secondsLeft = differenceInSeconds(MARRIAGE_DATE, now) % 60;
  }

  onMount(() => {
    updateCountdown();
    const interval = setInterval(updateCountdown, 1000); // Update every second
    return () => clearInterval(interval);
  });
</script>

<main>
  <div class="container">
    <div class="heart-background">
      <h1>Il tempo stringe...</h1>
      <div class="countdown">
        <div class="time-block">
          <span class="number">{yearsLeft}</span>
          <span class="label">Anni</span>
        </div>
        <div class="time-block">
          <span class="number">{daysLeft}</span>
          <span class="label">Giorni</span>
        </div>
        <div class="time-block">
          <span class="number">{hoursLeft}</span>
          <span class="label">Ore</span>
        </div>
        <div class="time-block">
          <span class="number">{minutesLeft}</span>
          <span class="label">Minuti</span>
        </div>
        <div class="time-block">
          <span class="number">{secondsLeft}</span>
          <span class="label">Secondi</span>
        </div>
      </div>
      <p class="wedding-date">Buona fortuna, fino al giorno del nostro matrimonio! 💍</p>
      <p class="wedding-location">9 Agosto 2037</p>
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

  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  html, body {
    height: 100%;
    margin: 0;
    padding: 0;
    overflow-x: hidden;
  }

  main {
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: var(--secondary-color);
    font-family: 'Playfair Display', serif;
    color: var(--primary-color);
    padding: 20px;
  }

  .container {
    width: 100%;
    max-width: 1000px;
    background-color: white;
    border-radius: 20px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.1);
    overflow: hidden;
  }

  .heart-background {
    background:
      linear-gradient(rgba(255,255,255,0.8), rgba(255,255,255,0.8)),
      url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 80 80" width="80" height="80"><path d="M0 0 Q40 40 80 0 Q40 40 0 80 Q40 40 0 0" fill="%23FFB6C1" opacity="0.1"/></svg>');
    padding: 20px;
    text-align: center;
  }

  h1 {
    font-family: 'Great Vibes', cursive;
    font-size: 2.5rem;
    color: var(--accent-color);
    margin-bottom: 20px;
  }

  .countdown {
    display: flex;
    justify-content: center;
    gap: 15px;
    margin: 20px 0;
    flex-wrap: wrap;
  }

  .time-block {
    display: flex;
    flex-direction: column;
    align-items: center;
    min-width: 100px;
    background-color: rgba(139, 69, 19, 0.05);
    padding: 10px;
    border-radius: 10px;
    transition: transform 0.3s ease;
  }

  .time-block:hover {
    transform: scale(1.05);
  }

  .number {
    font-size: 36px;
    font-weight: bold;
    color: var(--primary-color);
  }

  .label {
    font-size: 14px;
    color: var(--accent-color);
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  .wedding-date {
    font-size: 1.2rem;
    margin-top: 15px;
    color: var(--accent-color);
  }

  .wedding-location {
    font-family: 'Great Vibes', cursive;
    font-size: 1.8rem;
    color: var(--primary-color);
  }

  @media (max-width: 600px) {
    main {
      padding: 10px;
    }

    h1 {
      font-size: 2rem;
      margin-bottom: 10px;
    }

    .countdown {
      flex-direction: column;
      align-items: center;
      gap: 10px;
    }

    .time-block {
      width: 80%;
      max-width: 300px;
    }

    .number {
      font-size: 28px;
    }

    .label {
      font-size: 12px;
    }

    .wedding-date {
      font-size: 1rem;
    }

    .wedding-location {
      font-size: 1.5rem;
    }
  }
</style>
