<script setup>
import { ref, computed, watch } from 'vue'
const agreement = ref(false) //single checkbox (true/false)
const favorConverters = ref([]) //multiple checkbox (multitple values)
const unitType = ref('length') //single value of radio button
const feedback = ref('')
// const selectOptions = computed(() => {
//   if (unitType.value === 'length')
//     return `<option value="centimetre">Centimetre</option>
//             <option value="inch">Inch</option>`
//   else if (unitType.value === 'temperature')
//     return `<option value="celsius">Celsius</option>
//             <option value="fahrenheit">Fahrenheit</option>`
// })
const selectOptions = ref('')
const sourceUnit = ref('')
const targetUnit = ref('')
const sourceValue = ref(1)
// const targetValue = ref(1)

const targetValue = computed(() => {
  if (
    unitType.value === 'length' &&
    sourceUnit.value === 'centimetre' &&
    targetUnit.value === 'inch'
  )
    return (sourceValue.value / 2.54).toFixed(2)
  else if (
    unitType.value === 'length' &&
    sourceUnit.value === 'inch' &&
    targetUnit.value === 'centimetre'
  )
    return (sourceValue.value * 2.54).toFixed(2)
  else if (
    unitType.value === 'temperature' &&
    sourceUnit.value === 'celsius' &&
    targetUnit.value === 'fahrenheit'
  )
    return (sourceValue.value * (9 / 5) + 32).toFixed(2)
  else if (
    unitType.value === 'temperature' &&
    sourceUnit.value === 'fahrenheit' &&
    targetUnit.value === 'celsius'
  )
    return ((sourceValue.value - 32) * (5 / 9)).toFixed(2)
  else return sourceValue.value
})
watch(
  unitType,
  () => {
    if (unitType.value === 'length') {
      selectOptions.value = `<option value="centimetre">Centimetre</option>
            <option value="inch">Inch</option>`
      sourceUnit.value = 'centimetre'
      targetUnit.value = 'inch'
    } else if (unitType.value === 'temperature') {
      selectOptions.value = `<option value="celsius">Celsius</option>
            <option value="fahrenheit">Fahrenheit</option>`
      sourceUnit.value = 'celsius'
      targetUnit.value = 'fahrenheit'
    }
  },
  { immediate: true }
)
</script>

<template>
  <div class="w-full max-w-3xl p-10 shadow-2xl space-y-2">
    <!-- converter form -->
    <div>
      <h1 class="text-green-700 text-3xl">Converter</h1>
    </div>

    <form action="" class="space-y-2">
      <div class="flex space-x-3">
        <input type="checkbox" v-model="agreement" />
        <p>I read and accept converter application policy</p>
      </div>

      <div class="flex space-x-3">
        <p>Favorite Converters:</p>
        <input
          type="checkbox"
          value="unit converter"
          v-model="favorConverters"
        />
        <label>Unit Converter</label>
        <input
          type="checkbox"
          value="conversion calculator"
          v-model="favorConverters"
        />
        <label>Conversion Calculator</label>
      </div>

      <div class="flex space-x-3">
        <input type="radio" value="length" v-model="unitType" />
        <label>Length</label>
        <input type="radio" value="temperature" v-model="unitType" />
        <label>Temperature</label>
      </div>

      <div class="flex space-x-3 items-center">
        <div class="w-1/2 flex flex-col">
          <input
            v-model.number="sourceValue"
            type="text"
            value="1"
            class="text-center h-20 text-2xl border border-gray-200 outline-none"
          />
          <!-- dynamic options -->
          <select
            v-model="sourceUnit"
            v-html="selectOptions"
            class="bg-gray-50 border border-slate-300 outline-none"
          ></select>
        </div>
        <p class="text-3xl">=</p>
        <div class="w-1/2 flex flex-col">
          <div
            class="flex justify-center items-center h-20 text-2xl border border-gray-200"
          >
            <label>{{ targetValue }}</label>
          </div>

          <!-- dynamic options -->
          <select
            v-model="targetUnit"
            v-html="selectOptions"
            class="bg-gray-50 border border-slate-300 outline-none"
          ></select>
        </div>
      </div>
      <div class="flex flex-col">
        <label>Give us your feedback:</label>
        <textarea
          v-model="feedback"
          class="border border-slate-300 outlne-none max-h-10"
        ></textarea>
      </div>
      <button
        class="bg-green-700 text-white hover:bg-green-600 rounded-lg px-5 py-1"
      >
        Submit
      </button>
    </form>
  </div>
</template>

<style scoped></style>