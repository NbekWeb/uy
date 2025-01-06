<script setup>
const data = [
  {
    name: "В районе",
    childs: [
      "Сокольники",
      "Солнцево",
      "Капотня",
      "Куркино",
      "Левобережный",
      "Кузьминки",
      "Все районы",
    ],
  },
  {
    name: "Улицы, районы, метро",
    childs: [
      "Улицы",
      "Районы",
      "Сравнение новостроек",
      "Станции пригородных поездов",
      "Станции метро",
      "Все регионы",
    ],
  },
  {
    name: "Комнатность",
    childs: [
      "Однокомнатные",
      "Двухкомнатные",
      "Трехкомнатные",
      "Многокомнатные",
      "Студии",
    ],
  },
  {
    name: "Города в области",
    childs: ["Щербинка", "Москва", "Зеленоград", "Московский", "Троицк"],
  },
  {
    name: "Тип сделки",
    childs: ["Снять", "Снять посуточно"],
  },
];

const additional = [
  "Вся недвижимость",
  "Реклама",
  "Стань частью команды",
  "Пользовательское соглашение",
  "Правила рекомендаций",
  "Помощь",
];

const email = "help@realty.yandex.ru";
</script>
<template>
  <div class="bg-dark-200 text-white py-5">
    <div class="container">
      <div class="pb-5 border-b-white5 flex justify-between">
        <div v-for="(items, i) of data" :key="i" class="flex flex-col gap10">
          <span class="font-semibold">{{ items.name }}</span>
          <div class="flex flex-col gap10 text-white2">
            <NuxtLink to="/" v-for="(item, j) of items.childs" :key="j">
              <span class="foot-item">{{ item }}</span>
            </NuxtLink>
          </div>
        </div>
      </div>
      <div
        class="py-5 border-b-white5 flex text-white2 items-center justify-between"
      >
        <div class="flex gap-5">
          <NuxtLink to="/" v-for="(item, j) of additional" :key="j">
            <span class="foot-item">{{ item }}</span>
          </NuxtLink>
        </div>
        <div class="flex items-center gap10 text-4xl">
          <IconVk class="point" />
          <IconTg class="point" />
        </div>
      </div>
      <div class="py-5  flex gap-25 text-white2">
        <div>
          Яндекс.Недвижимость — аренда и продажа недвижимости в Москве и МО:
          поможем сдать, снять, продать или купить квартиру или другое жилье.
          Проектные декларации на https://наш.дом.рф Юридическая поддержка по
          правовым вопросам:
          <a :href="`mailto:${email}`" class="text-blue-100">{{ email }}</a>
        </div>
        <div class="flex items-center gap10 text-sm">
          <span
            class="flex qr p-2 items-center bg-white justify-center rounded-lg"
          >
            <img src="/img/qr.svg" />
          </span>
          <div class="scan-qr flex flex-col gap10">
            <span class="">
              Отсканируйте QR-код, чтобы скачать приложение
            </span>
            <div class="flex gap-2 items-center text-base">
              <div class="flex gap-1 items-center">
                <IconStar class="" />
                <span class="text-sm">4.8</span>
              </div>
              <IconTg />
              <IconVk />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.foot-item:hover {
  color: #1122bb;
}
.qr {
  width: 100px;
  height: 100px;
}
.scan-qr {
  width: 160px;
}
</style>
