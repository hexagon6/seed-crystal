<script>
  import CircleGroup from "./CircleGroup.svelte";
  const tau = Math.PI * 2;
  const construct = m => Array.from({ length: m }).map((_, n) => (tau / m) * n);
  const clip = number => number.toFixed(2);
  export const size = 100;
  let distance = 1.51; // Math.tan((-2 / 3) * Math.PI); // 120 degrees
  let num = 14; // 6;
  let angle = 0.6; // tau / 5;
  $: hex = construct(num);
  let radius;
  $: radius = 0.5 + (angle / tau) * (size / 2 - 1);
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
  input {
    width: 66%;
  }
  svg {
    width: 100%;
    height: 100%;
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
      distance={0}
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
<controlgroup>
  <control>
    <div>zoom [{clip(angle)}]</div>
    <input bind:value={angle} type="range" min={0} max={tau} step={0.1} />
  </control>
  <control>
    <div>distance [{clip(distance)}]</div>
    <input bind:value={distance} type="range" min={1} max={3} step={0.01} />
  </control>
  <control>
    <div>num [{num}]</div>
    <input bind:value={num} type="range" min={2} max={64} step={1} />
  </control>
</controlgroup>
