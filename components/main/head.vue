<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

const selectedLang = ref("ru");
const isLangDropdownOpen = ref(false);
const emit = defineEmits(["openModal"]);

const changeLang = (val) => {
  selectedLang.value = val;
};

const handleClickOutside = (event) => {
  const dropdown = document.querySelector(".lang");
  if (dropdown && !dropdown.contains(event.target)) {
    isLangDropdownOpen.value = false;
  }
};

onMounted(() => {
  document.addEventListener("click", handleClickOutside);
});

onBeforeUnmount(() => {
  document.removeEventListener("click", handleClickOutside);
});
</script>

<template>
  <div class="container">
    <div class="flex justify-between head items-center">
      <div class="flex items-center gap-5">
        <NuxtLink to="/">
          <span class="logo">Logo</span>
        </NuxtLink>
        <div class="text-lg flex items-center gap-2 point">
          <span class="font-medium p-1">Москва и МО</span>

          <IconChevron class="text-2xl" />
        </div>
        <div
          class="lang text-base rounded-xs font-medium relative point"
          @click.stop="isLangDropdownOpen = !isLangDropdownOpen"
        >
          <span class="flex items-center gap-1 uppercase p-1">
            {{ selectedLang }}
            <IconChevron
              class="text-2xl"
              :class="{ 'rotate-90': isLangDropdownOpen }"
            />
          </span>
          <div
            v-if="isLangDropdownOpen"
            class="absolute bg-white-300 flex flex-col gap-1 w-full rounded-xs"
          >
            <span
              @click="changeLang('ru')"
              class="w-full p-1 rounded-xs cursor-pointer"
            >
              RU
            </span>
            <span
              @click="changeLang('en')"
              class="w-full p-1 rounded-xs cursor-pointer"
            >
              EN
            </span>
          </div>
        </div>
      </div>
      <div class="flex items-center gap-5 text-xl text-dark-100">
        <span class="p-2 rounded-xs icon-bg flex items-center point">
          <IconHeart class="" />
        </span>
        <span  @click="$emit('openModal')" class="p-2 rounded-xs icon-bg flex items-center point">
          <IconMsg class="" />
        </span>

        <button
          class="text-lg py-1 px-5 h-8 flex items-center rounded-sm text-white btn-blue btn point"
        >
          Разместить объявление
        </button>

        <img src="/img/profil.webp" class="h-8" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.head {
  padding: 20px 0;
}

.logo {
  font-size: 32px;
  font-weight: bold;
  color: #1122bb;
}

.lang {
  border: none;
  outline: none;
  cursor: pointer;
}

.lang div {
  top: 32px;

  z-index: 10;
}

.lang div span:hover {
  background: rgba(17, 34, 187, 0.1);
}

.rotate-90 {
  transform: rotate(180deg);
}
.icon-bg:hover {
  background: #f3f3f6;
}
</style>
