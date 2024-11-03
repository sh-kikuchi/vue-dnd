<script setup lang="ts">
import { ref } from 'vue';
import HelloWorld from './components/HelloWorld.vue';

interface Item {
  id: number;
  title: string;
  list: number;
}

const items = ref<Item[]>([
  { id: 0, title: 'item A', list: 1 },
  { id: 1, title: 'item B', list: 1 },
  { id: 2, title: 'item C', list: 2 },
]);

// Filter items based on the list parameter
const getList = (list: number): Item[] => {
  return items.value.filter((item) => item.list === list);
};

const startDrag = (event: DragEvent, item: Item) => {
  if (event.dataTransfer) {
    console.log(item);
    event.dataTransfer.dropEffect = 'move';
    event.dataTransfer.effectAllowed = 'move';
    event.dataTransfer.setData('itemID', item.id.toString());
  }
};

const onDrop = (event: DragEvent, list: number) => {
  const itemID = event.dataTransfer?.getData('itemID');
  const item = items.value.find((item) => item.id === Number(itemID));
  if (item) item.list = list;
};
</script>

<template>
  <HelloWorld msg="Vue DnD" />
  <div
    class="drop-zone"
    @drop="onDrop($event, 1)"
    @dragenter.prevent
    @dragover.prevent
  >
    <div
      v-for="item in getList(1)"
      :key="item.id"
      class="drag-el"
      draggable="true"
      @dragstart="startDrag($event, item)"
    >
      {{ item.title }}
    </div>
  </div>
  <div
    class="drop-zone"
    @drop="onDrop($event, 2)"
    @dragenter.prevent
    @dragover.prevent
  >
    <div
      v-for="item in getList(2)"
      :key="item.id"
      class="drag-el"
      draggable="true"
      @dragstart="startDrag($event, item)"
    >
      {{ item.title }}
    </div>
  </div>
</template>

<style scoped>
.drop-zone {
  width: 50%;
  margin: 50px auto;
  background-color: aliceblue;
  padding: 10px;
  min-height: 10px;
}

.drag-el {
  background-color: aquamarine;
  color: aliceblue;
  padding: 5px;
  margin-bottom: 10px;
}

.drag-el:nth-last-of-type(1) {
  margin-bottom: 0;
}
</style>
