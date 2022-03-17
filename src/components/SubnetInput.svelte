<script lang="ts">
  import type { Cidr } from "../types";
  import { Netmask } from "netmask";

  let subnetString = "";
  const subnetRegEx = new RegExp(
    "^(([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5]).){3}([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])(/(3[0-2]|[1-2][0-9]|[0-9]))$"
  );
  $: netmask = new Netmask(
    `${cidr.octets[0]}.${cidr.octets[1]}.${cidr.octets[2]}.${cidr.octets[3]}/${cidr.mask}`
  );

  export let cidr: Cidr;

  $: subnets = subnetString
    .split("\n")
    .filter((subnet) => subnetRegEx.test(subnet.trim()));
</script>

<div class="subnet-input">
  <div>
    Add CIDR blocks below to check if they are in the block above (one per
    line):
  </div>
  <textarea bind:value={subnetString} />
  <div class="subnet-list">
    {#each subnets as subnet}
      <span
        class:in-block={netmask.contains(subnet)}
        class:not-in-block={!netmask.contains(subnet)}>{subnet}</span
      >
    {/each}
  </div>
  <div>Azure CLI command for VNet subnets:</div>
  <div class="command">
    az network vnet subnet list -g &lcub;resource_group&rcub; --vnet-name
    &lcub;vnet&rcub; --query '[].addressPrefix' -o tsv
  </div>
</div>

<style type="text/scss">
  .subnet-input {
    width: 100%;
    margin-top: 3em;

    textarea {
      width: 100%;
      margin-bottom: 0;
    }
  }

  .command {
    font-style: italic;
  }

  .subnet-list {
    .in-block {
      background-color: rgb(230, 255, 204);
      margin-right: 0.5rem;
    }

    .not-in-block {
      background-color: rgb(255, 230, 230);
      margin-right: 0.5rem;
    }

    margin-bottom: 2rem;
  }
</style>
