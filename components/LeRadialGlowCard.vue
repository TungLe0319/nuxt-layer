<template>
  <div class="flex w-full flex-col items-center justify-center">
    <div class="features">
      <div class="feature" :class="[backgroundColorClass]">
        <div class="feature-content  space-y-3" :style="{ color: textColor }">
          <Icon name="i-heroicons-swatch" size="40" />
          <div class="pl-1 flex flex-col space-y-3 ">
            <strong>{{ title }}</strong>
            <span>{{ content }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
const props = defineProps(['title', 'content', 'icon', 'color']);

type TailwindColor = 'amber' | 'gray' | 'red' | 'purple' | 'emerald'; // Add more colors as needed
const theme = {
  get colorWithOpacity() {

    return getColorRGB(props.color);
  },
};

const borderColor = {
  color:props.color
}

const backgroundColorClass = ref(getBackgroundColorClass(props.color));
const textColor = ref(getTextColorClass(props.color));


onMounted(() => {
  const featuresEl = document.querySelector(".features");
  const featureEls = document.querySelectorAll(".feature");
  featuresEl!.addEventListener("pointermove", (ev) => {
    featureEls.forEach((featureEl) => {
      // Not optimized yet, I know
      const rect = featureEl.getBoundingClientRect();
      featureEl.style.setProperty("--x", ev.clientX - rect.left);
      featureEl.style.setProperty("--y", ev.clientY - rect.top);
    });
  });
});
function getColorRGB(color: TailwindColor): string {
  // Add logic to map Tailwind color names to RGB values
  // For simplicity, you can provide predefined RGB values here
  switch (color) {
      case 'amber':
      return 'rgba(246, 199, 59, 0.2)';
    case 'gray':
      return 'rgba(169, 169, 169, 0.2)';
    case 'red':
      return 'rgba(255, 0, 0, 0.2)';
    case 'purple':
      return 'rgba(128, 0, 128, 0.2)';
    case 'emerald':
      return 'rgba(0, 128, 0, 0.2)';
    default:
      return 'rgba(246, 199, 59, 0.2)';  // Default to amber if color is not recognized
  }
}

// Watch for changes in props.color and update colors accordingly
watch(() => props.color, () => {
  updateColors();
});

// Method to update colors based on the color prop
function updateColors() {
  backgroundColorClass.value = getBackgroundColorClass(props.color);
  textColor.value = getTextColorClass(props.color);
}

// Method to map color prop to Tailwind CSS background color class
function getBackgroundColorClass(color: TailwindColor): string {
  return `bg-${color}-500`; // Adjust as needed
}

// Method to map color prop to Tailwind CSS text color class
function getTextColorClass(color: TailwindColor): string {
  return `text-${color}-900`; // Adjust as needed
}


</script>

<style scoped>
*,
*:before,
*:after {
  box-sizing: border-box;
  position: relative;
}

.features {
  width: 75vw;
  height: 50vh;

 padding: 10px;
  display: grid;


}

.feature {
  --x-px: calc(var(--x) * 1px);
  --y-px: calc(var(--y) * 1px);
  --border: 2px;

  border-radius: 0.5rem;
  overflow: hidden;


}

.feature {
  background: radial-gradient(800px circle at var(--x-px) var(--y-px),
      v-bind('borderColor.color'),transparency 40%,
    );

}

.feature:before,
.feature:after {
  content: "";
  display: block;
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  inset: 0px;
  border-radius: inherit;
  background: radial-gradient(800px circle at var(--x-px) var(--y-px),
      v-bind('theme.colorWithOpacity'),
      transparent 40%);

}

.feature:before {
  z-index: 1;
}

.feature:after {
  opacity: 5%;
  z-index: 2;
  transition: opacity 0.4s ease;
}

.feature:hover:after {
  opacity: 1;
}

.feature-content {
  background: #131315;
  border-radius: inherit;

  padding: 10px;
  z-index: 1;

  position: absolute;
  inset: var(--border);

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: start;

}
</style>
