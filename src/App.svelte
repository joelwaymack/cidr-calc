<script lang="ts">
	import Octet from './components/Octet.svelte';

	let cidr = 	{
		octet1: 0,
		octet2: 0,
		octet3: 0,
		octet4: 0,
		mask: 0
	};

	const inputChange = (event) => {
		const target = event.target.name;
		let value = event.target.valueAsNumber;
		console.log(value);
		value = !value || value < 0 ? 0 : value;

		if (target === 'mask') {
			value = value > 32 ? 32 : value;
		} else {
			value = value > 255 ? 255 : value;
		}
		console.log(value);
		cidr[target] = value;
	};
</script>

<div class="ip">
	<input type="number" name="octet1" bind:value={cidr.octet1} on:input={inputChange} />
	<div class="dot">.</div>
	<input type="number" name="octet2" bind:value={cidr.octet2} on:input={inputChange} />
	<div class="dot">.</div>
	<input type="number" name="octet3" bind:value={cidr.octet3} on:input={inputChange} />
	<div class="dot">.</div>
	<input type="number" name="octet4" bind:value={cidr.octet4} on:input={inputChange} />
	<div class="dot">/</div>
	<input type="number" name="mask" bind:value={cidr.mask} on:input={inputChange} />
</div>

<div class="ip">
	<Octet value={cidr.octet1} />
	<div>.</div>
	<Octet value={cidr.octet2} />
	<div>.</div>
	<Octet value={cidr.octet3} />
	<div>.</div>
	<Octet value={cidr.octet4} />
	<div>/</div>
	<div>{cidr.mask}</div>
</div>

<style>
	input {
		width: 3rem;
		text-align: center;
	}

	input::-webkit-outer-spin-button,
	input::-webkit-inner-spin-button {
		-webkit-appearance: none;
		margin: 0;
	}

	input[type=number] {
		-moz-appearance: textfield;
	}

	.ip {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		align-items: baseline;
		gap: .5rem;
	}

	.dot {
		font-size: 2rem;
	}
</style>