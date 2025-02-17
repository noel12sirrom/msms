
<svelte:head>
	<title>Employees</title>
	<meta name="description" content="About this app" />
</svelte:head>

<script>
	import Tble from '$lib/components/Tble.svelte';
	let users = [
		{ ID: 1, Status: "Active", Name: "Alice", Role: ["Cashier", "Manager"], Contact_Number: "1876 2514811", DOB: "15-05-2003", Email: "alice@example.com" },
		{ ID: 2, Status: "Inactive", Name: "Bob", Role: "Technician", Contact_Number: "1876 2514811", DOB: "02-12-1997", Email: "bob@example.com" },
		{ ID: 3, Status: "Active", Name: "Charlie", Role: "Mechanic", Contact_Number: "1876 2514811", DOB: "01-03-1874", Email: "charlie@example.com" },
		{ ID: 4, Status: "Inactive", Name: "David", Role: "Technician", Contact_Number: "1876 2514811", DOB: "27-09-1943", Email: "david@example.com" },
		{ ID: 5, Status: "Active", Name: "Emma", Role: ["Cashier", "Sales"], Contact_Number: "1876 2514812", DOB: "18-07-1985", Email: "emma@example.com" },
		{ ID: 6, Status: "Inactive", Name: "Frank", Role: "Manager", Contact_Number: "1876 2514813", DOB: "11-11-1980", Email: "frank@example.com" },
		{ ID: 7, Status: "Active", Name: "Grace", Role: "Mechanic", Contact_Number: "1876 2514814", DOB: "25-03-1992", Email: "grace@example.com" },
		{ ID: 8, Status: "Inactive", Name: "Hannah", Role: ["Manager", "Technician"], Contact_Number: "1876 2514815", DOB: "07-01-1987", Email: "hannah@example.com" },
		{ ID: 9, Status: "Active", Name: "Ivy", Role: "Customer Support", Contact_Number: "1876 2514816", DOB: "22-10-1990", Email: "ivy@example.com" },
		{ ID: 10, Status: "Inactive", Name: "James", Role: "Technician", Contact_Number: "1876 2514817", DOB: "03-05-1994", Email: "james@example.com" },
		{ ID: 11, Status: "Active", Name: "Kara", Role: ["Sales", "Customer Support"], Contact_Number: "1876 2514818", DOB: "13-09-1996", Email: "kara@example.com" },
		{ ID: 12, Status: "Active", Name: "Leo", Role: "Mechanic", Contact_Number: "1876 2514819", DOB: "20-06-1988", Email: "leo@example.com" },
		{ ID: 13, Status: "Inactive", Name: "Mia", Role: "Sales", Contact_Number: "1876 2514820", DOB: "30-01-1993", Email: "mia@example.com" },
		{ ID: 14, Status: "Active", Name: "Nina", Role: "Technician", Contact_Number: "1876 2514821", DOB: "17-02-1991", Email: "nina@example.com" },
		{ ID: 15, Status: "Inactive", Name: "Oscar", Role: "Manager", Contact_Number: "1876 2514822", DOB: "12-04-1982", Email: "oscar@example.com" },
		{ ID: 16, Status: "Active", Name: "Paul", Role: "Mechanic", Contact_Number: "1876 2514823", DOB: "23-08-1975", Email: "paul@example.com" },
		{ ID: 17, Status: "Inactive", Name: "Quinn", Role: "Sales", Contact_Number: "1876 2514824", DOB: "05-12-1989", Email: "quinn@example.com" },
		{ ID: 18, Status: "Active", Name: "Rachel", Role: "Customer Support", Contact_Number: "1876 2514825", DOB: "14-06-1984", Email: "rachel@example.com" },
		{ ID: 19, Status: "Inactive", Name: "Sam", Role: "Technician", Contact_Number: "1876 2514826", DOB: "09-09-1990", Email: "sam@example.com" },
		{ ID: 20, Status: "Active", Name: "Tina", Role: "Manager", Contact_Number: "1876 2514827", DOB: "16-02-1986", Email: "tina@example.com" }
	];

  </script>

  <!-- Modal (Confirmation Popup) -->
  <div class="flex gap-2 m-0 p-0 items-center justify-between m-5 w-[90%]">
	<h1 class="text-4xl font-semibold text-left w-[88%] ">Employees</h1>
	<button class="bg-orange-500 text-white px-4 py-2 rounded-md hover:bg-orange-600">
		Log out
	</button>
</div>
  <Tble items={users} tableName="Employee" />