<script lang="ts">
  import Pace from './Pace.svelte'
  import Time from './Time.svelte'
  import Result from './Result.svelte'

  let units;
  let pacePerHour:number;
  let time:string | undefined;
  const convertHourToSecond:number = 3600;
  const convertMinuteToSecond:number = 60;
  $: pacePerSecond = (pacePerHour ?? 0) / convertHourToSecond;
  $: timeInSeconds = convertTimeToSeconds(time);
  $: console.log('timeInSeconds', timeInSeconds);
  $: distance = calculateDistance(pacePerSecond, timeInSeconds);

  /*
  * Converts string `hour:minute:second' to seconds
  */
  function convertTimeToSeconds(time?:string): number | null {
    if (time) {
      const hourInSeconds = Number.parseInt(time.slice(0,2)) * convertHourToSecond;
      const minuteInSeconds = Number.parseInt(time.slice(3,5)) * convertMinuteToSecond;
      const seconds = Number.parseInt(time.slice(6,9));

      return hourInSeconds + minuteInSeconds + seconds; 
    }

    return null;
  }

  function calculateDistance(pace:number | null, distance:number | null): number | null {
    return pace * distance;
  }
</script>

<div>
  <Pace bind:pacePerHour={pacePerHour} bind:units={units}/>
  <Time bind:time={time}/>
  <Result bind:distance={distance} bind:units={units}/>
</div>