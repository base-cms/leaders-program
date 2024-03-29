<template>
  <div v-if="canDisplay" class="leaders-content-deck">
    <div class="leaders-content-deck__header">
      <div class="leaders-content-deck__header-left">
        <slot name="header-left" />
      </div>
      <div class="leaders-content-deck__header-right">
        <slot name="header-right" />
      </div>
    </div>
    <div class="leaders-content-deck__body">
      <div
        v-for="(item, index) in limitedValue"
        :key="index"
        :class="itemClasses"
      >
        <slot :item="item" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: Array,
      default: () => [],
    },
    limit: {
      type: Number,
      default: 4,
    },
    itemModifiers: {
      type: Array,
      default: () => [],
    },
  },

  computed: {
    canDisplay() {
      return Boolean(this.value.length);
    },
    limitedValue() {
      return this.value.slice(0, this.limit);
    },
    itemClasses() {
      const elementName = 'leaders-content-deck__item';
      return [
        elementName,
        ...this.itemModifiers.map(mod => `${elementName}--${mod}`),
      ];
    },
  },
};
</script>

<style lang="scss">
@import "../../../scss/variables";
@import "../../../scss/functions";

.leaders-content-deck {
  $block: &;

  &__header {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin-bottom: $leaders-card-padding / 2;
    font-size: 14px;
  }

  &__header-left {
    font-weight: 800;
  }

  &__body {
    display: flex;
    flex-direction: row;
  }

  &__item {
    &--promo {
      padding-right: leaders-promo-card-padding();
      padding-left: leaders-promo-card-padding();
    }

    &--video {
      padding-right: leaders-video-card-padding();
      padding-left: leaders-video-card-padding();
    }

    &:first-child {
      padding-left: 0;
    }

    &:last-child {
      padding-right: 0;
    }
  }

  a {
    color: $leaders-card-body-color;
    &:hover {
      color: $leaders-card-body-color;
    }
  }

  + #{ $block } {
    padding-top: $leaders-card-padding;
    border-top: 1px solid $leaders-card-body-hr-color;
  }

}
</style>
