<svelte:head>
	<title>Inventory</title>
	<meta name="description" content="About this app" />
</svelte:head>

<script>
	let parts = [
		{ id: 1, name: "Brake Shoe", partNumber: "0000A24", quantity: 10, price: 5000, brand: "Bosch" },
		{ id: 2, name: "Brake Caliper", partNumber: "0000A25", quantity: 15, price: 12000, brand: "AP Racing" },
		{ id: 3, name: "Head Lamp", partNumber: "0000A26", quantity: 25, price: 3000, brand: "Philips" },
		{ id: 4, name: "Tire", partNumber: "0000A27", quantity: 30, price: 7500, brand: "Michelin" },
		{ id: 5, name: "Clutch Lever", partNumber: "0000A28", quantity: 5, price: 2000, brand: "Renthal" },
		{ id: 6, name: "Throttle Cable", partNumber: "0000A29", quantity: 1200, price: 1500, brand: "Motion Pro" },
		{ id: 7, name: "Handlebar", partNumber: "0000A30", quantity: 8, price: 3500, brand: "Pro Taper" },
		{ id: 8, name: "Oil Filter", partNumber: "0000A31", quantity: 50, price: 1200, brand: "K&N" },
		{ id: 9, name: "Battery", partNumber: "0000A32", quantity: 20, price: 10000, brand: "Yuasa" },
		{ id: 10, name: "Chain", partNumber: "0000A33", quantity: 18, price: 4000, brand: "DID" },
		{ id: 11, name: "Spark Plug", partNumber: "0000A34", quantity: 40, price: 1000, brand: "NGK" },
		{ id: 12, name: "Fuel Pump", partNumber: "0000A35", quantity: 6, price: 8500, brand: "Walbro" },
		{ id: 13, name: "Seat", partNumber: "0000A36", quantity: 7, price: 12000, brand: "Sargent" },
		{ id: 14, name: "Foot Pegs", partNumber: "0000A37", quantity: 14, price: 1800, brand: "IMS" },
		{ id: 15, name: "Mirrors", partNumber: "0000A38", quantity: 22, price: 2500, brand: "CRG" },
		{ id: 16, name: "Windshield", partNumber: "0000A39", quantity: 9, price: 5500, brand: "National Cycle" },
		{ id: 17, name: "Brake Pads", partNumber: "0000A40", quantity: 35, price: 4500, brand: "EBC" },
		{ id: 18, name: "Suspension Springs", partNumber: "0000A41", quantity: 4, price: 9000, brand: "Ohlins" },
		{ id: 19, name: "Speedometer", partNumber: "0000A42", quantity: 11, price: 15000, brand: "Veypor" },
		{ id: 20, name: "Fuel Tank", partNumber: "0000A43", quantity: 3, price: 20000, brand: "Genuine" },
	];

  
	let newName = "";
	let newPartNumber = "";
	let newQuantity = 0;
	let newPrice = 0;
	let newBrand = "";

	function editCell(event, parts, field) {
	  parts[field] = event.target.innerText.trim();
	}
  
	function addPart() {
	  if (newName.trim() && newPartNumber.trim() ) {
		parts = [...parts, { id: parts.length + 1, name: newName, partNumber: newPartNumber, quantity: newQuantity, price: newPrice, brand: newBrand }];
		newName = "";
		newPartNumber = ""
		newQuantity = 0;
		newPrice = 0;
	  }
	}
	function deletePart(id) {
	  parts = parts.filter((part) => part.id !== id);
	}

	let showModal = false;
  	let partToDelete = null;

	const openModal = (part) => {
		partToDelete = part;  // Store the part to be deleted
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
	<h2 class="text-lg font-semibold">Are you sure you want to delete "{partToDelete.name}"?</h2>
	<div class="mt-4 flex justify-between">
	  <button 
		class="bg-gray-500 text-white px-4 py-2 rounded-md hover:bg-gray-600"
		on:click={closeModal}>
		Cancel
	  </button>
	  <button 
		class="bg-red-500 text-white px-4 py-2 rounded-md hover:bg-red-600"
		on:click={deletePart(partToDelete.id),closeModal}>
		Delete
	  </button>
	</div>
  </div>
</div>
{/if}

  <!-- Add Row Form -->
	
  <div class="overflow-x-auto flex gap-2 m-4">
		<input bind:value={newPartNumber} placeholder="Part Number" class="border px-4 py-2 rounded-md" />
	  	<input bind:value={newName} placeholder="Name" class="border px-4 py-2 rounded-md" />
	  	<input bind:value={newQuantity} placeholder="quantity" class="border px-4 py-2 rounded-md" />
	  	<button on:click={addPart} class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600">
		Add Part
	  </button>
	</div>
  <div class="overflow-x-auto max-h-[80vh] p-4 ">
	
	
	<table class="w-full border-collapse rounded-lg shadow-lg">
	  <thead>
		<tr class="bg-gray-800 text-white text-left">
		  <th class="px-6 py-3">Part #</th>
		  <th class="px-6 py-3">Brand</th>
		  <th class="px-6 py-3">Name</th>
		  <th class="px-6 py-3">Quantity</th>
		  <th class="px-6 py3">Unit Price</th>
		  <th class="px-6 py3"></th>
		</tr>
	  </thead>
	  
	  <tbody>
		
		{#each parts as part, i}
		  <tr class="border-b {i % 2 === 0 ? 'bg-gray-100' : 'bg-gray-200'} hover:bg-gray-300 transition">
			
			<td 
			  class="px-6 py-3 focus:outline-none cursor-pointer"
			  contenteditable="true"
			  on:blur={(e) => editCell(e, part, 'partNumber')}
			  on:keydown={(e) => e.key === 'Enter' && e.target.blur()}>
			  {part.partNumber}
			</td>
			<td 
			  class="px-6 py-3 focus:outline-none cursor-pointer"
			  contenteditable="true"
			  on:blur={(e) => editCell(e, part, 'brand')}
			  on:keydown={(e) => e.key === 'Enter' && e.target.blur()}>
			  {part.brand}
			</td>
			<td 
			  class="px-6 py-3 focus:outline-none cursor-pointer"
			  contenteditable="true"
			  on:blur={(e) => editCell(e, part, 'name')}
			  on:keydown={(e) => e.key === 'Enter' && e.target.blur()}>
			  {part.name}
			</td>
			
			<td 
			  class="px-6 py-3 focus:outline-none cursor-pointer"
			  contenteditable="true"
			  on:blur={(e) => editCell(e, part, 'quantity')}
			  on:keydown={(e) => e.key === 'Enter' && e.target.blur()}>
			  {part.quantity}
			</td>
			<td 
			  class="px-6 py-3 focus:outline-none cursor-pointer"
			  contenteditable="true"
			  on:blur={(e) => editCell(e, part, 'quantity')}
			  on:keydown={(e) => e.key === 'Enter' && e.target.blur()}>
			  {part.price}
			</td>

			<td class="px-6 py-3">
				<button 
					on:click={() => openModal(part)}
					class="bg-red-500 text-white px-3 py-1 rounded-md hover:bg-red-700">
					Delete
				</button>
			</td>
		  </tr>
		{/each}
	  </tbody>
	</table>
  

  </div>
