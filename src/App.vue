<script setup lang="ts">
import {onMounted} from "vue";
import Arweave from "arweave";
import {LoggerFactory, Warp, WarpWebFactory} from "warp-contracts";

onMounted(async () => {
  // Set up Arweave client
  const arweave: Arweave = Arweave.init({
    host: "localhost",
    port: 1984,
    protocol: "http",
  });

  const wallet = await arweave.wallets.generate();

  const walletAddress = await arweave.wallets.getAddress(wallet);
  await arweave.api.get(`/mint/${walletAddress}/1000000000000000`);

  LoggerFactory.INST.logLevel('debug');

  const warp: Warp = new WarpWebFactory.memCached(arweave);
  // const warp: Warp = WarpWebFactory.memCachedBased(arweave).useArweaveGateway().build();
});
</script>

<template>
</template>