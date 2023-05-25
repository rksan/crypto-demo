<template>
  <TAppVue>
    <OCryptoFormVue></OCryptoFormVue>
  </TAppVue>
</template>

<script>
import { defineComponent } from "vue";
import { TAppVue } from "@/components/template";
import { OCryptoFormVue } from "@/components/organisms";

export default defineComponent({
  name: "p-crypto-page",
  components: { TAppVue, OCryptoFormVue },
});
</script>
