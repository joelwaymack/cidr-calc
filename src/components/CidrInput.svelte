<script lang="ts">
	import type { Cidr } from '../types';

	export let cidr: Cidr;

	const inputChange = (event) => {
		const target = event.target.name;
		let value = event.target.valueAsNumber;
		value = !value || value === NaN || value < 0 ? 0 : value;

		if (target === 'mask') {
			value = value > 32 ? 32 : value;
			cidr.mask = value;
		} else {
			value = value > 255 ? 255 : value;
			cidr.octets[target] = value;
		}
	};
</script>

<div class="cidr-input">
	{#each cidr.octets as o, octet}
		<input type="number" name={octet.toString()} bind:value={cidr.octets[octet]} on:input|capture={inputChange} />
		{#if octet != cidr.octets.length - 1}
			<div>.</div>
		{/if}
	{/each}
	<div>/</div>
	<input type="number" name="mask" bind:value={cidr.mask} on:input|capture={inputChange} />
</div>

<style type="text/scss">
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

	.cidr-input {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		align-items: baseline;
		gap: .5em;
	}
</style>