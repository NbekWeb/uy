<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const emit = defineEmits(["close"]);

const singleMsg = ref(false);
const notifications = ref(false);
const notificationRef = ref(null); // Reference to the notification modal

const toggle = () => {
  singleMsg.value = !singleMsg.value;
};

const toggleNotification = () => {
  event.stopPropagation()
  notifications.value = !notifications.value;
};

const handleClickOutside = (event) => {
  if (
    notificationRef.value &&
    !notificationRef.value.contains(event.target) &&
    notifications.value == true
  ) {
    notifications.value = false; // Hide the modal if clicked outside
  }
};

onMounted(() => {
  document.addEventListener("click", handleClickOutside);
});

onUnmounted(() => {
  document.removeEventListener("click", handleClickOutside);
});

const text = ref(""); // Content of the textarea
const textareaRef = ref(null); // Reference to the textarea element

const adjustHeight = () => {
  const textarea = textareaRef.value;
  if (textarea) {
    textarea.style.height = "auto"; // Reset height
    textarea.style.height = textarea.scrollHeight + "px"; // Set height to content
  }
};

onMounted(() => {
  adjustHeight(); // Adjust height on mount in case of default content
});
</script>

<template>
  <div class="modal-content text-dark-100 flex">
    <div class="messages">
      <div class="flex items-center gap10 p-5">
        <IconClose @click="$emit('close')" class="text-2xl close-btn point" />
        <span class="font-medium text-xl">Сообщения</span>
      </div>

      <div class="my-5 p-5">
        <button
          class="text-lg py-1 gap-2 w-full justify-center h-8 flex items-center rounded-sm text-white btn-blue btn point"
        >
          <IconRing class="text-xl" />
          Разместить объявление
        </button>
      </div>
      <div
        class="flex gap-5 chatbot p-5 point"
        @click="toggle"
        :class="singleMsg && 'bg-white-300'"
      >
        <img src="/img/chatbot.png " class="rounded-sm w-20" />
        <div class="flex-grow flex flex-col justify-between">
          <div class="flex justify-between items-center">
            <span class="text-xl">Я.Недвижимость</span>
            <span class="text-base text-grey-900"> 13:03</span>
          </div>
          <div class="text-sm text-grey-900">
            <span>Чат с поддержкой </span>
            <span class="limit2"
              >Здравствуйте! На связи бот 🙂 Уточните ваш вопрос. Попробую
              помочь.
            </span>
          </div>
        </div>
      </div>
    </div>
    <div class="single-msg flex flex-col justify-between" v-show="singleMsg">
      <div class="p-5 single-msg-head flex justify-between items-center">
        <span class="font-semibold text-lg"> Я.Недвижимость</span>
        <div class="relative">
          <IconDots
            @click="toggleNotification"
            class="text-xl text-grey-900 dots point"
          />
          <div
            v-if="notifications"
            ref="notificationRef"
            class="modal-dots absolute bg-white rounded-sm"
          >
            <div class="px-3 py-1 point flex items-center gap-2">
              <img src="/img/ring.svg" />
              <span> Отключить уведомления </span>
            </div>
          </div>
        </div>
      </div>
      <div class="p-5 flex flex-col gap-5">
        <div class="flex justify-center mb-5">
          <span class="text-grey-900">Сегодня</span>
        </div>
        <div class="chat bg-white-100 max-w-max relative">
          <div class="relative chat-content p-3 text-base">
            <span class="relative flex pr-3"
              >Здравствуйте! На связи бот 🙂 Уточните ваш вопрос. Попробую
              помочь.

              <span class="text-xs text-grey-900 absolute chat-time"
                >13:03</span
              >
            </span>
          </div>
          <IconChatborder class="text-white-100 chat-part absolute" />
        </div>
        <div class="send-msg flex w-full bg-white-100 gap10 items-end">
          <div class="gap10 min-h-10 flex items-center text-2xl text-grey-900">
            <IconSending class="point send-msg-icons" />
            <IconLoc class="point send-msg-icons" />
          </div>
          <div class="flex-grow min-h-10 flex items-center">
            <textarea
              ref="textareaRef"
              v-model="text"
              class="textarea w-full resize-none"
              @input="adjustHeight"
              rows="1"
              placeholder="Напишите сообщение..."
            ></textarea>
          </div>
          <div
            @click="
              () => {
                text = '';
              }
            "
            class="send-icon text-2xl flex items-center justify-center bg-blue-100 text-white rounded-full"
            :class="!text ? 'opacity-0' : 'opacity-100'"
          >
            <IconSend class="" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.close-btn {
  opacity: 60%;
}
.close-btn:hover {
  opacity: 100%;
}
.chatbot:hover {
  background: #f3f3f6;
}
.messages {
  width: 350px;
}
.single-msg {
  width: 550px;
  border-left: 1px solid rgba(0, 0, 0, 0.1);
}

.dots:hover {
  color: #1b1d29;
}

.single-msg-head {
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
}

.chat {
  border-radius: 16px 16px 16px 0;
}

.chat-content {
  z-index: 10;
  max-width: 360px;
}

.chat-part {
  bottom: -1px;
  left: -6px;
  z-index: 0;
}

.chat-time {
  bottom: -4px;
  right: 0px;
}
.send-msg {
  border-radius: 24px;
  padding: 2px 4px 2px 20px;
}

.textarea {
  border: none;
  outline: none;
  background: transparent;
  min-height: 1rem;
  height: auto; /* Allow the textarea to grow dynamically */
  overflow-y: hidden; /* Prevent vertical scrollbars */
  resize: none; /* Disable manual resizing */
  width: 100%; /* Full width for better usability */
  font-size: 16px; /* Match font size to ensure consistent height */
}
.send-icon {
  min-width: 40px;
  min-height: 40px;
  width: 40px;
  height: 40px;
}

.send-msg-icons:hover {
  color: #1b1d29;
}

.modal-dots {
  top: 24px;
  right: 0px;
  min-width: max-content;
  padding: 12px 0;
  box-shadow: 0 16px 48px 0 rgba(0, 0, 0, 0.16);
}

.modal-dots div:hover {
  background: #f3f3f6;
}

.modal-dots div img {
  width: 24px;
}
</style>
