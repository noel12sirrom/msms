<script>
	import Modal from "$lib/components/Modal.svelte";
	/** @type {{ id: number, name: string, itemNumber: string, quantity: number, price: number, brand: string }[]} */
	export let items = []
	let newName = "";
	let newItemNumber = "";
	let newQuantity = 0;
	let newPrice = 0;
	let newBrand = "";
	
	let showModal = false;
  	let itemToDelete = null;


	function editCell(event, items, field) {
	  items[field] = event.target.innerText.trim();
	}
  
	function addItem() {
	  if (newName.trim() && newItemNumber.trim() ) {
		items = [...items,
		{ id: items.length + 1,
		name: newName,
		itemNumber: newItemNumber,
		quantity: newQuantity,
		price: newPrice,
		brand: newBrand }];
		newName = "";
		newItemNumber = ""
		newQuantity = 0;
		newPrice = 0;
	  }
	}
	function deleteItem() {
	if(itemToDelete){
	  	items = items.filter((item) => item.ID !== itemToDelete.ID);
	  	console.log("Deleted:", itemToDelete);
		itemToDelete = null;  // Reset selected item
	}
	  showModal = false;
	}

	
	function openModal(item) {
		itemToDelete = item;
		console.log(itemToDelete)  // Store the item to be deleted
		showModal = true;      // Open the modal
	};

	function closeModal() {
		showModal = false; 
		itemToDelete = null;   // Close the modal without deleting
	};
  
  </script>

  <!-- Modal (Confirmation Popup) -->
  <Modal 
	show={showModal}
	title="Delete Item"

	message={`Are you sure you want to delete "${itemToDelete?.Name}"?`}
	onCancel={closeModal}
	onConfirm={() => {deleteItem()}} />


<div class="flex gap-2 m-0 p-0 items-center justify-center m-5">
	<input bind:value={newItemNumber} placeholder="Item Number" class="border px-4 py-2 rounded-md" />
	<input bind:value={newName} placeholder="Name" class="border px-4 py-2 rounded-md" />
	<input bind:value={newQuantity} placeholder="quantity" class="border px-4 py-2 rounded-md" />
	<button on:click={addItem} class="bg-orange-500 text-white px-4 py-2 rounded-md hover:bg-orange-600">
		Add Item
	</button>
</div>
  
<div class="overflow-x-auto hide-scrollbar p-4 flex flex-col gap-4 max-h-[80vh] w-[90%]">

	<table class="w-full border-collapse rounded-xl  border-separate border-spacing-y-2" >
		<thead class="">
		<tr class=" text-Black text-left ">
			{#each Object.keys(items[0]) as key}
			<th class="px-4 py-2">{key.replace("_"," ")}</th>
			{/each}
			<th class="px-6 py-3 ">Action</th>
		</tr>
		</thead>
		
		<tbody>
		{#each items as item}
			<tr class="bg-slate-200/65 hover:bg-slate-300/65 transition ">

				{#each Object.values(item) as value}
					<td 
					class="px-6 py-5 focus:outline-none cursor-pointer"
					contenteditable="true"
					on:blur={(e) => editCell(e, item, {value})}
					on:keydown={(e) => e.key === 'Enter' && e.target.blur()}>
					{value}
					</td>
				{/each}
				

				<td class="px-6 py-5 flex gap-2">

					<button 
						on:click={() => openModal(item)}
						class=" text-red-400  hover:text-red-600 text-center text-2xl">
						x
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