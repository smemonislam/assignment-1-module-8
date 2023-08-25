<script setup>
import { reactive } from "vue";
// DefineProps
const props = defineProps(["modelValue"]);

// defineEmits
defineEmits(["update:modelValue", "messageEmitted"]);

const data = reactive({
  name: "",
  phone: "",
  address: "",
});

function onSubmit() {
  let orderDetails = {
    name: data.name,
    phone: data.phone,
    address: data.address,
    total: props.modelValue,
  };

  console.log(orderDetails);
}
</script>
<template>
  <div id="modal">
    <div class="backdrop" @click="$emit('messageEmitted')"></div>
    <div class="modalBody">
      <div class="formContainer" id="orderForm">
        <h1>Complete the form below and hit submit</h1>
        <form class="orderForm" @submit.prevent="onSubmit">
          <ul>
            <li>
              <input
                type="text"
                class="fieldStyle fieldSplit alignLeft"
                placeholder="Name"
                v-model="data.name"
              />
              <input
                type="text"
                class="fieldStyle fieldSplit alignRight"
                placeholder="Phone no."
                v-model="data.phone"
              />
            </li>
            <li>
              <input
                type="hidden"
                class="fieldStyle fieldSplit alignRight"
                :value="modelValue"
                @input="$emit('update:modelValue', $event.target.value)"
              />
            </li>
            <li>
              <textarea
                class="fieldStyle"
                placeholder="Address"
                v-model="data.address"
              ></textarea>
            </li>
            <li>
              <input type="submit" value="Submit" />
            </li>
          </ul>
        </form>
      </div>
    </div>
  </div>
</template>
