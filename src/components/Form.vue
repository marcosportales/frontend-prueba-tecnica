<template>
  <form
    @submit.prevent="submit"
    class="max-w-[300px] w-full flex flex-col gap-y-4"
  >
    <div>
      <fwb-input v-model="first_name" required label="First Name" />
    </div>

    <div>
      <fwb-input
        v-model="last_name"
        required
        label="Last Name"
        class="hidden md:block"
      />
    </div>

    <div>
      <fwb-input type="email" v-model="email" required label="Correo" />
    </div>

    <div>
      <fwb-input
        type="number"
        v-model="age"
        required
        label="Edad"
        class="hidden md:block"
      />
    </div>

    <div>
      <fwb-select v-model="sex" :options="genders" label="Sexo" />
    </div>

    <fwb-button>{{ form_submitting ? "Agregando..." : "Agregar" }}</fwb-button>
  </form>
</template>

<script setup>
import axios from "axios";
import { ref } from "vue";
import { FwbInput, FwbButton, FwbSelect } from "flowbite-vue";

// props
const { add_new_user } = defineProps(["add_new_user"]);

// vars
const first_name = ref("");
const last_name = ref("");
const email = ref("");
const age = ref("");
const sex = ref("");
const form_submitting = ref(false);

// static data
const genders = [
  { value: "F", name: "Femenino" },
  { value: "M", name: "Masculino" },
];

const clear_form = () => {
  first_name.value = "";
  last_name.value = "";
  email.value = "";
  age.value = "";
  sex.value = "";
};

const getNacionality = async (fullName) => {
  form_submitting.value = true;

  const BASE_URL = "https://api.nationalize.io";
  const {
    data: { country },
  } = await axios.get(`${BASE_URL}?name=${fullName}`);

  const { countryId } = Object.entries(country).reduce(
    (acc, [_, { country_id, probability }]) => {
      return probability > acc.maxPercent
        ? { countryId: country_id, maxPercent: probability }
        : acc;
    },
    { countryId: "", maxPercent: 0 }
  );

  const countryName = await get_country(countryId);
  form_submitting.value = false;

  return await countryName;
};

const get_country = async (countryId) => {
  const url = `https://restcountries.com/v3.1/alpha/${countryId}`;
  const { data } = await axios.get(url);
  const { common } = data[0].name;
  return common;
};

const submit = async () => {
  const user = {
    firstName: first_name.value,
    lastName: last_name.value,
    email: email.value,
    age: age.value,
    sex: sex.value,
    nacionality: await getNacionality(`${first_name.value} ${last_name.value}`),
  };

  add_new_user(user);
  clear_form();
};
</script>
