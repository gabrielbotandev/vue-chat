<template>
  <VContainer>
    <VForm @submit.prevent="onSubmit">
      <VCard max-width="600" class="mx-auto pa-5">
        <VCardTitle>
          <div class="d-flex align-center justify-center">
            <VIcon icon="mdi-forum" color="primary"/>
            <h3 class="ml-2 text-primary">Vue Chat</h3>
          </div>
        </VCardTitle>
        <VCardText class="py-4">
          <VTextField label="Nome de usuário" v-model="state.username"></VTextField>
          <VSelect :items="rooms" label="Sala" v-model="state.room"></VSelect>
        </VCardText>
        <VCardActions>
          <VBtn
            block
            color="primary"
            :disabled="!state.username || !state.room"
            variant="outlined"
            type="submit"
          >
            Entrar na sala
          </VBtn>
        </VCardActions>
      </VCard>
    </VForm>
  </VContainer>
</template>

<script lang="ts" setup>
import { reactive } from 'vue';
import { useRouter } from 'vue-router';
const router = useRouter();
const rooms = ['Front-end', 'Back-end', 'Fullstack', 'DevOps'];
const state = reactive({
  username: '',
  room: rooms[0],
});
const onSubmit = () => {
  console.log('[SUBMIT]');
  router.push(`/chat?username=${state.username}&room=${state.room}`);
};


</script>