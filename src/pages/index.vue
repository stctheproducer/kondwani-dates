<script setup lang="ts">
/* eslint-disable no-console */
import { ref, watch } from 'vue'
import { DateTime } from 'luxon'
const startDate = ref(new Date().toISOString().split('T')[0])
const endDate = ref<string|null>(null)
const quarters = [1, 2, 3, 4]
const quarter = ref<number>(1)

const calculateEndDate = (quarter: number, startDate: string) => {
  const endOfStartDateQuarter = DateTime.fromISO(startDate).endOf('quarter')
  const localEndDate = quarter > 1 ? endOfStartDateQuarter.plus({ quarters: quarter - 1 }) : endOfStartDateQuarter
  endDate.value = localEndDate.endOf('day').toISODate()
}

watch([quarter, startDate], ([quarter, startDate]) => {
  calculateEndDate(quarter, startDate)
})
</script>

<template>
  <div>
    <div class="py-4" />

    <div class="mx-auto my-2 w-[250px]">
      <label for="quarter" class="font-medium text-sm text-left text-gray-700 block">Number of Quarters</label>
      <select id="quarter" v-model="quarter" name="quarter" class="rounded-md border-gray-300 mt-1 text-base w-full py-2 pr-10 pl-3 block sm:text-sm focus:outline-none focus:border-indigo-500 focus:ring-indigo-500">
        <option v-for="(q, index) in quarters" :key="index">
          {{ q }}
        </option>
      </select>
    </div>

    <div class="mx-auto my-2 w-[250px]">
      <label for="start-date" class="font-medium text-sm text-left text-gray-700 block">Start Date</label>
      <div class="mt-1">
        <input
          id="start-date"
          v-model="startDate"
          type="date"
          name="start-date"
          class="rounded cursor-not-allowed bg-gray-100 border-gray-300 shadow-sm w-full py-2 px-4 block focus:(border-gray-300 ring-transparent) "
          disabled
        />
      </div>
    </div>

    <div class="mx-auto my-2 w-[250px]">
      <label for="end-date" class="font-medium text-sm text-left text-gray-700 block">End Date</label>
      <div class="mt-1">
        <input
          id="end-date"
          v-model="endDate"
          type="date"
          name="end-date"
          class="rounded cursor-not-allowed bg-gray-100 border-gray-300 shadow-sm ring-transparent w-full py-2 px-4 block focus:(border-gray-300 ring-transparent) "
          disabled
        />
      </div>
    </div>

    <div class="mx-auto my-2 w-[250px]">
      <div class="text-left">
        <p><strong>Quarter:</strong> {{ quarter }}</p>
        <p><strong>Start date:</strong> {{ startDate }}</p>
        <p><strong>End date:</strong> {{ endDate }}</p>
      </div>
    </div>
  </div>
</template>
