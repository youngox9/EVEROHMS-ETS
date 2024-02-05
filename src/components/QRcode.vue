<template>
  <img v-if="props.value" :src="qrcode" v-bind="{ ...$attrs, ...$props }" />
</template>

<script setup>
import { useStore } from "vuex";
import { computed, ref, watch } from "vue";
import { useRouter } from "vue-router";
import { useQRCode } from "@vueuse/integrations/useQRCode";

const store = useStore();
const router = useRouter();

const src = ref(props?.value);

const props = defineProps({
  value: {
    type: String,
    default: () => {
      return "";
    },
  },
});

const qrcode = useQRCode(src || "1");

watch(
  () => props.value,
  (val, prev) => {
    src.value = val;
  },
  { deep: true, immediate: true }
);
</script>
