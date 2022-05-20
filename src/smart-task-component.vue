<script lang="ts">
import { defineComponent } from "vue";

export enum SmartTaskStatus {
  Backlog = 1,
  ReadyToStart = 2,
  InProgress = 3,
  Completed = 4,
  Skipped = 5,
  Faulted = 6,
}

export interface SmartTaskState {}

export default /*#__PURE__*/ defineComponent({
  name: "SmartTaskComponent", // vue component name
  props: {
    componentState: Object as () => SmartTaskState,
    componentStatus: Object as () => SmartTaskStatus,
  },
  data() {
    return { model: {} };
  },
  computed: {},
  methods: {
    async submitForm() {
      this.$emit("execute-smart-task", this.model);
    },
  },
  created() {
    if (this.componentState) {
      this.model = this.componentState;
    }
  },
  setup() {
    return {SmartTaskStatus}
  },
});
</script>

<template>
  <form v-if="componentStatus != SmartTaskState.Completed">
    <div class="my-5">
      <button type="button" @click="submitForm" class="btn btn-sm btn-primary">
        Mark as Completed
      </button>
    </div>
  </form>
  <form v-if="componentStatus == SmartTaskState.Completed">
    <p>Task has been completed.</p>
    <div class="my-5">
      <button type="button" @click="submitForm" class="btn btn-sm btn-white">
        Mark as In-Progress
      </button>
    </div>
  </form>
</template>

