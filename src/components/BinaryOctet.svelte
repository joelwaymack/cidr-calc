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
    {#each binary as bit, index}
        <li class:masked={cidr.mask - (octet * 8) - index <= 0}>{bit}</li>
    {/each}
</ol>

<style type="text/scss">
    ol {
        padding-inline-start: 0;
        font-size: 12px;

        li {
            display: inline;
            border: 1px black solid;
            list-style-type: none;
            padding: 0.2em 0.3em;

            &.masked {
                background-color: lightgray;
            }
        }
    }
</style>