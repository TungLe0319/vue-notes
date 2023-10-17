<!-- eslint-disable no-unused-vars -->
<script>
import { onMounted, ref, watch, watchEffect } from "vue";
import FirstMenuRow from "./components/FirstMenuRow.vue";

export default {
  setup() {
    const fontsize = ref(24);
    onMounted(() => {});
    watchEffect(() => {});
    async function watchClipboard() {
      if (navigator) {
        try {
          const clipBoard = await navigator.clipboard.readText();
          if (clipBoard !== this.previousClipboardData) {
            console.log("Clipboard content has changed:", clipBoard);
            this.previousClipboardData = clipBoard;
          }
        } catch (error) {
          // Handle the error (e.g., log it)
          console.error("Clipboard read error:", error);
        }
      }
    }
    async function startClipboardWatcher() {
      this.previousClipboardData = await navigator.clipboard.readText();
      setInterval(this.watchClipboard, 1000); // Check every second
    }
    function changeFontSize(e) {
      if (event.ctrlKey && (e.key === "+" || e.key === "-")) {
        event.preventDefault();
        const newFontSize =
          event.key === "+" ? this.fontSize + 1 : this.fontSize - 1;
        this.fontSize = newFontSize;
      }
    }

    return {
      previousClipboardData: null,
      text: "Type here...",
      fontsize,
    };
  },

  components: {
    FirstMenuRow,
  },
};
</script>

<template>
  <div class="main-container">
    <div class="notes-and-sidebar-container">
      <textarea
        class="notes-area"
        id="notes-area"
        v-model="text"
        :style="{ fontSize: fontsize + 'px' }"
        @keydown="changeFontSize"
      ></textarea>
      <div class="side-bar">
        <ul class="side-bar-menu">
          <li>
            <img
              class="side-bar-icon"
              src="https://cdn-icons-png.flaticon.com/128/1/1176.png"
              alt=""
            />
          </li>
          <li>
            <img
              class="side-bar-icon"
              src="https://cdn-icons-png.flaticon.com/128/1/1176.png"
              alt=""
            />
          </li>
          <li>
            <img
              class="side-bar-icon"
              src="https://cdn-icons-png.flaticon.com/128/1/1176.png"
              alt=""
            />
          </li>
          <li>
            <img
              class="side-bar-icon"
              src="https://cdn-icons-png.flaticon.com/128/1/1176.png"
              alt=""
            />
          </li>
        </ul>
      </div>
    </div>
    <div class="menu-container">
      <FirstMenuRow />
    </div>
  </div>
</template>

<style lang="scss">
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
  padding: 5px;
  padding-right: 10px;
  overflow-y: auto;
  resize: none;
}

.notes-area:focus {
  outline: none;
}

.side-bar {
  width: 1.5%; /* Initially a smaller width */
  background-color: #ff5733;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  .side-bar-menu {
    margin-left: 12px;
    padding-left: 12px;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 0%;
    opacity: 0;
    list-style: none;
  }

  li {
    margin-top: 8px;
    margin-bottom: 8px;
  }

  .side-bar-icon {
    width: 30px;
    height: 30px;
  }
}

.side-bar:hover {
  width: 5%; /* Expand on hover */
  .side-bar-menu {
    width: 100%;
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
