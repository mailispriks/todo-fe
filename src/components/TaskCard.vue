<template>
  <div class="bg-white shadow rounded px-3 pt-3 pb-5 border-2" :class="'border-' + task.color.toLowerCase() + '-400'">
    <div class="flex justify-between">
      <p class="text-gray-700 font-semibold font-sans tracking-wide text-sm">{{ task.title }}</p>
    </div>
    <div class="flex mt-4 justify-between items-center">
      <span class="text-sm text-gray-600">{{ dayjs(task.date).format('DD.MM.YYYY') }}</span>
      <badge v-if="task.priority" :color="badgeColor"><span class="capitalize">{{ task.priority.toLowerCase() }}</span></badge>
    </div>
  </div>
</template>
<script>
import Badge from "./Badge.vue";
import dayjs from 'dayjs'

export default {
  components: {
    Badge
  },
  props: {
    task: {
      priority: Object,
      default: () => ({})
    }
  },
  computed: {
    badgeColor() {
      const mappings = {
        HIGH: "red",
        MEDIUM: "yellow",
        LOW: "green",
        default: "teal"
      };
      return mappings[this.task.priority] || mappings.default;
    }
  },
  methods: {
    dayjs
  }
};
</script>
