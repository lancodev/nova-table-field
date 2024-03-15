<template>
  <div class="relative rounded-lg rounded-b-lg bg-gray-100 dark:bg-gray-800 bg-clip border border-gray-200 dark:border-gray-700 overflow-hidden" :class="{ 'mr-12': editMode && canDelete }">
    <slot />
  </div>
</template>

<script>
export default {
  props: {
    canDelete: {
      type: Boolean,
      default: true,
    },
    editMode: {
      type: Boolean,
      default: true,
    },
    defaultValues: {
      type: Object,
      default: () => [],
    }
  },
};
</script>
