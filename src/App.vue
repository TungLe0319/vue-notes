<script>
import FirstMenuRow from "./components/FirstMenuRow.vue";

export default {
  name: "App",
  components: {
    FirstMenuRow,
  },
};
</script>

<template>
  <div class="main-container">
    <div class="notes-and-sidebar-container">
      <div class="notes-area p-1">NOTES AREA <br /></div>
      <div class="side-bar">
        <ul class="side-bar-menu">
          <li>1</li>
          <li>2</li>
          <li>3</li>
          <li>4</li>
        </ul>
      </div>
    </div>
    <div class="menu-container">
      <FirstMenuRow />
    </div>
  </div>
</template>

<style>
html,
body {
  margin: 0px;
  height: 100%;
}
#app {
  margin: 0px;
}
.main-container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  border: 2px solid #666;
  background-color: #2196f3;
}

.notes-and-sidebar-container {
  display: flex;
  justify-content: space-between;
  background-color: #4caf50;

  height: 80vh;
}

.notes-area {
  width: 98%; /* Initially take up most of the width */
  background-color: #ffc107;

  padding-right: 10px;
  overflow-y: auto;
}

.side-bar {
  width: 1.5%; /* Initially a smaller width */
  background-color: #ff5733;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  transition: width 0.5s;

  .side-bar-menu {
    width: 0;
    opacity: 0;
  }
}

.side-bar:hover {
  width: 5%; /* Expand on hover */
  .side-bar-menu {
    width: 2px;
    opacity: 1;
  }
}

.menu-container {
  border-top: 4px black solid;
  display: flex;
  flex-direction: column;
  height: 17vh;
}

.row-1,
.row-2,
.row-3,
.row-4 {
  display: flex;
  justify-content: space-between;
}
</style>
