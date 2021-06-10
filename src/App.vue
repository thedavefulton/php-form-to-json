<template>
  <div class="text-center mt-4">
    <h1 class="text-4xl tracking-tight font-extrabold text-gray-900 sm:text-5xl md:text-6xl">
      PHP Form
      <span class="text-indigo-600">to JSON</span>
    </h1>
    <p class="mt-3 max-w-md mx-auto text-base text-gray-500 sm:text-lg md:mt-5 md:text-xl md:max-w-3xl">
      Move over sliced bread! Now you can easily convert a raw PHP form query string to a formatted JSON object.
    </p>
  </div>
  <div class="flex flex-row">
    <div class="h-screen w-1/2 p-4">
    <label for="form-data" class="block text-sm font-medium text-gray-700 mb-1">Raw Query String</label>
      <textarea id="form-data" class="block w-full h-5/6 focus:outline-none rounded-md focus:border-indigo-500 focus:border-indigo-500 border-gray-300" v-model="formData"/>
    </div>
    <div class="h-screen w-1/2 p-4">
      <label for="json-data" class="block text-sm font-medium text-gray-700 mb-1">Formatted JSON</label>
      <textarea id="json-data" class="block w-full h-5/6 focus:outline-none rounded-md focus:border-indigo-500 focus:border-indigo-500 border-gray-300" v-model="jsonData"/>
    </div>
  </div>
</template>

<script lang="ts">
import {defineComponent, ref, watch} from 'vue'
import qs from 'qs'

export default defineComponent({
  name: 'App',
  setup() {
    const formData = ref("")
    const jsonData = ref("")

    watch(formData, (value) => {
      jsonData.value = JSON.stringify(qs.parse(value, {depth: 10}), null, 2)
    })

    // watch(jsonData, (value) => {
    //   formData.value = qs.stringify(JSON.parse(value), {arrayFormat: "brackets"})
    //   console.log(value)
    // })
    return {formData, jsonData}
  }
})
</script>
