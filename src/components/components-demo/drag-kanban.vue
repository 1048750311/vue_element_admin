<template>
  <div class="components-container board">
    <Kanban :key="1" :list="list1" :group="group" class="kanban todo" header-text="待维修" />
    <Kanban :key="2" :list="list2" :group="group" class="kanban working" header-text="维修中" />
    <Kanban :key="3" :list="list3" :group="group" class="kanban done" header-text="维护完成" />
  </div>
</template>
<script>
import Kanban from '../Kanban/index.vue'

export default {
  name: 'DragKanbanDemo',
  components: {
    Kanban
  },
  data() {
    return {
      group: 'mission',
      list1: [
        { name: '华为S5700-28C-HI', id: 15770147240 },
        { name: '华为OSPF设备', id: 17364861348 },
        { name: '华为AR201', id: 15578903019 },
        { name: '华为AR1201', id: 15734394129 },
        { name: '华为AR2220', id: 15553296646 },
        { name: '华为AP2050', id: 15708551372 }
      ],
      list2: [
        { name: '华为AR1201', id: 15544177772 },
        { name: '华为AR2220', id: 15733607862 }
      ],
      list3: [
        { name: '华为AR201', id: 18330347078 },
        { name: '华为AR1201', id: 17353426344 },
        { name: '华为AR2220', id: 17350379375 }
      ]
    }
  }
}
</script>
<style lang="scss" >
.board {
  width: 100%;
  margin-left: 20px;
  display: flex;
  justify-content: space-around;
  flex-direction: row;
  align-items: flex-start;
}

.kanban {
  &.todo {
    .board-column-header {
      background: #f9564a;
    }
  }

  &.working {
    .board-column-header {
      background: #f9944a;
    }
  }

  &.done {
    .board-column-header {
      background: #2ac06d;
    }
  }
}
</style>
