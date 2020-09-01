<template>
  <div class="n-button">
    <v-btn
      :id="`id-${name}`"
      depressed
      :to="to"
      :href="href"
      :target="target"
      :exact="exact"
      :type="submit ? 'submit' : type"
      v-bind="attrs"
      v-on="$listeners"
    >
      <slot>{{ label }}</slot>
    </v-btn>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import { RawLocation } from 'vue-router';

@Component
export default class iButton extends Vue {
  @Prop({ required: true, type: String })
  name!: string;

  @Prop({ type: String })
  id?: string;

  @Prop({ default: 'accent' })
  color!: string;

  @Prop()
  to?: string | RawLocation;

  @Prop()
  href?: string | RawLocation;

  @Prop()
  target?: string;

  @Prop({ default: 'button', type: String })
  type!: string;

  @Prop({ type: String })
  label?: string;

  @Prop({ default: false, type: Boolean })
  submit!: boolean;

  @Prop({ default: false, type: Boolean })
  text!: boolean;

  @Prop({ default: true, type: Boolean })
  tile!: boolean;

  @Prop({ default: false, type: Boolean })
  icon!: boolean;

  @Prop({ default: false, type: Boolean })
  outlined!: boolean;

  @Prop({ default: false, type: Boolean })
  exact!: boolean;

  @Prop({ default: false, type: Boolean })
  loading!: boolean;

  @Prop({ default: false, type: Boolean })
  disabled!: boolean;

  protected get attrs() {
    return {
      id: this.id || `id-${this.name}`,
      name: this.name,
      text: !this.submit,
      tile: this.tile,
      icon: this.icon,
      outlined: this.outlined,
      color: this.color,
      disabled: this.disabled,
      loading: this.loading,
    };
  }
}
</script>

<style lang="stylus">
.n-button {
  .v-btn {
    &.v-size--default {
      @extend $text-default;
    }
  }

  .v-btn--tile {
    min-width: auto !important;
    padding: 0 12px !important;
  }
}
</style>
