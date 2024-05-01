<template>
  <div class="content">
    <span class="header">{{ props.item.name }}</span>

    <div class="detail" v-for="attr in props.item.attributes" :key="attr?.code">
      <div class="field">
        <span class="title">code:</span>
        <input class="input-field" :value="attr.code" />
      </div>

      <div class="field">
        <span class="title">name:</span>
        <input class="input-field" :value="attr.name" />
      </div>

      <div v-if="attr.color" class="field">
        <span class="title">color:</span>
        <input class="input-field" :value="attr.color" />
      </div>

      <div v-if="attr.size" class="field">
        <span class="title">size:</span>
        <span>
          <input class="input-field" :value="attr.size.width" type="number" /> x
          <input class="input-field" :value="attr.size.height" type="number" />
        </span>
      </div>

      <div v-if="attr.weight" class="field">
        <span class="title">weight:</span>
        <input class="input-field" :value="attr.weight" type="number" />
      </div>
    </div>

    <div class="add">
      <label class="title"> type </label>
      <select class="select-field" ref="selectRef">
        <option value="color">color</option>
        <option value="size">size</option>
        <option value="weight">weight</option>
      </select>

      <button @click="addAttribute">Add</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps, ref } from "vue";

const props = defineProps<{
  item: {
    id: number;
    name: string;
    attributes: {
      code: string;
      name: string;
      color?: string;
      size?: { width: number; height: number };
      weight?: number;
    };
  };
}>();

const selectRef = ref<HTMLSelectElement>();

const innerItem = ref(props.item);

const addAttribute = () => {
  const selectedType = selectRef.value?.value;
  console.log(selectedType, "selectedType");
  if (!selectedType) return;

  switch (selectedType) {
    case "color":
      innerItem.value.attributes.push({
        code: "new code",
        name: "new field",
        color: "color",
      });
      break;
    case "size":
      innerItem.value.attributes.push({
        code: "new code",
        name: "new field",
        size: { width: 0, height: 0 },
      });
      break;
    case "weight":
      innerItem.value.attributes.push({
        code: "new code",
        name: "new field",
        weight: 0,
      });
      break;
  }
};
</script>

<style scoped lang="css">
.header {
  font-weight: 400;
  font-size: 25px;
  text-transform: capitalize;
}
.content {
  display: flex;
  flex-direction: column;
  padding: 20px;
  gap: 20px;
}
.detail {
  padding: 10px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.field {
  display: flex;
  gap: 5px;
}
.title {
  font-weight: bold;
  width: 100px;
  text-transform: capitalize;
}
.add {
  display: flex;
  gap: 10px;
}
.input-field {
  padding: 4px 8px;
  border-radius: 6px;
  border: 1px solid lightblue;
}

.select-field {
  padding: 4px 8px;
  border-radius: 6px;
  border: 1px solid lightblue;
}

button {
  padding: 4px 25px;
  border-radius: 6px;
  background-color: lightblue;
  border: 1px solid lightblue;
}
</style>
