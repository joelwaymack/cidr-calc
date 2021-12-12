<script lang="ts">
	import BinaryBlock from './components/BinaryBlock.svelte';
	import CidrInput from './components/CidrInput.svelte';
	import Footer from './components/Footer.svelte';
	import Header from './components/Header.svelte';
	
	import type { Cidr } from './types';

	let cidr : Cidr = {
		octets: [0, 0, 0, 0],
		mask: 0
	};
</script>

<div class="box">
	<div class="content">
		<Header />
		<CidrInput bind:cidr={cidr} />
		<BinaryBlock {cidr} />
		<Footer />
	</div>
</div>

<style type="text/scss">
	.box {
		display: flex;
		justify-content: center;
	}
</style>