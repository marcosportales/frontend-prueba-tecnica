<template>
  <fwb-table class="flex-1">
    <fwb-table-head>
      <fwb-table-head-cell>Nombre</fwb-table-head-cell>
      <fwb-table-head-cell>Apellidos</fwb-table-head-cell>
      <fwb-table-head-cell>Correo</fwb-table-head-cell>
      <fwb-table-head-cell>Edad</fwb-table-head-cell>
      <fwb-table-head-cell>Sexo</fwb-table-head-cell>
      <fwb-table-head-cell>Nacionalidad</fwb-table-head-cell>
    </fwb-table-head>

    <fwb-table-body>
      <fwb-table-row v-for="user in users">
        <fwb-table-cell>{{ user.firstName }}</fwb-table-cell>
        <fwb-table-cell>{{ user.lastName }}</fwb-table-cell>
        <fwb-table-cell>{{ user.email }}</fwb-table-cell>
        <fwb-table-cell>{{ user.age }}</fwb-table-cell>
        <fwb-table-cell>{{
          user.sex === "M" ? "Masculino" : "Sexo"
        }}</fwb-table-cell>
        <fwb-table-cell>{{ user.nacionality }}</fwb-table-cell>
      </fwb-table-row>
    </fwb-table-body>
  </fwb-table>
</template>

<script setup>
import {
  FwbA,
  FwbTable,
  FwbTableBody,
  FwbTableCell,
  FwbTableHead,
  FwbTableHeadCell,
  FwbTableRow,
} from "flowbite-vue";

// props
const { users } = defineProps(["users"]);
</script>
