<template>
  <div class="modal fade show">
    <div class="modal-dialog modal-dialog-scrollable">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">{{ title }}</h5>
          <button
            type="button"
            class="btn-close"
            @click="closeModal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body" style="height: 200px" @scroll="onScroll">
          <slot></slot>
        </div>
        <div class="modal-footer">
          <slot name="footer">
            <button type="button" class="btn btn-secondary" @click="closeModal">
              Close
            </button>
            <button
              :disabled="!isScrolledFully"
              type="button"
              class="btn btn-primary"
            >
              Save changes
            </button>
          </slot>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import scrollHandler from "../../mixins/lesson9-most-useless/scrollHandler";

export default {
  name: "Modal",
  mixins: [scrollHandler],
  props: {
    title: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      isScrolledFully: false,
    };
  },
  methods: {
    closeModal() {
      this.$emit("close");
    },
    onScrollEnd() {
      this.isScrolledFully = true;
    },
  },
};
</script>

<style scoped>
.modal {
  display: block;
}
</style>
