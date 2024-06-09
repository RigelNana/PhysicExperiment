<template>
  <div id="app">
    <div class="sidebar-container">
      <div class="sidebar" :class="{ expanded: isExpanded }">
        <button @click="toggleSidebar">☰</button>
        <transition name="fade">
          <div class="menu" v-show="isExpanded">
            <div class="menu-item">功能1</div>
            <div class="menu-item">功能2</div>
            <div class="menu-item">功能3</div>
          </div>
        </transition>
      </div>
    </div>
    <div class="content">
      <table>
        <thead>
        <tr>
          <th>名称</th>
          <th>值</th>
          <th>计算结果</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="(item, index) in items" :key="index">
          <td><input v-model="item.name" type="text" /></td>
          <td><input v-model.number="item.value" type="number" @input="updateValues" /></td>
          <td>{{ calculateValue(item) }}</td>
        </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isExpanded: false,
      items: [
        { name: 'Item 1', value: 0 },
        { name: 'Item 2', value: 0 },
        { name: 'Item 3', value: 0 },
      ],
    };
  },
  methods: {
    toggleSidebar() {
      this.isExpanded = !this.isExpanded;
    },
    updateValues() {

    },
    calculateValue(item) {
      return item.value * 2;
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
  text-align: left;
  padding-left: 20px;
  opacity: 1;
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