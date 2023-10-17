<template>
  <ul class="line-row">
    <li class="line-item">CheckList</li>

    <li class="line-item">CallTemplates</li>
  
    <li class="line-item">Other Checklist stuff</li>
  </ul>

  <div v-if="isOpen">
    <div class="modal">
      <div class="modal-content">
        <!-- <input type="text" bind:value="{emailInput}" />  -->
        <button on:click="{close}">Close</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      phonePattern: /\b\d{10}\b|\b\d{3}-\d{3}-\d{4}\b/g,
      ticketPattern: /\bIRC\d{8}\b/g,
      emailPattern: /\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b/g,
      isOpen: false,
      emailInput: "",
    };
  },
  methods: {
    open() {
      console.log("Opened");
      this.isOpen = true;
    },
    close() {
      console.log("Closed");
      this.isOpen = false;
    },
    checkInput() {
      // You can add logic here to check the email input
    },
  },
};
</script>
<style scoped>
.line-row {
  display: flex;
  padding: 3px;
  margin-top: 2px;
  margin-bottom: 2px;
}
.line-item {
  padding: 0.5rem;
  margin-left: 1px;
  margin-right: 1px;
  background-color: #8b5cf6;
  cursor: pointer;
  border: 2px solid #000;
}

.line-item:hover {
  filter: brightness(90%);
}

.line-item {
  display: flex;
  align-items: center;
}

.modal {
  position: absolute;
  top: 110px;

  z-index: 10;
  left: 0;
  width: 100%;
  height: 100%;

  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background: white;
  padding: 10px;
  border-radius: 2px;
}
</style>
