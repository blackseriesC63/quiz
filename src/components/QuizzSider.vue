<script setup>
import { ref, onMounted, onUnmounted, toRefs } from "vue";
import { Icon } from "@iconify/vue";

const props = defineProps({
  modelValue: Boolean,
});

const emit = defineEmits(["update:modelValue"]);

const { modelValue } = toRefs(props);

const toggleSide = () => {
  emit("update:modelValue", !modelValue.value);
};

// Function to get the current time as a formatted string
const getCurrentTime = () => {
  const now = new Date();
  return now.toLocaleTimeString();
};

// Reactive reference to hold the current time
const currentTime = ref(getCurrentTime());

// Function to update the current time every second
const updateCurrentTime = () => {
  currentTime.value = getCurrentTime();
};

let timer;

onMounted(() => {
  // Start the timer to update the time every second
  timer = setInterval(updateCurrentTime, 1000);
});

onUnmounted(() => {
  // Clear the timer when the component is unmounted
  clearInterval(timer);
});
</script>

<template>
  <div
    :class="modelValue ? 'w-[45%]' : 'w-[65px]'"
    class="fixed top-0 right-0 h-screen duration-300 bg-primary"
  >
    <div class="flex items-center justify-between shadow-md pr-5">
      <div>
        <button
          class="bg-orange-700 py-8 px-2 flex justify-center hover:bg-slate-900 hover:text-white"
          :class="!modelValue ? 'w-[65px]' : ''"
          @click="toggleSide"
        >
          <Icon
            :class="!modelValue ? '' : 'rotate-180'"
            class="text-4xl"
            icon="iconamoon:arrow-left-2-bold"
          />
        </button>
      </div>

      <div class="text-3xl py-8">{{ currentTime }}</div>

      <button class="text-neutral-200">Chiqish ></button>
    </div>

    <div class="p-5 pl-20">
      <div class="text-xl mb-4">Matematika</div>
      <div class="flex gap-4">
        <button
          v-for="n in 10"
          :key="n"
          class="bg-primary rounded-full w-10 h-10 flex items-center justify-center border border-black hover:bg-black hover:text-white"
        >
          {{ n }}
        </button>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
