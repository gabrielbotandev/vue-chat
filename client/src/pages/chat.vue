<template>
  <VContainer>
    <VCard class="mx-auto pa-5">
      <VCardTitle class="pb-5">
        <div class="d-flex align-center justify-space-between text-primary">
          <div class="d-flex align-center">
            <VIcon icon="mdi-forum" color="primary" />
            <div class="font-weight-bold text-h6 ml-2 text-primary">
              Vue Chat
            </div>
          </div>
          <VBtn color="primary" elevation="0" @click="leaveRoom">
            Sair de {{ $route.query.room }}
          </VBtn>
        </div>
      </VCardTitle>
      <VDivider></VDivider>
      <VCardText class="py-6 px-0">
        <div class="d-flex">
          <!-- Sidebar -->
          <div class="py-4 px-6 bg-dark rounded-lg">
            <div class="mb-4">
              <div class="d-flex align-center mb-2 px-3 py-2 rounded-md">
                <VIcon icon="mdi-message" color="primary" />
                <div class="text-body-1 ml-2 text-primary">Sala</div>
              </div>
              <div class="mb-2 text-body-1 ml-2 text-capitalize">
                {{ currentRoom }}
              </div>
            </div>
            <div class="d-flex align-center mb-2 px-3 py-2 rounded-md">
              <VIcon icon="mdi-account-group" color="primary" />
              <div class="text-body-1 ml-2 text-primary">Usuários</div>
            </div>
            <v-list class="bg-dark py-0 px-0">
              <v-list-item v-for="(user, i) in users" :key="i">
                <v-list-item-title>{{ user.username }}</v-list-item-title>
                <VDivider
                  color="white"
                  v-if="user.username === route.query.username"
                ></VDivider>
              </v-list-item>
            </v-list>
          </div>
          <!-- Chat -->
          <div style="height: 400px" class="overflow-y-auto pl-6 flex-fill">
            <div
              class="bg-transparent w-full mb-3 d-flex"
              v-for="(chat, i) in chats"
              :key="i"
              :class="{
                'justify-center': chat.username === 'Aviso',
                'justify-end': chat.username === route.query.username,
                'justify-start': chat.username !== route.query.username,
              }"
            >
              <div>
                <!-- Cabeçalho (Nome e Horário) -->
                <div
                  v-if="chat.username !== 'Aviso'"
                  class="d-flex align-center text-xs mb-1 px-2"
                >
                  <span class="font-weight-bold mr-2 text-white">
                    {{ chat.username }}
                  </span>
                  <span class="opacity-50">
                    {{ chat.time }}
                  </span>
                </div>
                <!-- Caixa de Mensagem -->
                <div
                  class="px-6 py-2 rounded-md"
                  :class="{
                    'opacity-20 text-center':
                      chat.username === 'Aviso',
                    'bg-grey-darken-3 rounded-lg text-right':
                      chat.username === route.query.username,
                    'bg-grey-darken-2 rounded-lg text-left':
                      chat.username !== route.query.username &&
                      chat.username !== 'Aviso',
                  }"
                >
                  <div class="text-body-1">
                    {{ chat.text }}
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </VCardText>
      <VDivider></VDivider>
      <VCardActions class="pt-6">
        <form class="w-100" @submit.prevent="onSubmit">
          <VTextField
            hide-details
            variant="solo"
            elevation="0"
            rounded="lg"
            placeholder="Digite sua mensagem..."
            v-model="message"
          >
            <template #append-inner>
              <VBtn
                append-icon="mdi-send-variant"
                rounded="lg"
                class="bg-primary text-white px-6"
                @click="onSubmit"
              >
                Enviar
              </VBtn>
            </template>
          </VTextField>
        </form>
      </VCardActions>
    </VCard>
  </VContainer>
</template>

<script setup lang="ts">
type Chat = {
  username: string;
  text: string;
  time: string;
  room?: string;
};
type User = {
  id: string;
  username: string;
  room: string;
};
import { useRoute, useRouter } from "vue-router";
import { ref, onMounted, onBeforeUnmount, nextTick } from "vue";
import { io, type Socket } from "socket.io-client";
const route = useRoute();
const router = useRouter();

const message = ref("");
const chats = ref<Chat[]>([]);
const users = ref<User[]>([]);
const currentRoom = ref("");
const socket = ref<Socket>();
const onSubmit = async () => {
  socket.value?.emit("chatMessage", message.value);
  await nextTick(() => (message.value = ""));
};

const leaveRoom = () => {
  socket.value?.emit('leaveRoom', { room: route.query.room });
  router.push("/");
};

onMounted(() => {
  socket.value = io("http://localhost:3001");
  const { username, room } = route.query as Partial<Chat>;

  if (!username || !room) {
    router.push("/");
  }
  socket.value?.emit("joinRoom", { username, room });
  socket.value?.on("roomUsers", (response: { room: string; users: User[] }) => {
    users.value = response.users;
    currentRoom.value = response.room;
  });
  socket.value?.on("message", (message: Chat) => {
    chats.value.push(message);
  });
});
onBeforeUnmount(() => {
  console.log("[DISCONNECT_BLOCK]");
  socket.value?.disconnect();
});
</script>

<style scoped></style>
