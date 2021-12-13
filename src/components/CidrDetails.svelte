<script lang="ts">
    import type { Cidr } from '../types';
    import { Netmask } from 'netmask';
    
    export let cidr: Cidr;
    $: netmask = new Netmask(`${cidr.octets[0]}.${cidr.octets[1]}.${cidr.octets[2]}.${cidr.octets[3]}/${cidr.mask}`);
</script>

<div class="cidr-details">
    <table>
        <tr>
            <th>Bit mask:</th>
            <td>{netmask.mask}</td>
        </tr>
        <tr>
            <th>First address:</th>
            <td>{netmask.first}</td>
        </tr>
    </table>
    <table>
        <tr>
            <th>Addresses:</th>
            <td>{netmask.size}</td>
        </tr>
        <tr>
            <th>Last address:</th>
            <td>{netmask.last}</td>
        </tr>
    </table>
</div>

<style type="text/scss">
    .cidr-details {
        display: flex;
        gap: 3em;
        justify-content: center;

        th {
            text-align: right;
        }
    }
</style>