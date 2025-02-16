<script>
  export let show = false;
  export let title = "Confirm Action";
  export let item = {};
  export let message = "Are you sure you want to proceed?";
  export let onCancel = () => {};
  export let onConfirm = () => {};

  
</script>

{#if show}
  <div class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50">
    <div class="bg-white rounded-lg p-6 w-80 shadow-lg">
      <h2 class="text-lg font-semibold">{title}</h2>
      <p class="mt-2 text-gray-600">{message}</p>
      <div class="mt-4 flex justify-between">
        <button 
          class="bg-gray-500 text-white px-4 py-2 rounded-md hover:bg-gray-600"
          on:click={onCancel}>
          Cancel
        </button>
        <button 
          class="bg-red-500 text-white px-4 py-2 rounded-md hover:bg-red-600"
          on:click={onConfirm}>
          Confirm
        </button>
      </div>
    </div>
  </div>
{/if}
