<script>
  import CircleGroup from "./CircleGroup.svelte";
  const tau = Math.PI * 2;
  const construct = m => Array.from({ length: m }).map((_, n) => (tau / m) * n);
  export const size = 100;
  let distance = Math.tan((-2 / 3) * Math.PI); // 120 degrees
  let num = 6;
  let angle = tau / 5;
  $: hex = construct(num);
  let radius;
  $: radius = 0.5 + (angle / tau) * (size / 2 - 1);
</script>

<style>
  /* input {
    width: 100%;
  } */
  svg {
    width: 100%;
    height: calc(100% - 5em);
  }
  /* text {
    font-size: 3px;
    text-anchor: middle;
  } */
</style>

<svg viewBox="0 0 {size} {size}">
  <g transform="translate({size / 2},{size / 2})">
    <!-- <text x={size * -0.35} y={size * -0.35}>
       {Math.trunc(radius * 10) / 10}
    </text> -->
    <circle
      cx={0}
      r={radius}
      fill="#A5E4E2"
      stroke="#98AFC7"
      stroke-width={radius / 30} />
    <CircleGroup
      {radius}
      hexes={hex}
      strokemod="60"
      stroke="#98AFC7"
      fill="rgba(255,63,127,0.1)" />
    <CircleGroup
      rotation="90"
      {radius}
      {distance}
      hexes={hex}
      strokemod="120"
      stroke="#98AFC7" />
    <CircleGroup
      {radius}
      distance={distance ** 2}
      hexes={hex}
      strokemod="150"
      stroke="#98AFC7" />
    <CircleGroup
      rotation={30}
      {radius}
      distance={distance * 2}
      hexes={hex}
      strokemod="180"
      stroke="#98AFC7"
      fill="rgba(136,127,255,0.1)" />
  </g>
</svg>
<!-- angle [{angle}]
<input bind:value={angle} type="range" min={0} max={tau} step={0.1} />
distance [{distance}]
<input bind:value={distance} type="range" min={1} max={3} step={0.01} />
num [{num}]
<input bind:value={num} type="range" min={6} max={64} step={1} /> -->
