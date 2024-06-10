
<template>
  <div id="app">
    <div class="sidebar-container">
      <div class="sidebar" :class="{ expanded: isExpanded }">
        <button @click="toggleSidebar">☰</button>
        <transition name="fade">
          <div class="menu" v-show="isExpanded">
            <div class="menu-item" @click="selectTable('1')">杨氏模量</div>
            <div class="menu-item" @click="selectTable('2')">功能2</div>
            <div class="menu-item" @click="selectTable('3')">功能3</div>
          </div>
        </transition>
      </div>
    </div>
    <div class="content">
      <component :is="tables[currentTable]"></component>
    </div>
  </div>
</template>

<script>

import yangMod from "@/components/YangMod.vue";
import YangMod from "@/components/YangMod.vue";
export default {
  components: {YangMod},
  data() {
    return {
      isExpanded: false,
      currentTable: '1',
      tables: {
        '1': yangMod,
        // '功能2': [
        //   { name: 'Item A', value: 100 },
        //   { name: 'Item B', value: 200 },
        //   { name: 'Item C', value: 300 },
        // ],
        // '功能3': [
        //   { name: 'Item X', value: 1000 },
        //   { name: 'Item Y', value: 2000 },
        //   { name: 'Item Z', value: 3000 },
        // ]
      }
    };
  },
  methods: {
    toggleSidebar() {
      this.isExpanded = !this.isExpanded;
    },
    // updateValues() {
    //
    // },
    // calculateValue(item) {
    //   return item.value * 2;
    // },
    selectTable(table) {
      this.currentTable = table;
    },
  },
};
</script>

<style>
#app {
  display: flex;
  height: 100vh;
  width: 100%;
  overflow: hidden;
}

.sidebar-container {
  display: flex;


}

.sidebar {
  width: 50px;
  transition: width 0.3s ease;
  background-color: #333;
  color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
  overflow: hidden;
  position: fixed;
  left: 0;
  top: 0;
  bottom: 0;

}

.sidebar.expanded {
  width: 200px;
}

.menu {
  margin-top: 20px;
  width: 100%;
}

.menu-item {
  margin: 10px 0;
  text-align: center;
  padding-left: 0px;
  opacity: 1;
  cursor: pointer;
  text-decoration: none;


}
.menu-item:hover{
  text-decoration: underline;
}
button {
  background: none;
  border: none;
  color: white;
  font-size: 20px;
  cursor: pointer;
}

.content {
  flex-grow: 1;
  padding: 20px;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
}

th {
  background-color: #f2f2f2;
  text-align: left;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.fade-enter-active {
  animation: fadeIn 0.2s ease forwards;
}

.fade-leave-active {
  transition: opacity 0.2s;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>