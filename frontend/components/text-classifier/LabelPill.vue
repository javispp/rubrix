<template>
  <div>
      <p v-for="label in labels" :key="label.index"  class="pill" :title="label.class">
        <span class="pill__text">{{ label.class }} </span>
        <span class="pill__confidence" v-if="showConfidence">
          <ReNumeric
            class="radio-data__confidence"
            :value="decorateConfidence(label.confidence)"
            type="%"
            :decimals="2"
          ></ReNumeric>
        </span>
      </p>
      <span v-if="predicted" :class="['pill__predicted', predicted]"></span>
    </div>
</template>

<script>
export default {
  props: {
    labels: {
      type: Array,
      required: true,
    },
    predicted: {
      type: String,
    },
    showConfidence: {
      type: Boolean,
      default: false,
    }
  },
  methods: {
    decorateConfidence(confidence) {
      return confidence * 100;
    },
  }
};
</script>

<style lang="scss" scoped>
%pill {
  display: inline-flex;
  width: auto;
  background: transparent;
  color: $lighter-color;
  border-radius: 3px;
  padding: 0.2em 1em;
  @include font-size(14px);
  margin-top: 0;
  margin-bottom: 0;
  border: 1px solid transparent;
  margin-right: 0.5em;
}
.annotations {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 1em;
}
.predictions {
  margin-top: 1em;
  display: flex;
  flex-wrap: wrap;
  margin-right: -0.8em;
  margin-left: -0.8em;
  .pill {
    height: 40px;
    line-height: 40px;
    display: flex;
    width: 240px;
    align-items: center;
    margin-left: 0.8em;
    margin-right: 0.8em;
    margin-bottom: 1.6em;
    font-weight: bold;
    border-color: $line-smooth-color;
    box-shadow: $shadow-light;
    border-radius: 5px;
    &__confidence {
      margin-right: 0;
      margin-left: auto;
    }
  }
}
.pill {
  @extend %pill;
  border: 1px solid $line-medium-color;
  color: $font-medium-color;
  margin-bottom: 0.5em;
  @include font-size(13px);
  line-height: 1.4em;
  &__container {
    display: flex;
    margin-bottom: 1em;
  }
  &__text {
    display: inline-block;
    max-width: 200px;
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
  }
  &__confidence {
    font-weight: bold;
    margin-left: 1em;
  }
  &__predicted {
    margin: 0.4em;
    height: 15px;
    width: 15px;
    border-radius: 50%;
    display: inline-block;
    &.ko {
      background: $error;
    }
    &.ok {
      background: $success;
    }
  }
}
</style>
