<script setup lang="ts">
import { nanoid } from "nanoid";
import type { Column, Task } from "../types";
import draggable from "vuedraggable";
const columns = ref<Column[]>([
  {
    id: nanoid(),
    title: "Backlog",
    tasks: [
      {
        id: nanoid(),
        title: "Create marketing landing page",
        createdAt: new Date(),
      },
      {
        id: nanoid(),
        title: "Develop cool new feature",
        createdAt: new Date(),
      },
      {
        id: nanoid(),
        title: "Fix page nav bug",
        createdAt: new Date(),
      },
    ],
  },
  { title: "Selected for Dev", id: nanoid(), tasks: [] },
  { title: "In progress", id: nanoid(), tasks: [] },
  { title: "QA", id: nanoid(), tasks: [] },
  { title: "Complete", id: nanoid(), tasks: [] },
]);
</script>

<template>
  <div>
    <draggable
      v-model="columns"
      group="columns"
      item-key="id"
      :animation="150"
      handle=".drag-handle"
      class="flex gap-4 overflow-x-auto items-start"
    >
      <template #item="{ element: column }: { element: Column }"
        ><div class="column p-5 rounded min-w-[250px] bg-gray-200">
          <header class="font-bold mb-4">
            <DragHandle />
            {{ column.title }}
          </header>
          <draggable
            v-model="column.tasks"
            group="tasks"
            item-key="id"
            :animation="150"
            ><template #item="{ element: task }: { element: Task }"
              ><TrelloBoardTask :task="task" /></template
          ></draggable>

          <footer>
            <button class="text-gray-500">+ Add a Card</button>
          </footer>
        </div></template
      >
    </draggable>
  </div>
</template>
