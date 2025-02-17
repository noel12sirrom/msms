<script>
  export let show = false;
  export let title = "Confirm Action";
  export let message = "Are you sure you want to proceed?";
  export let itemList = null; 
  export let onCancel = () => {};
  export let onConfirm = () => {};
  export let newEmployee = {
    Name: "",
    Status: "Active",
    Role: [],
    Contact_Number: "",
    DOB: "N/A",
    Email: "N/A",
  };
  export let newPart = {
    Name: "",
    Part_Number: "",
    Quantity: 0,
    Price: 0,
    Brand: "N/A",
  };

  let availableRoles = ["Cashier", "Manager", "Technician", "Mechanic", "Sales", "Customer Support"];
  
  function toggleRole(role) {
    if (newEmployee.Role.includes(role)) {
      newEmployee.Role = newEmployee.Role.filter(r => r !== role);
    } else {
      newEmployee.Role = [...newEmployee.Role, role];
    }
  }
</script>

{#if show}
  <div class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50">
    <div class="bg-white rounded-lg p-6 w-80 shadow-lg">
      <h2 class="text-lg font-semibold">{title}</h2>
      <p class="mt-2 text-gray-600">{message}</p>
      {#if title === "Add Employee"}
        <p class="mt-2 text-gray-600">Fill in the details to add a new employee.</p>
        <div class="mt-4 space-y-3">
          <div>
            <label for="name" class="block text-sm font-medium text-gray-700">Name <span class="text-red-500">*</span></label>
            <input 
              id="name"
              type="text" 
              bind:value={newEmployee.Name} 
              placeholder="Enter name" 
              class="w-full border border-orange-300 border-gray-300 px-4 py-2 rounded-md focus:ring-2 focus:ring-orange-400 focus:outline-none" required/>
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700">Contact Number <span class="text-red-500">*</span></label>
            <input 
              type="text" 
              bind:value={newEmployee.Contact_Number} 
              placeholder="Enter contact number" 
              class="w-full border border-orange-300 border-gray-300 px-4 py-2 rounded-md focus:ring-2 focus:ring-orange-400 focus:outline-none" required/>
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700">Email</label>
            <input 
              type="email" 
              bind:value={newEmployee.Email} 
              placeholder="Enter email" 
              class="ww-full border border-orange-300 border-gray-300 px-4 py-2 rounded-md focus:ring-2 focus:ring-orange-400 focus:outline-none" />
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700">Date of Birth</label>
            <input 
              type="date" 
              bind:value={newEmployee.DOB} 
              class="w-full border border-orange-300 border-gray-300 px-4 py-2 rounded-md focus:ring-2 focus:ring-orange-400 focus:outline-none" />
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700">Role</label>
            <div class="flex flex-wrap gap-2">
              {#each availableRoles as role}
                <button 
                  class="px-3 py-1 rounded-md border {newEmployee.Role.includes(role) ? 'bg-orange-500 text-white' : 'bg-gray-200 text-gray-700'}"
                  on:click={() => toggleRole(role)}>
                  {role}
                </button>
              {/each}
            </div>
          </div>
        </div>
      {/if}


      {#if title === "Add Part"}
        <p class="mt-2 text-gray-600">Fill in the details to add a new part.</p>
        <div class="mt-4 space-y-3">
          <div>
            <label for="name" class="block text-sm font-medium text-gray-700">Name *</label>
            <input 
              id="name"
              type="text" 
              bind:value={newPart.Name} 
              placeholder="Enter name" 
              class="w-full border border-orange-300 px-4 py-2 rounded-md focus:ring-2 focus:ring-orange-400 focus:outline-none" required/>
          </div>

          <div>
            <label class="block  text-sm font-medium text-gray-700">Part Number *</label>
            <input 
              type="text" 
              bind:value={newPart.Part_Number} 
              placeholder="Enter part number" 
              class="w-full border border-orange-300 px-4 py-2 rounded-md focus:ring-2 focus:ring-orange-400 focus:outline-none" />
          </div>

          <div>
            <label class="block  text-sm font-medium text-gray-700">Quantity</label>
            <input 
              type="number" 
              bind:value={newPart.Quantity} 
              placeholder="Enter quantity" 
              class="w-full border border-orange-300 border-gray-300 px-4 py-2 rounded-md focus:ring-2 focus:ring-orange-400 focus:outline-none" />

          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700">Price</label>
            <input 
              type="number" 
              bind:value={newPart.Price} 
              placeholder="Enter price" 
              class="w-full border border-orange-300 border-gray-300 px-4 py-2 rounded-md focus:ring-2 focus:ring-orange-400 focus:outline-none" />
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700">Brand</label>
            <input 
              type="text" 
              bind:value={newPart.Brand} 
              placeholder="Enter brand" 
              class="w-full border border-orange-300 border-gray-300 px-4 py-2 rounded-md focus:ring-2 focus:ring-orange-400 focus:outline-none" />
          </div>
        </div> 
      {/if}
      
      
      <div class="mt-4 flex justify-between">
        <button 
          class="bg-gray-500 text-white px-4 py-2 rounded-md hover:bg-gray-600"
          on:click={onCancel}>
          Cancel
        </button>
        <button 
          class="bg-red-500 text-white px-4 py-2 rounded-md hover:bg-red-600"
          on:click={()=> {
            if(newPart.Name && newPart.Part_Number || newEmployee.Name && newEmployee.Contact_Number || title === "Delete Item"){
              onConfirm()
            }
            }}>
          Confirm
        </button>
      </div>
    </div>
  </div>
{/if}
