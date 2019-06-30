<script>
  import CircleGroup from "./CircleGroup.svelte";
  const TAU = Math.PI * 2;
  export const size = 100;
  $: number = 10;
  $: times = 2;
  $: shownums = false;
  let radius = size / 2 - 1;
  const constructPos = m =>
    Array.from({ length: m }).map((_, n) => (TAU / m) * n);
  const constructLines = t => m =>
    Array.from({ length: m }).map((_, n) => [n, (n * t) % m]);
  $: positions = constructPos(number);
  $: lines = constructLines(times)(number);
</script>

<style>
  controlgroup {
    display: flex;
    width: 100%;
  }
  control {
    display: flex;
    flex-flow: column;
    width: 100%;
  }
  control.min {
    width: 10%;
  }
  input {
    width: 85%;
  }
  input[type="checkbox"] {
    width: 10%;
  }
  svg {
    width: 100%;
    height: calc(100% - 5em);
  }
  /* text {
    font-size: 3px;
    text-anchor: middle;
  } */
  svg > g > text {
    font: 0.2em sans-serif;
    /* fill: rgba(124, 55, 80, 0.8); */
    fill: white;
  }
</style>

<svg viewBox="0 0 {size} {size}">
  <g transform="translate({size / 2},{size / 2})">
    <!-- <text x={size * -0.35} y={size * -0.35}>
       {Math.trunc(radius * 10) / 10}
    </text> -->
    <circle
      cx={0}
      r={radius}
      fill="rgba(124, 55, 80, 1)"
      stroke="#98AFC7"
      stroke-width="0.01em" />
    {#each positions as h, i}
      <circle r={1 / 2} cx={radius * Math.cos(h)} cy={radius * Math.sin(h)} />
      {#if shownums}
        <text x={0.8 * radius * Math.cos(h)} y={0.8 * radius * Math.sin(h)}>
           {i}
        </text>
      {/if}
    {/each}
    {#each lines as [p0, p1], i}
      <line
        x1={radius * Math.cos(positions[p0])}
        y1={radius * Math.sin(positions[p0])}
        x2={radius * Math.cos(positions[p1])}
        y2={radius * Math.sin(positions[p1])}
        stroke="rgba(255, 255, 0, 0.9)"
        stroke-width={10 / number} />
    {/each}
  </g>
</svg>
<controlgroup>
  <control>
    <div>number [{number}]</div>
    <input bind:value={number} type="range" min={3} max={400} step={1} />
  </control>
  <control>
    <div>times [{times}]</div>
    <input bind:value={times} type="range" min={1} max={400} step={1} />
  </control>
  <control class="min">
    <div>numbers</div>
    <input bind:checked={shownums} type="checkbox" />
  </control>
</controlgroup>
