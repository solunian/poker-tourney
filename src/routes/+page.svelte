<script lang="ts">
  let inputbox = $state("");
  let messages: string[] = $state([]);

  let ws = new WebSocket("ws://localhost:8000/ws/");

  // ws.onopen = () => {
  //   console.log("WebSocket open");
  // };

  ws.onmessage = (event) => {
    messages.push(event.data);
  };

  // ws.onerror = (error) => {
  //   console.error("WebSocket error:", error);
  // };

  // ws.onclose = () => {
  //   console.log("WebSocket close");
  // };
</script>

<div class="spaces-y-4 px-2">
  <h1 class="text-3xl text-orange-500">WebSocket Chat</h1>
  <form
    onsubmit={(event) => {
      event.preventDefault();
      ws.send(inputbox);
      inputbox = "";
    }}>
    <div class="flex flex-row gap-2">
      <input type="text" bind:value={inputbox} class="w-full border px-2" autocomplete="off" />
      <button class="border px-2">Send</button>
    </div>
  </form>
  <ul>
    {#each messages as m}
      <li>{m}</li>
    {/each}
  </ul>
</div>
