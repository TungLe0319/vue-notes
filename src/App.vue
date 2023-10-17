<!-- eslint-disable no-unused-vars -->
<script setup>
import { ref, onMounted } from "vue";
import FirstMenuRow from "./components/FirstMenuRow.vue";
import SecondMenuRow from "./components/SecondMenuRow.vue";
import SideBarMenu from "./components/SideBarMenu.vue";

const fontsize = ref(24);
const notesTextarea = ref(null);
const phoneNumber = ref("Phone#");
const ticketNumber = ref("Ticket#");
const assetTag = ref("Asset#");
const userEmail = ref("User");
onMounted(() => {
  // Initialize your component here
  const why = document.getElementById("notes-area");
  why.addEventListener("focus", () => {
    watchClipBoard();
  });
});

async function watchClipBoard() {
  const clipBoard = await navigator.clipboard.readText();
console.log(clipBoard);
  // Regular expressions
  const phoneRegex = /(\+\d{1,2}\s?)?\(?\d{3}\)?[-.\s]?\d{3}[-.\s]?\d{4}/g; // Matches phone numbers
  const ticketRegex = /Ticket:\s?(\w+)/g; // Matches ticket numbers (assuming a format like "Ticket: ABC123")
  const emailRegex = /[\w.-]+@[\w.-]+\.\w+/g; // Matches email addresses

  // Check for matches and update the refs
  const phoneMatches = clipBoard.match(phoneRegex);
  if (phoneNumber.value === "Phone#") {
    if (phoneMatches) {
      phoneNumber.value = phoneMatches[0];
    }
  }

  const ticketMatches = clipBoard.match(ticketRegex);
  if (ticketMatches && !ticketNumber.value) {
    ticketNumber.value = ticketMatches[0].replace("Ticket# ", "");
  }

  if (userEmail.value === "User") {
    const emailMatches = clipBoard.match(emailRegex);
    if (emailMatches) {
      userEmail.value = emailMatches[0];
    }
  }
}

function changeFontSize(event) {
  if (event.key === "Alt" && (event.key === "+" || event.key === "-")) {
    console.log("hi");
    event.preventDefault();
    const newFontSize =
      event.key === "+" ? fontsize.value + 1 : fontsize.value - 1;
    fontsize.value = newFontSize;
  }
}

const text = ref("Type here...");
</script>

<template>
  <div class="main-container">
    <div class="notes-and-sidebar-container">
      <textarea
        class="notes-area"
        id="notes-area"
        ref="notesTextarea"
        v-model="text"
        :style="{ fontSize: fontsize + 'px' }"
        @keydown="changeFontSize"
      ></textarea>
      <div class="side-bar">
        <SideBarMenu />
      </div>
    </div>
    <div class="menu-container">
      <ul class="line-row">
        <li class="line-item">Classified</li>
        <li class="line-item">
          <input type="text" v-model="userEmail" />
        </li>

        <li class="line-item">
          <input type="text" v-model="assetTag" />
        </li>

        <li class="line-item">
          <input type="text" v-model="ticketNumber" />
        </li>
        <li class="line-item">
          <input type="text" v-model="phoneNumber" />
        </li>
      </ul>

      <!-- <FirstMenuRow />
      <SecondMenuRow /> -->
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

input {
  padding: 6px;
  background: transparent;
  outline: none;
  border: none;
  font-weight: 400;
  background-color: #8b5cf6;
  cursor: pointer;
  width: auto; /* Set the width to automatically grow as needed */
  max-width: 100px;
}
input:focus {
  outline: #ff5733 4px solid;
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

  height: 79vh;
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

  .side-bar-icon {
    width: 30px;
    height: 30px;
  }
}

.line-row {
  display: flex;
  padding: 3px;
  margin-top: 2px;
  margin-bottom: 2px;
  list-style: none;
}
.line-item {
  margin-left: 1px;
  margin-right: 1px;
  background-color: #8b5cf6;
  cursor: pointer;
  border: 2px solid #000;
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

/* For Webkit-based browsers (Chrome, Safari) */
::-webkit-scrollbar {
  width: 8px; /* Adjust the width of the scrollbar */
}

::-webkit-scrollbar-track {
  background: #333; /* Track color */
}

::-webkit-scrollbar-thumb {
  background: #e0ded9; /* Thumb color */
  border-radius: 6px; /* Thumb border radius */
}
</style>
