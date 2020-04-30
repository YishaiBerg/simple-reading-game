<template>
  <div>
    <q-card class="bg-positive text-white q-py-md">
      <q-card-section>
        <div class="text-h2 text-center">תשובה נכונה</div>
      </q-card-section>

        <div class="text-center">
            <q-btn @click="$emit('new-game')">משחק חדש</q-btn>
        </div>
    </q-card>
  </div>
</template>

<script>
export default {
  name: 'answer-correct'
}
</script>

<style lang="scss" scoped></style>
