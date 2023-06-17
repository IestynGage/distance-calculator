<script lang="ts">
  import Pace from './Pace.svelte'
  import Time from './Time.svelte'
  import Result from './Result.svelte'
  import type { Units } from '../types/units.type'

  const CONVERT_HOUR_TO_SECOND:number = 3600;
  const CONVERT_MINUTE_TO_SECOND:number = 60;

  let units:Units;
  let pacePerHour:string | undefined;
  let time:string | undefined;

  $: distance = calculateDistance(Number.parseInt(pacePerHour), time);
  $: validationMessages = validateInput(pacePerHour, time);

  /*
  * Converts string `hour:minute:second' to seconds
  */
  function convertTimeToSeconds(time?:string): number | null {
    if (time) {
      const hourInSeconds = Number.parseInt(time.slice(0,2)) * CONVERT_HOUR_TO_SECOND;
      const minuteInSeconds = Number.parseInt(time.slice(3,5)) * CONVERT_MINUTE_TO_SECOND;
      const seconds = Number.parseInt(time.slice(6,9));

      return hourInSeconds + minuteInSeconds + seconds; 
    }

    return null;
  }

  function calculateDistance(pacePerHour?:number, time?:string): number | undefined {
    if( pacePerHour === undefined || Number.isNaN(pacePerHour) || time === undefined) {
      return undefined;
    }

    let pacePerSecond = (pacePerHour ?? 0) / CONVERT_HOUR_TO_SECOND;
    let timeInSeconds = convertTimeToSeconds(time);

    return pacePerSecond * timeInSeconds;
  }

  function validateInput(pacePerHour, time) {
    let validationMessages = [];

    if (pacePerHour === "" || pacePerHour === undefined) {
      validationMessages.push("You need to insert value into pace.");
    } 
    else if (Number.isNaN(Number.parseInt(pacePerHour))) {
      validationMessages.push("You can not insert a character other than a number as pace.");
    }
    if (time === undefined) {
      validationMessages.push("You need to insert value into duration");
    }

    return validationMessages;
  }
</script>

<div>
  <Pace bind:pacePerHour={pacePerHour} bind:units={units}/>
  <br />
  <Time bind:time={time}/>
	{#each validationMessages as message, i}
  <p class="secondary">{message}</p>
  {/each}
  <Result bind:distance={distance} bind:units={units}/>
</div>