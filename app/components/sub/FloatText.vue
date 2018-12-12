<template>
    <GridLayout rows="20, auto" marginBottom="5">
        <Label ref="label" row="1" :text="hint" opacity="0.4" fontSize="14"  class="input"></Label>
        <TextField ref="textField" 
        v-model="value" 
        :secure="secure" 
        :keyboardType="keyboardType" 
        @textChange="onInput" 
        @focus="onFocus" 
        @blur="onBlur" 
        row="1"  
        borderBottomWidth="2" 
        borderBottomColor="#cec8c8" 
        padding="2"
        ></TextField>
    </GridLayout>
</template>

<script>
import Vue from "vue";
import { Color } from "tns-core-modules/color";
export default Vue.extend({
  props: ["value", "hint", "secure", "keyboardType", "editable"],
  methods: {
    onInput() {
      this.$emit("input", this.value);
    },
    floatLabel(setBorderColor = true) {
      /**
       * try catch as workaround
       * (when component is used as a model onFouces gets called when UI elements are already destroyed => error)
       */
      try {
        const label = this.$refs.label.nativeView;
        const textField = this.$refs.textField.nativeView;
        // animate the label sliding up and less transparent.
        label.animate({
          translate: { x: 0, y: -20 },
          opacity: 1
        });
        // set the border bottom color to green to indicate focus
        if (setBorderColor) {
          textField.borderBottomColor = new Color("#494eea");
        }
      } catch (e) {
        console.log(e);
      }
    },
    defloatLabel(setBorderColor = true) {
      try {
        const label = this.$refs.label.nativeView;
        const textField = this.$refs.textField.nativeView;
        // if there is text in our input then don't move the label back to its initial position.
        if (!textField.text) {
          label.animate({
            translate: { x: 0, y: 0 },
            opacity: 0.4
          });
        }
        // reset border bottom color.
        if (setBorderColor) {
          textField.borderBottomColor = new Color("#cec8c8");
        }
      } catch (e) {
        console.log(e);
      }
    },
    onFocus() {
      this.floatLabel();
      this.$emit("focus");
    },
    onBlur() {
      this.defloatLabel();
      this.$emit("blur");
    }
  },
  mounted() {
    const label = this.$refs.label.nativeView;
    const textField = this.$refs.textField.nativeView;
    if (textField.text) {
      setTimeout(() => this.floatLabel(false), 750);
    }
  },
  watch: {
    // set transition when text gets changed programatically
    value: {
      handler: function(newVal, oldVal) {
        const label = this.$refs.label.nativeView;
        const textField = this.$refs.textField.nativeView;
        if (
          (oldVal == undefined && newVal != undefined) ||
          (oldVal == "" && newVal != oldVal)
        ) {
          this.floatLabel(false);
        } else if (newVal == "" && oldVal != newVal) {
          this.defloatLabel(false);
        }
      }
    }
  }
});
</script>