<script>
  import Progress from "./Progress.svelte";

  let total_time = 20;

  let second_left = total_time;

  let isRunning = false;
  $: progress = ((total_time - second_left) / total_time) * 100;

  function startTimer() {
    isRunning = true;
    const timer = setInterval(() => {
      second_left -= 1;
      if (second_left === 0) {
        clearInterval(timer);
        isRunning = false;
        second_left = total_time;
      }
    }, 1000);
  }
</script>

<div bp="grid">
  <h2 bp="offset-5@md 4@md 12@sm">Seconds Left:{second_left}</h2>
</div>

<Progress {progress} />
<div bp="grid">
  <button
    bp="offset-5@md 4@md 12@sm"
    class={`start ${isRunning && "disabled"}`}
    on:click={startTimer}
    disabled={isRunning}
  >
    Start
  </button>
</div>
