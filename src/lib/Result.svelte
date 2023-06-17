<script lang="ts">
  let count: number = undefined;
  export let units;
  export let distance: number | null = null;

  const roundDp:number = 1000;
</script>

<p> You ran {distance ? Math.round(distance * roundDp) / roundDp : "???"} {units === 'Mph'? 'miles' : 'kilometers'}.</p>
