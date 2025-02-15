
<svelte:head>
	<title>Employees</title>
	<meta name="description" content="About this app" />
</svelte:head>

<script>
	let users = [
		{ id: 1, name: "Alice", role: ["Cashier", "Manager"], contactNumber: "1876 2514811", DOB: "15-05-2003", email: "alice@example.com", status: "Active" },
		{ id: 2, name: "Bob", role: "Technician", contactNumber: "1876 2514811", DOB: "02-12-1997", email: "bob@example.com", status: "Inactive" },
		{ id: 3, name: "Charlie", role: "Mechanic", contactNumber: "1876 2514811", DOB: "01-03-1874", email: "charlie@example.com", status: "Active" },
		{ id: 4, name: "David", role: "Technician", contactNumber: "1876 2514811", DOB: "27-09-1943", email: "david@example.com", status: "Inactive" },
		{ id: 5, name: "Emma", role: ["Cashier", "Sales"], contactNumber: "1876 2514812", DOB: "18-07-1985", email: "emma@example.com", status: "Active" },
		{ id: 6, name: "Frank", role: "Manager", contactNumber: "1876 2514813", DOB: "11-11-1980", email: "frank@example.com", status: "Inactive" },
		{ id: 7, name: "Grace", role: "Mechanic", contactNumber: "1876 2514814", DOB: "25-03-1992", email: "grace@example.com", status: "Active" },
		{ id: 8, name: "Hannah", role: ["Manager", "Technician"], contactNumber: "1876 2514815", DOB: "07-01-1987", email: "hannah@example.com", status: "Inactive" },
		{ id: 9, name: "Ivy", role: "Customer Support", contactNumber: "1876 2514816", DOB: "22-10-1990", email: "ivy@example.com", status: "Active" },
		{ id: 10, name: "James", role: "Technician", contactNumber: "1876 2514817", DOB: "03-05-1994", email: "james@example.com", status: "Inactive" },
		{ id: 11, name: "Kara", role: ["Sales", "Customer Support"], contactNumber: "1876 2514818", DOB: "13-09-1996", email: "kara@example.com", status: "Active" },
		{ id: 12, name: "Leo", role: "Mechanic", contactNumber: "1876 2514819", DOB: "20-06-1988", email: "leo@example.com", status: "Active" },
		{ id: 13, name: "Mia", role: "Sales", contactNumber: "1876 2514820", DOB: "30-01-1993", email: "mia@example.com", status: "Inactive" },
		{ id: 14, name: "Nina", role: "Technician", contactNumber: "1876 2514821", DOB: "17-02-1991", email: "nina@example.com", status: "Active" },
		{ id: 15, name: "Oscar", role: "Manager", contactNumber: "1876 2514822", DOB: "12-04-1982", email: "oscar@example.com", status: "Inactive" },
		{ id: 16, name: "Paul", role: "Mechanic", contactNumber: "1876 2514823", DOB: "23-08-1975", email: "paul@example.com", status: "Active" },
		{ id: 17, name: "Quinn", role: "Sales", contactNumber: "1876 2514824", DOB: "05-12-1989", email: "quinn@example.com", status: "Inactive" },
		{ id: 18, name: "Rachel", role: "Customer Support", contactNumber: "1876 2514825", DOB: "14-06-1984", email: "rachel@example.com", status: "Active" },
		{ id: 19, name: "Sam", role: "Technician", contactNumber: "1876 2514826", DOB: "09-09-1990", email: "sam@example.com", status: "Inactive" },
		{ id: 20, name: "Tina", role: "Manager", contactNumber: "1876 2514827", DOB: "16-02-1986", email: "tina@example.com", status: "Active" },
	];
  
	let newName = "";
	let newContactNumber = "";
  
	function editCell(event, user, field) {
	  user[field] = event.target.innerText.trim();
	}
  
	function addUser() {
	  if (newName.trim() && newContactNumber.trim()) {
		users = [...users, {id: users.length + 1, name: newName, role: [], contactNumber: newContactNumber, DOB: "", email: "", status: "Active"}];
		newName = "";
		newContactNumber = "";
	  }
	}
	function deleteUser(id) {
	  users = users.filter((user) => user.id !== id);
	}

	let showModal = false;
  	let userToDelete = null;

	const openModal = (user) => {
		userToDelete = user;  // Store the part to be deleted
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
	<h2 class="text-lg font-semibold">Are you sure you want to delete "{userToDelete.name}"?</h2>
	<div class="mt-4 flex justify-between">
	  <button 
		class="bg-gray-500 text-white px-4 py-2 rounded-md hover:bg-gray-600"
		on:click={closeModal}>
		Cancel
	  </button>
	  <button 
		class="bg-red-500 text-white px-4 py-2 rounded-md hover:bg-red-600"
		on:click={deleteUser(userToDelete.id),closeModal}>
		Delete
	  </button>
	</div>
  </div>
</div>
{/if}

  <div class=" overflow-x-auto flex gap-2 m-4 items-center ">
		<input bind:value={newName} placeholder="Name" class="border px-4 py-2 rounded-md" />
		<input bind:value={newContactNumber} placeholder="Cellphone" class="border px-4 py-2 rounded-md" />
		<button on:click={addUser} class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600">
		  Add Employee
		</button>
	  </div>
  <div class="overflow-x-auto p-4 max-h-[80vh]">
	

	<table class="w-full border-collapse rounded-lg shadow-lg">
	  <thead>
		<tr class="bg-gray-800 text-white text-left">
		  <th class="px-6 py-3">ID</th>
		  <th class="px-6 py3">Status</th>
		  <th class="px-6 py-3">Name</th>
		  <th class="px-6 py-3">Role</th>
		  <th class="px-6 py-3">Contact Number</th>
		  <th class="px-6 py-3">DOB</th>
		  <th class="px-6 py-3">Email</th>
		  
		  <th class="px-6 py3"></th>
		</tr>
	  </thead>
	  <tbody>
		{#each users as user, i}
		  <tr class="border-b {i % 2 === 0 ? 'bg-gray-100' : 'bg-gray-200'} hover:bg-gray-300 transition">
			<td class="px-6 py-3">{user.id}</td>
			<td class="px-6 py-3">
				<button 
					on:click={() => {user.status = user.status === 'Active' ? 'Inactive' : 'Active'}}
					class="px-2 py-0.5 rounded-md text-white font-medium transition duration-200 hover:opacity-80"
					class:bg-green-500 ={user.status === 'Active'} 
					class:bg-slate-500={user.status !== 'Active'}>
					{user.status}
				</button>
			</td>
			<td 
			  class="px-6 py-3 focus:outline-none cursor-pointer"
			  contenteditable="true"
			  on:blur={(e) => editCell(e, user, 'name')}
			  on:keydown={(e) => e.key === 'Enter' && e.target.blur()}>
			  {user.name}			  
			</td>
			<td 
			  class="px-6 py-3 focus:outline-none cursor-pointer"
			  contenteditable="true"
			  on:blur={(e) => editCell(e, user, 'email')}
			  on:keydown={(e) => e.key === 'Enter' && e.target.blur()}>
			  {user.role}
			</td>
			<td 
			  class="px-0 py-3 focus:outline-none cursor-pointer"
			  contenteditable="true"
			  on:blur={(e) => editCell(e, user, 'contactNumber')}
			  on:keydown={(e) => e.key === 'Enter' && e.target.blur()}>
			  {user.contactNumber}
			</td>
			<td 
			  class="px-0 py-3 focus:outline-none cursor-pointer"
			  contenteditable="true"
			  on:blur={(e) => editCell(e, user, 'email')}
			  on:keydown={(e) => e.key === 'Enter' && e.target.blur()}>
			  {user.DOB}
			</td>
			<td 
			  class="px-6 py-3 focus:outline-none cursor-pointer"
			  contenteditable="true"
			  on:blur={(e) => editCell(e, user, 'email')}
			  on:keydown={(e) => e.key === 'Enter' && e.target.blur()}>
			  {user.email}
			</td>

			<td class="px-6 py-3">
				<button 
					on:click={() => openModal(user)}
					class="bg-red-400 text-white px-2 py-0.5 rounded-md hover:bg-red-700">
					Delete
				</button>
			</td>
		  </tr>
		{/each}
	  </tbody>
	</table>
  
	<!-- Add Row Form -->
	
  </div>