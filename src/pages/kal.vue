<script setup lang="ts">
import { useVuelidate } from '@vuelidate/core'
import { between, required, requiredIf } from '@vuelidate/validators'

const user = useUserStore()
const name = $ref(user.savedName)

const router = useRouter()

const state = reactive({
  vad: '',
  mängd: 1,
  enhet: 'st',
  kcal: 500,
})
const rules = reactive({
  vad: { required },
  mängd: { between01500: between(0, 1500) },
  enhet: { reqIfMängd: requiredIf(state.mängd > 0) },
  kcal: { required },
})
const v$ = useVuelidate(rules, state)
const kal = ''
</script>

<template>
  <div>
    <div :class="{ error: v$.vad.$errors.length }">
      vad:
      <input v-model="state.vad" class="border border-grey-300 rounded">
      <div v-for="error of v$.vad.$errors" :key="error.$uid" class="input-errors">
        <div class="error-msg">
          {{ error.$message }}
        </div>
      </div>
    </div>
    <div :class="{ error: v$.mängd.$errors.length }">
      mängd:
      <input v-model="state.mängd" class="border border-grey-300 rounded">
      <div v-for="error of v$.mängd.$errors" :key="error.$uid" class="input-errors">
        <div class="error-msg">
          {{ error.$message }}
        </div>
      </div>
    </div>
    <div :class="{ error: v$.enhet.$errors.length }">
      vad:
      <input v-model="state.enhet" class="border border-grey-300 rounded">
      <div v-for="error of v$.enhet.$errors" :key="error.$uid" class="input-errors">
        <div class="error-msg">
          {{ error.$message }}
        </div>
      </div>
    </div>
    <div :class="{ error: v$.kcal.$errors.length }">
      vad:
      <input v-model="state.kcal" class="border border-grey-300 rounded">
      <div v-for="error of v$.kcal.$errors" :key="error.$uid" class="input-errors">
        <div class="error-msg">
          {{ error.$message }}
        </div>
      </div>
    </div>
    <snabbVy />
  </div>
</template>

<route lang="yaml">
meta:
  layout: home
</route>
