<template>
  <section class="flex gap-x-4">
    <fwb-button>Edad Promedio: {{ avgAge }}</fwb-button>
    <fwb-button>Hombres: {{ mens }}</fwb-button>
    <fwb-button>Mujeres: {{ womens }}</fwb-button>
    <fwb-button>Menor edad: {{ youngest }}</fwb-button>
    <fwb-button>Mayor edad: {{ oldest }}</fwb-button>
  </section>
</template>

<script setup>
import { FwbButton } from "flowbite-vue";
import { computed } from "vue";

// props
const { users } = defineProps(["users"]);

const avgAge = computed(
  () => users.reduce((acc, user) => acc + user.age, 0) / users.length
);

const womens = computed(() => users.filter((user) => user.sex === "F").length);

const mens = computed(() => users.filter((user) => user.sex === "M").length);

const youngest = computed(() =>
  users.reduce((acc, user) => Math.min(acc, user.age), Infinity)
);

const oldest = computed(() =>
  users.reduce((acc, user) => Math.max(acc, user.age), 0)
);
</script>
