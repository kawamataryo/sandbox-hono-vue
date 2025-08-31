<template>
  <div class="min-h-screen flex items-center justify-center p-4">
    <div class="max-w-xl w-full">
      <Card>
        <CardHeader>
          <CardTitle>About</CardTitle>
          <CardDescription
            >Simple page to test Vue Router navigation.</CardDescription
          >
        </CardHeader>
        <CardContent class="space-y-4">
          <p class="text-sm text-muted-foreground">This is a secondary page.</p>
          <RouterLink to="/">
            <Button variant="outline">Back to Home</Button>
          </RouterLink>
        </CardContent>
      </Card>
    </div>
  </div>
</template>

<script setup lang="ts">
import { RouterLink } from 'vue-router'
import { Button } from '@/components/ui/button'
import {
  Card,
  CardContent,
  CardDescription,
  CardHeader,
  CardTitle,
} from '@/components/ui/card'
</script>

<style scoped></style>
