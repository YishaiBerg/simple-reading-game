<template>
  <div>
    <q-card class="bg-negative text-white q-py-md">
      <q-card-section>
        <div class="text-h2 text-center">תשובה לא נכונה</div>
      </q-card-section>

        <div class="text-center">
            <q-btn color="primary" @click="$emit('close')">המשך במשחק</q-btn>
        </div>
    </q-card>
  </div>
</template>

<script>
export default {
  name: 'answer-wrong'
}
</script>

<style lang="scss" scoped></style>
