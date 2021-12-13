<script lang="ts">
    import type { Cidr } from '../types';
    import BinaryOctet from './BinaryOctet.svelte';
    
    export let cidr: Cidr;
</script>

<div class="binary-block">
    {#each cidr.octets as o, octet}
        <BinaryOctet {cidr} {octet} />
        {#if octet != cidr.octets.length - 1}
            <div>.</div>
        {/if}
    {/each}
</div>

<style type="text/scss">
	.binary-block {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		align-items: baseline;
		gap: .5rem;
	}
</style>