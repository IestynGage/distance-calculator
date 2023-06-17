<script lang="ts">
  export let time:string;
</script>

<div>
  Time: <input id="settime" type="time" step="1" bind:value={time}/>
</div>