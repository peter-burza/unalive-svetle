<script>
  let { data, lifeExpentency } = $props();

  const yearsArr = $derived([...Array(lifeExpentency).keys()]); // Creates an array of lifeExpentency.length count numbers in it
  const weeksArr = [...Array(52).keys()];

  const weekNum = $derived(lifeExpentency * 52 - parseInt(data["weeks"]));
  const finalWeek = $derived(lifeExpentency * 52);
</script>

<section id="calendar">
  <p><i>Each group of dots represents 52 weeks / 1 year of your life.</i></p>

  <div class="dozen-grid">
    {#each yearsArr as year, yearIndex}
      <div class="year-grid">
        {#each weeksArr.map((val, valIndex) => {
          const currWeek = yearIndex * 52 + valIndex;
          const dotStyle = currWeek == finalWeek - 1 ? " death" : currWeek < weekNum ? " solid" : currWeek == weekNum ? " pulse" : " ";
          return { week: val, currWeek, dotStyle };
        }) as week, weekIndex}
            <div class="dot {week.dotStyle}"></div>
        {/each}
      </div>
    {/each}
  </div>
</section>
