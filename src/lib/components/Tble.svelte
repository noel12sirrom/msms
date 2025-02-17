<script>
	import Modal from "$lib/components/Modal.svelte";
	
	export let items = []
	export let tableName = "Table"

	let modalTitle = "";
	let modalMessage = "";
	let showModal = false;
  	let itemToDelete = null;

	let  newEmployee = {Name: "",Status: "Active",Role: [],Contact_Number: "",DOB: "",Email: "",};
	let newPart = {Name: "",Part_Number: "",Quantity: 0,Price: 0,Brand: "",};



	function editCell(event, items, field) {
	  items[field] = event.target.innerText.trim();
	}
	
	function addItem() {
    if (modalTitle === "Add Employee") {
        if (newEmployee.Name.trim() && newEmployee.Contact_Number.trim()) {
            items = [...items,
                {
                    ID: items.length + 1,
					Status: "Active",
                    Name: newEmployee.Name,
                    Role: [...newEmployee.Role], // Assuming this is an array
                    Contact_Number: newEmployee.Contact_Number,
					DOB: newEmployee.DOB,
					Email: newEmployee.Email
                }
            ];
            // Reset form fields
            newEmployee = { Name: "", Status: "", Role: [], Contact_Number: "" };
        }
    } else if (modalTitle === "Add Part") {
        if (newPart.Name.trim() && newPart.Part_Number.trim()) {
            items = [...items,
                {
                    ID: items.length + 1,
                    Name: newPart.Name,
                    Part_Number: newPart.Part_Number,
                    Quantity: newPart.Quantity,
                    Price: newPart.Price,
					Brand: newPart.Brand
                }
            ];
            // Reset form fields
            newPart = { Name: "", Part_Number: "", Quantity: 0, Price: 0 };
        }
    }
	closeModal();
}

	function deleteItem() {
		console.log("deleteITem func called");
	if(itemToDelete){
	  	items = items.filter((item) => item.ID !== itemToDelete.ID);
	  	console.log("Deleted:", itemToDelete);
		itemToDelete = null;  // Reset selected item
	}
	  showModal = false;
	}

	
	function openModal(option) {
		if(option== "delete"){
			modalTitle = "Delete Item";
			console.log("itemToDelete", itemToDelete);
			modalMessage = `Are you sure you want to delete "${itemToDelete?.Name}"?`;
		}
		else if(option== "add"){
			if(tableName == "Employee"){
				modalTitle = "Add Employee";
			}
			else if(tableName == "Inventory"){
				modalTitle = "Add Part";
			}
			modalMessage = "";
					
		}
		
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
	title={modalTitle}
  	itemList = {items}
	message={modalMessage}
	{newEmployee}
	{newPart}
	onCancel={closeModal}
	onConfirm={() => {
		console.log("onconfirm clicked");
		if (modalTitle == "Add Employee"){
			addItem(newEmployee);
		}else if (modalTitle == "Add Part"){
			addItem(newPart);
		}else if (modalTitle == "Delete Item"){
			deleteItem()
		}}} />

  
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
					{#if value =='Active'|| value =='Inactive'}
						<td class="px-6 py-3">
							<button 
								on:click={() => {item.Status = item.Status === 'Active' ? 'Inactive' : 'Active'}}
								class="px-2 py-0.5 rounded-md text-white font-medium transition duration-200 hover:opacity-80"
								class:bg-green-500 ={item.Status === 'Active'} 
								class:bg-slate-500={item.Status !== 'Active'}>
								{item.Status}
							</button>
						</td>
					{:else}
					<td 
					class="px-6 py-5 focus:outline-none cursor-pointer"
					contenteditable="true"
					on:blur={(e) => editCell(e, item, {value})}
					on:keydown={(e) => e.key === 'Enter' && e.target.blur()}
					>
					{value}
					</td>
					{/if}
					
				{/each}
				

				<td class="px-6 py-5 flex gap-2">
					<button 
						on:click={() => {itemToDelete = item; openModal("delete") }}
						class=" text-red-400  hover:text-red-600 hover:scale-150 text-center text-2xl transition duration-200">
						&times;
					</button>
				</td>
			</tr>
		{/each}
		</tbody>
	</table>
	<button on:click={() => openModal("add")} class="sticky bottom-0 left-[93%] w-5 h-5 px-7 py-7 bg-orange-500 text-white text-4xl rounded-full hover:bg-orange-600 flex justify-center items-center ">
		&#43;
	</button>
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