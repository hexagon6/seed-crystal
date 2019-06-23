<script>
  export let hexes,
    fill,
    rotation = 0,
    radius,
    distance,
    strokemod,
    stroke;
  $: num = hexes.length;
  $: strokeWidth = radius / strokemod;
  $: distanceRadius = distance ? distance * radius : radius;
</script>

<g transform={`rotate(${rotation})`}>
  {#each hexes as h, i}
    <circle
      r={radius}
      cx={distanceRadius * Math.cos(h)}
      cy={distanceRadius * Math.sin(h)}
      stroke-width={strokeWidth}
      fill={fill || `rgba(127,255,255,${1 / num})`}
      {stroke} />
  {/each}
</g>
