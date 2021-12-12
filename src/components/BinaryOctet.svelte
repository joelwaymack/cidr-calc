<script lang="ts">
    import type { Cidr } from "../types";

    export let cidr: Cidr;
    export let octet: number;

    const convertToBinary = (number: number): string => {
        let binary = '';
        for(let bit = 0; bit < 8; bit++) {
            binary += ((number & (1 << (7 - bit))) >> (7 - bit));
        }
        return binary;
    };

    $: binary = convertToBinary(cidr.octets[octet]);
</script>

<ol>
    {#each binary as bit}
        <li>{bit}</li>
    {/each}
</ol>

<style type="text/scss">
    ol {
        padding-inline-start: 0;
        font-size: 6px;

        li {
            display: inline;
            border: 1px black solid;
            list-style-type: none;
            padding: 0.4em 0.6em;
        }
    }
</style>