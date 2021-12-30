<template>
  <div :class="isMultiSelect ? 'wrapper-multiSelect' : 'wrapper-select'">
    <legend v-if="isMultiSelect">Группа клиентов*</legend>
    <legend v-else-if="isPaspport">Тип документа*</legend>
    <legend v-else>Лечащий врач</legend>
    <div :class="isPaspport ? 'documnet-select' : 'select'">
      <p
        :class="isVisible ? 'title-active' : isRequired ? 'is-error' : 'title'"
        @click="isVisible = !isVisible"
      >
        {{ isMultiSelect ? defaultMultiValue.join(" ") : defaultValue }}
        <span :class="isVisible ? 'toggle-open' : 'toggle-close'"></span>
      </p>

      <div :class="isVisible ? 'options-active' : 'options'" v-if="isVisible">
        <p v-for="option in selectOptions" :key="option.value" @click="selectOption(option)">
          {{ option.value }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "custom-select",
    props: {
      isMultiSelect: { type: Boolean },
      isPaspport: { type: Boolean },
      isRequired: { type: Boolean, require: true },
      selectOptions: {
        type: Array,
        default() {
          return [];
        },
      },
      defaultValue: {
        type: String,
        default() {
          return "";
        },
      },
      defaultMultiValue: {
        type: Array,
        default() {
          return [];
        },
      },
    },
    data() {
      return {
        isVisible: false,
      };
    },
    methods: {
      selectOption(option) {
        this.$emit("select", option);
        this.isVisible = false;
      },
      hideSelect() {
        this.isVisible = false;
      },
    },
  };
</script>

<style lang="scss">
  @import "../../scss/_vars.scss";
  @import "../../scss/_mixins.scss";
  .wrapper-multiSelect {
    flex: 2;
    @media (max-width: map-get($breack-point, mobile)) {
      margin-bottom: 1em;
    }
  }
  legend {
    font-size: 1.05rem;
    margin-bottom: $mrg-label;
  }
  .select,
  .multi-select {
    position: relative;
    width: 15em;
    @media (max-width: map-get($breack-point, mobile)) {
      width: 24em;
    }
  }
  .wrapper-multiSelect {
    margin-right: 0.6em;
  }
  .wrapper-select {
    margin-bottom: 1.3em;
  }
  .documnet-select {
    position: relative;
    width: 100%;
  }
  .title,
  .title-active {
    border: 1px solid #a1bcdb;
    border-radius: 5px;
    padding: 0.8em;
    font-size: 0.95rem;
    cursor: pointer;
    &:hover {
      border-color: $clr-primary-light;
    }
    @media (max-width: map-get($breack-point, mobile)) {
      &:hover {
        border-color: $clr-primary;
      }
    }
  }
  .select p,
  .documnet-select p {
    margin: 0;
    .toggle-close,
    .toggle-open {
      position: absolute;
      top: 0.9em;
      right: 0.8em;
      &::before {
        display: inline-block;
        content: "\25BD";
        color: $clr-primary-light;
      }
    }
    .toggle-open {
      top: 0.8em;
      &::before {
        content: "\25B3";
      }
    }
  }
  .options,
  .options-active {
    border-radius: 5px;
    position: absolute;
    top: 3em;
    right: 0;
    width: 100%;
    z-index: 3;
    @media (max-width: map-get($breack-point, mobile)) {
      top: 3.15em;
    }
  }
  .title-active,
  .options-active {
    border: 1px solid $clr-primary;
  }
  .options p,
  .options-active p {
    border-top-left-radius: 4px;
    border-top-right-radius: 4px;
    background-color: $clr-body-form;
    font-size: 0.95rem;
    padding-top: 0.5em;
    padding-bottom: 0.5em;
    padding-left: 0.5em;
    color: $clr-placeholder;

    &:not(:first-child) {
      border-top-left-radius: 0px;
      border-top-right-radius: 0px;
    }

    &:last-child {
      border-bottom-left-radius: 4px;
      border-bottom-right-radius: 4px;
    }
    &:not(:last-child) {
      border-bottom: 1px solid $clr-primary;
    }
    &:hover {
      cursor: pointer;
      background-color: $clr-primary-light;
      color: rgba(44, 39, 56, 1);
    }
  }
  .is-error {
    border: 1px solid $clr-error;
    border-radius: 5px;
    padding: 0.8em;
    font-size: 0.95rem;
    cursor: pointer;
    &:hover {
      border-color: $clr-error-light;
    }
  }
</style>
