<script>
	export let items = []
	let newName = "";
	let newItemNumber = "";
	let newQuantity = 0;
	let newPrice = 0;
	let newBrand = "";

	function editCell(event, items, field) {
	  items[field] = event.target.innerText.trim();
	}
  
	function addItem() {
	  if (newName.trim() && newItemNumber.trim() ) {
		items = [...items, { id: items.length + 1, name: newName, itemNumber: newItemNumber, quantity: newQuantity, price: newPrice, brand: newBrand }];
		newName = "";
		newItemNumber = ""
		newQuantity = 0;
		newPrice = 0;
	  }
	}
	function deleteItem(id) {
	  items = items.filter((item) => item.id !== id);
	}

	let showModal = false;
  	let itemToDelete = null;

	const openModal = (item) => {
		itemToDelete = item;  // Store the item to be deleted
		showModal = true;      // Open the modal
	};

	const closeModal = () => {
		showModal = false;    // Close the modal without deleting
	};

  
  </script>

  <!-- Modal (Confirmation Popup) -->
{#if showModal}
<div class="fixed inset-0 flex items-center justify-center bg-opacity-80 transition">
  <div class="bg-white rounded-lg p-6 w-80  bg-opacity-70 transition">
	<h2 class="text-lg font-semibold">Are you sure you want to delete "{itemToDelete.name}"?</h2>
	<div class="mt-4 flex justify-between">
	  <button 
		class="bg-gray-500 text-white px-4 py-2 rounded-md hover:bg-gray-600"
		on:click={closeModal}>
		Cancel
	  </button>
	  <button 
		class="bg-red-500 text-white px-4 py-2 rounded-md hover:bg-red-600"
		on:click={deleteItem(itemToDelete.id),closeModal}>
		Delete
	  </button>
	</div>
  </div>
</div>
{/if}

  <!-- Add Row Form -->
	<div class="flex gap-2 m-0 p-0 items-center jus">
		<input bind:value={newItemNumber} placeholder="Item Number" class="border px-4 py-2 rounded-md" />
	  	<input bind:value={newName} placeholder="Name" class="border px-4 py-2 rounded-md" />
	  	<input bind:value={newQuantity} placeholder="quantity" class="border px-4 py-2 rounded-md" />
	  	<button on:click={addItem} class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600">
		Add Item
	  </button>
	</div>
  
  <div class="overflow-x-auto hide-scrollbar p-4 flex flex-col gap-4 max-h-[80vh] w-full">
	
	<table class="w-full border-collapse rounded-xl  border-separate border-spacing-y-2" >
	  <thead class="sticky top-0 bg-gray-800 text-white text-left ">
		<tr class=" text-Black text-left ">
			{#each Object.keys(items[0]) as key}
			<th class="px-4 py-2">{key.replace("_"," ")}</th>
			{/each}
			<th class="px-6 py-3">Action</th>
		</tr>
	  </thead>
	  
	  <tbody>
		{#each items as item, i}
		  	<tr class="bg-gray-200 hover:bg-gray-300 transition ">

				{#each Object.values(item) as value}
					<td 
					class="px-6 py-3 focus:outline-none cursor-pointer"
					contenteditable="true"
					on:blur={(e) => editCell(e, item, {value})}
					on:keydown={(e) => e.key === 'Enter' && e.target.blur()}>
					{value}
					</td>
				{/each}
				

				<td class="px-6 py-3">
					<button 
						on:click={() => openModal(item)}
						class="bg-red-500 text-white px-3 py-1 rounded-md hover:bg-red-700">
						Delete
					</button>
				</td>
		  </tr>
		{/each}
	  </tbody>
	</table>
  

  </div>
  <style>
	.hide-scrollbar::-webkit-scrollbar {
	display: none;
	}
	.hide-scrollbar {
	-ms-overflow-style: none;  /* for Internet Explorer */
	scrollbar-width: none;  /* for Firefox */
	}
  </style>