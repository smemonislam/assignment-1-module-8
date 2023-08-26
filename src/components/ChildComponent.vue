<script setup>
import { reactive, onBeforeUpdate } from "vue";
import SingleInput from "./SingleInput.vue";
// DefineProps
const props = defineProps(["total"]);

// defineEmits
defineEmits(["update:modelValue", "messageEmitted"]);

// const data = reactive({
//   name: "",
//   phone: "",
//   address: "",
// });

let data = reactive([
  {
    name: "",
    type: "text",
    placeholder: "Name",
  },
  {
    name: "",
    type: "tel",
    placeholder: "Number",
  },
  {
    name: "",
    type: "text",
    placeholder: "Address",
  },
  {
    name: "",
    type: "text",
    placeholder: "Total Amount",
  },
]);

onBeforeUpdate(() => {
  data[3].name = props.total;
});
function onSubmit() {
  // let orderDetails2 = {
  //   // name: data[0].name,
  //   // phone: data[1].name,
  //   // address: data[2].name,
  //   // total: data[3].name,
  //   // address: data.address,
  //   total: props.modelValue,
  // };

  let orderDetails = [];
  data.forEach((element) => {
    orderDetails.push(element.name);
  });

  console.log(orderDetails);
  // console.log(orderDetails2);
}
</script>
<template>
  <div id="modal">
    <div class="backdrop" @click="$emit('messageEmitted')"></div>
    <div class="modalBody">
      <div class="formContainer" id="orderForm">
        <h1>Complete the form below and hit submit</h1>
        <p>{{ data }}</p>
        <p>{{ total }}</p>
        <form class="orderForm" @submit.prevent="onSubmit">
          <ul>
            <li v-for="(item, index) in data" :key="index">
              <SingleInput
                v-model="item.name"
                :type="item.type"
                :placeholder="item.placeholder"
              />
              <!-- <input
                type="text"
                class="fieldStyle fieldSplit alignLeft"
                placeholder="Name"
                v-model="data.name"
              /> -->
              <!-- <input
                type="text"
                class="fieldStyle fieldSplit alignRight"
                placeholder="Phone no."
                v-model="data.phone"
              /> -->
            </li>
            <li>
              <!-- <input
                type="text"
                class="fieldStyle fieldSplit alignRight"
                :value="modelValue"
                @input="$emit('update:modelValue', $event.target.value)"
              /> -->
            </li>
            <li>
              <!-- <textarea
                class="fieldStyle"
                placeholder="Address"
                v-model="data.address"
              ></textarea> -->
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
