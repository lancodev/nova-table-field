<template>
  <div class="bg-gray-100 dark:bg-gray-800 rounded-t-lg flex items-center key-value-item border-b border-gray-200 dark:border-gray-700">
    <div class="flex flex-grow key-value-fields">
      <div
        :class="{
            'bg-white dark:bg-gray-800': rowIndex > 0,
          }"
        :key="`column-${index}`"
        @click="handleColumnFieldFocus(index)"
        class="flex-grow"
        v-for="(cell, index) in row.cells"
      >
        <textarea
          :class="{
            'bg-white dark:bg-gray-800': rowIndex > 0,
            'border-l border-gray-200 dark:border-gray-700': index > 0,
          }"
          :disabled="!isEditable"
          :dusk="`key-value-value-${index}`"
          :key="cell.id"
          @focus="handleColumnFieldFocus(index)"
          class="block min-h-input w-full min-h-full bg-clip dark:bg-gray-800 uppercase font-bold text-xxs text-gray-500 tracking-wide px-3 py-2"
          ref="columnFields"
          v-model="row.cells[index]"
        />
      </div>
    </div>

    <div class="flex justify-center h-11 w-11 absolute" style="right: -40px" v-if="isEditable && canDelete">
      <button
        @click="$emit('remove-row', row.id)"
        class="flex appearance-none cursor-pointer text-70 hover:text-danger active:outline-none active:shadow-outline focus:outline-none focus:shadow-outline"
        style="align-items: center"
        tabindex="-1"
        title="Delete"
        type="button"
      >
        <icon type="trash" />
      </button>
    </div>
  </div>
</template>

<script>
import autosize from 'autosize';

export default {
  props: {
    rowIndex: Number,
    row: Object,
    disabled: {
      type: Boolean,
      default: false,
    },
    readOnly: {
      type: Boolean,
      default: false,
    },
    canDelete: {
      type: Boolean,
      default: true,
    },
  },

  mounted() {
    console.log(this.rowIndex)
    autosize(this.$refs.columnFields);
  },

  methods: {
    handleColumnFieldFocus(index) {
      this.$refs.columnFields[index].select();
    },
  },

  computed: {
    isEditable() {
      return !this.readOnly && !this.disabled;
    },
  },
};
</script>
