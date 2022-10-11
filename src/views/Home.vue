<template>
  <div class="home">
    <transition name="toast">
      <Toast v-if="showToast" />
    </transition>
    <Todos @badValue="triggerToast" />
    <transition name="fade">
      <p v-if="showP">Reference is in the source code actually.</p>
    </transition>
    <button @click="showP = !showP">Toggle Animation Reference</button>
  </div>
</template>

<script>
import { ref } from 'vue';
import Toast from '../components/Toast';
import Todos from '../components/Todos';

export default {
  components: { Toast, Todos },
  setup() {
    const showToast = ref(false);

    const showP = ref(false);

    const triggerToast = () => {
      showToast.value = true;
      setTimeout(() => (showToast.value = false), 3000);
    };

    return { showToast, triggerToast, showP };
  },
};
</script>

<style>
button {
  padding: 0.8rem;
  background: #42b983;
  border: none;
  border-radius: 8px;
  font-weight: bold;
  cursor: pointer;
}
.fade-enter-from {
  transform: translateX(-100px);
  opacity: 0;
}
.fade-enter-to {
  transform: translateX(0);
}
.fade-enter-active {
  transition: all 0.5s ease;
}
.fade-leave-from {
  opacity: 1;
}
.fade-leave-to {
  transform: translateX(100px);
  opacity: 0;
}
.fade-leave-active {
  transition: all 0.5s ease;
}

.toast-enter-active {
  animation: wobble 0.3s ease-in-out;
}

.toast-leave-to {
  transform: translateY(-100px);
  opacity: 0;
}
.toast-leave-active {
  transition: all 0.3s ease;
}

@keyframes wobble {
  0% {
    transform: translateY(-100px);
    opacity: 0;
  }
  50% {
    transform: translateY(0px);
    opacity: 1;
  }

  60% {
    transform: translateX(8px);
  }
  70% {
    transform: translateX(-8px);
  }
  80% {
    transform: translateX(4px);
  }
  90% {
    transform: translateX(-4px);
  }
  100% {
    transform: translateX(0px);
  }
}
</style>

