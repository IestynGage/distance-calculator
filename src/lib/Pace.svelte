<script lang="ts">
  import type { Units } from '../types/units.type'

  export let units:Units;
  export let pacePerHour:string;
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

