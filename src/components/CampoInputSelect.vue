<template>
  <div>
    <input
      v-if="type === 'text'"
      :value="inputModel"
      @input="$emit('update:modelValue', $event)"
      :placeholder="placeholder"
      class="input"
    />

    <div v-else>
      <div class="select is-fullwidth">
        <select
          :value="selectModel"
          @change="$emit('update:modelValue', $event.target.value)"
        >
          <option v-for="option in options" :key="option" :value="option">
            {{ option }}
          </option>
        </select>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CampoInputSelect",
  props: {
    type: String,
    inputModel: String,
    selectModel: String,
    options: Array,
    placeholder: String,
  },
};
</script>
