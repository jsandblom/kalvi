<script setup lang="ts">
import { useVuelidate } from '@vuelidate/core'
import { between, required, requiredIf } from '@vuelidate/validators'

const user = useUserStore()
const name = $ref(user.savedName)

const router = useRouter()
const go = () => {
  if (name)
    router.push(`/hi/${encodeURIComponent(name)}`)
}

const state = reactive({
  vad: '',
  mängd: 1,
  enhet: 'st',
  kcal: 500,
})
const rules = reactive({
  vad: { required },
  mängd: between(0, 1500),
  enhet: requiredIf(state.mängd > 0),
  kcal: { required },
})
const v$ = useVuelidate(rules, state)
</script>

<template>
  <div :class="{ error: v$.vad.$errors.length }">
    vad:
    <input v-model="state.vad" class="border border-grey-300 rounded">
    <div v-for="error of v$.vad.$errors" :key="error.$uid" class="input-errors">
      <div class="error-msg">
        {{ error.$message }}
      </div>
    </div>
  </div>
  <snabbVy />
</template>

<route lang="yaml">
meta:
  layout: home
</route>
