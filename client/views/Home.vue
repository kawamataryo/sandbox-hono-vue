<template>
  <div class="min-h-screen flex items-center justify-center p-4">
    <div class="max-w-xl w-full space-y-4">
      <Card>
        <CardHeader>
          <CardTitle>Hono and Vue SPA Example</CardTitle>
        </CardHeader>
        <CardContent class="space-y-4">
          <div class="space-y-2">
            <Label for="text">Text</Label>
            <Input id="text" v-model="text" placeholder="Type here" />
          </div>
          <div class="flex gap-2">
            <Button :disabled="loading" @click="onSubmit">
              {{ loading ? 'Sending...' : 'Send' }}
            </Button>
            <Button variant="outline" @click="onClear">Clear</Button>
          </div>
          <div v-if="error" class="text-sm text-red-600">{{ error }}</div>
        </CardContent>
        <CardFooter>
          <div class="w-full">
            <Label>Response</Label>
            <pre class="mt-2 rounded-md border p-3 text-sm overflow-x-auto"
              >{{ responseText }}
            </pre>
            <div class="mt-4">
              <RouterLink to="/about">
                <Button variant="ghost" size="sm">Go to About</Button>
              </RouterLink>
            </div>
          </div>
        </CardFooter>
      </Card>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { RouterLink } from 'vue-router'
import { Button } from '@/components/ui/button'
import { Input } from '@/components/ui/input'
import { Label } from '@/components/ui/label'
import {
  Card,
  CardContent,
  CardDescription,
  CardFooter,
  CardHeader,
  CardTitle,
} from '@/components/ui/card'

const text = ref('')
const loading = ref(false)
const error = ref<string | null>(null)
const responseText = ref('')

async function onSubmit() {
  error.value = null
  responseText.value = ''
  loading.value = true
  try {
    const res = await fetch('/api/echo', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ text: text.value }),
    })
    const data = await res.json()
    if (!res.ok) {
      throw new Error(data?.error || 'Request failed')
    }
    responseText.value = JSON.stringify(data, null, 2)
  } catch (e: any) {
    error.value = e?.message ?? 'Unexpected error'
  } finally {
    loading.value = false
  }
}

function onClear() {
  text.value = ''
  responseText.value = ''
  error.value = null
}
</script>

<style scoped></style>
