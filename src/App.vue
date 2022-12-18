<script setup>
import { ref } from 'vue';
import { onClickOutside } from '@vueuse/core'

const isModalOpen = ref(false);
const modalRef = ref(null);

function toggleModal() {
  isModalOpen.value = !isModalOpen.value
  console.log(isModalOpen.value)
}

onClickOutside(modalRef, toggleModal);

</script>

<template>
  <div class="test">
    <p>Hello, Vue Modal</p>
    <button @click="toggleModal">Open Modal</button>
  </div>
  <Teleport to="#modal">
    <Transition name="modal">
      <div v-if="isModalOpen" class="modal-bg">
        <div ref="modalRef" class="modal">
          click outside this modal to close it.
          <button @click="toggleModal">Close Modal</button>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<style scoped>
.modal-enter-active,
.modal-leave-active {
  transition: all .25s ease;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
  transform: scale(1.2);
}

.test {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding-top: 30px;
  gap: 5px;
  text-align: center;
}

.test p {
  font-size: 30px;
  font-weight: 600;
}

.test button {
  background-color: aquamarine;
  color: black;
}

.modal-bg {
  position: fixed;
  z-index: 1;
  inset: 0;
  background: rgba(0, 0, 0, 0.5);
  display: grid;
  place-content: center;
}

.modal {
  background-color: white;
  border-radius: 3px;
  padding: 30px;
  height: 100px;
  display: grid;
  gap: 10px;
  place-content: center;
  align-items: flex-start;
}

button {
  padding: 7px 20px;
  border-radius: 2px;
  outline: none;
  border: none;
  width: fit-content;
  height: fit-content;
  cursor: pointer;
  margin-inline: auto;
}

.modal button {
  background-color: coral;
  color: white;
}
</style>
