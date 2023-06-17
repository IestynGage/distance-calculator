<script lang="ts">
  export let units;
  export let pacePerHour:number;
</script>

<div>
  Pace:
  <input bind:value={pacePerHour} />
  units
  <select bind:value={units}>
    <option>Mph</option>
    <option>Kph</option>
  </select>
</div>

