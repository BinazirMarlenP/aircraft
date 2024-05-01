<template>
  <div class="list">
    <span
      v-for="item in props.items"
      :key="item.id"
      class="item"
      :class="{ itemSelected: isSelected(item) }"
      @click="handleItemClick(item)"
    >
      {{ item.name }}
    </span>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits, ref, Ref } from "vue";

const props = defineProps<{
  items: {
    id: string;
    name: string;
  }[];
}>();

const emit = defineEmits(["click"]);

const selectedItem: Ref<string | null> = ref(null);

const isSelected = (item: { id: string }) => {
  return selectedItem.value === item.id;
};

const handleItemClick = (item: { id: string }) => {
  selectedItem.value = item.id;
  emit("click", item);
};
</script>

<style lang="css">
.list {
  display: flex;
  flex-direction: column;
  border: 1px solid lightblue;
  border-radius: 6px;
}

.item {
  padding: 10px;
  cursor: pointer;
  font-size: 20px;
  font-weight: 400;
  min-width: 250px;
  border-radius: 6px 6px 0 0;
  text-transform: capitalize;
}

.itemSelected {
  padding: 10px;
  cursor: pointer;
  font-size: 25px;
  font-weight: bold;
  min-width: 250px;
  border-radius: 6px 6px 0 0;

  background: lightskyblue;
}

.item:hover {
  background: #f0f0ff;
}
</style>
