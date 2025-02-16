<svelte:head>
	<title>Inventory</title>
	<meta name="description" content="About this app" />
</svelte:head>

<script>
	import Tble from '$lib/components/Tble.svelte';
	let parts = [
		{ ID: 1, Name: "Brake Shoe", Part_Number: "0000A24", Quantity: 10, Price: 50, Brand: "Bosch" },
		{ ID: 2, Name: "Brake Caliper", Part_Number: "0000A25", Quantity: 15, Price: 120, Brand: "AP Racing" },
		{ ID: 3, Name: "Head Lamp", Part_Number: "0000A26", Quantity: 25, Price: 30, Brand: "Philips" },
		{ ID: 4, Name: "Tire", Part_Number: "0000A27", Quantity: 30, Price: 75, Brand: "Michelin" },
		{ ID: 5, Name: "Clutch Lever", Part_Number: "0000A28", Quantity: 5, Price: 20, Brand: "Renthal" },
		{ ID: 6, Name: "Throttle Cable", Part_Number: "0000A29", Quantity: 12, Price: 15, Brand: "Motion Pro" },
		{ ID: 7, Name: "Handlebar", Part_Number: "0000A30", Quantity: 8, Price: 35, Brand: "Pro Taper" },
		{ ID: 8, Name: "Oil Filter", Part_Number: "0000A31", Quantity: 50, Price: 12, Brand: "K&N" },
		{ ID: 9, Name: "Battery", Part_Number: "0000A32", Quantity: 20, Price: 100, Brand: "Yuasa" },
		{ ID: 10, Name: "Chain", Part_Number: "0000A33", Quantity: 18, Price: 40, Brand: "DID" },
		{ ID: 11, Name: "Spark Plug", Part_Number: "0000A34", Quantity: 40, Price: 10, Brand: "NGK" },
		{ ID: 12, Name: "Fuel Pump", Part_Number: "0000A35", Quantity: 6, Price: 85, Brand: "Walbro" },
		{ ID: 13, Name: "Seat", Part_Number: "0000A36", Quantity: 7, Price: 120, Brand: "Sargent" },
		{ ID: 14, Name: "Foot Pegs", Part_Number: "0000A37", Quantity: 14, Price: 18, Brand: "IMS" },
		{ ID: 15, Name: "Mirrors", Part_Number: "0000A38", Quantity: 22, Price: 25, Brand: "CRG" },
		{ ID: 16, Name: "Windshield", Part_Number: "0000A39", Quantity: 9, Price: 55, Brand: "National Cycle" },
		{ ID: 17, Name: "Brake Pads", Part_Number: "0000A40", Quantity: 35, Price: 45, Brand: "EBC" },
		{ ID: 18, Name: "Suspension Springs", Part_Number: "0000A41", Quantity: 4, Price: 90, Brand: "Ohlins" },
		{ ID: 19, Name: "Speedometer", Part_Number: "0000A42", Quantity: 11, Price: 150, Brand: "Veypor" },
		{ ID: 20, Name: "Fuel Tank", Part_Number: "0000A43", Quantity: 3, Price: 200, Brand: "Genuine" },
	];

</script>
<div class="flex flex-col items-center justify-center w-full">
	<div class="flex gap-2 m-0 p-0 items-center justify-between m-5 w-[90%]">
		<h1 class="text-4xl font-semibold text-left w-[88%] ">Inventory</h1>
		<button class="bg-orange-500 text-white px-4 py-2 rounded-md hover:bg-orange-600">
			Log out
		</button>
	</div>
	

	<Tble items={parts} />
</div>
