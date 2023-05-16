<template>
  <q-page class="flex flex-start column">
    <div class="container q-py-xl q-px-xl q-mx-auto flex column justify-between">

      <div>
        <img class="logo" src="~assets/images/wahelp-logo.svg" />
      </div>

      <div class="offer flex column">
        <div class="offer_date flex">
          <div class="offer_date__item flex items-center">
            Бесплатный вебинар
          </div>
          <div class="offer_date__item flex items-center">
            25 мая <span class="q-px-sm">•</span> 15:00 МСК
          </div>
        </div>

        <h1 class="offer_caption"><span class="text-whaccent">3 секрета</span> успешного найма сотрудников для создания
          команды мечты</h1>

        <div class="offer_subtitle desktop-only">Как за 2 дня получить 50 откликов на объявление</div>
      </div>

      <div class="cta flex column q-mb-lg">
        <q-btn class="cta_button" unelevated color="accent" text-color="primary" label="Зарегистрироваться"
          @click="modal = true" />

        <div class="cta_subtitle flex row no-wrap desktop-only q-ml-md">
          <q-icon size="1.4vw" name="fa fa-gift" />
          Подключим 5 мессенджеров к вашему<br />чату с клиентами в YCLIENTS
        </div>
        <div class="cta_subtitle flex row no-wrap mobile-only">
          <q-icon size="1.2rem" name="fa fa-gift" />
          Подключим 5 мессенджеров<br />к вашему чату с клиентами<br />в YCLIENTS
        </div>
      </div>

    </div>

    <div class="author desktop-only">
      <img class="author_img" src="~assets/images/yana.png">

      <div class="author_name flex column">
        <div class="author_name__title">Яна Иванченко</div>
        <div class="author_name__subtitle">владелец бьюти-студий<br>и бизнес-тренер</div>
      </div>
    </div>

    <div class="info desktop-only flex row no-wrap">
      <div class="info_icon bg-primary"><q-icon size="1.5rem" color="dark" name="fa fa-square-check" />
      </div>
      <div>
        <p class="info_title">Как решать задачи<br />в бизнесе</p>
        <p class="info_subtitle">Встреча с экспертом для тех, кто ищет работающие решения для развития бизнеса и
          увеличения прибыли</p>
      </div>
    </div>

  </q-page>

  <q-dialog transition-show="fade" transition-hide="fade" transition-duration="500" persistent v-model="modal">
    <q-card class="modal">
      <q-card-section class="flex justify-end">
        <q-btn icon="close" color="primary" flat round dense v-close-popup />
      </q-card-section>
      <q-card-section class="q-px-xl q-py-none">
        <h3 class="q-ma-none">Оставить заявку</h3>
      </q-card-section>
      <q-card-section class="q-px-xl">
        <q-form @submit="onSubmit" class="q-mt-xl flex column">
          <q-input label-color="dark" bg-color="secondary" standout="bg-accent text-primary" v-model="clientName"
            name="name" lazy-rules="ondemand" :rules="[val => !!val || 'Необходимо заполнить']"
            label="Как к вам обращаться?" />
          <q-input label-color="dark" bg-color="secondary" standout="bg-accent text-primary" v-model.number="clientNumber"
            name="phone" mask="+7 (###) ### - ####" lazy-rules="ondemand"
            :rules="[val => !!val || 'Необходимо заполнить']" label="Номер телефона" class="q-mt-sm" />
          <q-checkbox size="sm" v-model="checkbox" dark color="dark" label="Принимаю политику конфиденциальности" />
          <q-btn :disable="!checkbox" class="q-mt-lg q-py-md" label="Отправить" type="submit" rounded color="accent" />
        </q-form>
      </q-card-section>
    </q-card>

  </q-dialog>
</template>

<script setup>
import { useMeta } from 'quasar'
import { ref } from 'vue'
import axios from 'axios'

const metaData = {
  title: 'Вебинар',
  titleTemplate: title => `${title} - Wahelp Workshop`,
  meta: {
    description: { name: 'description', content: 'Page 1' },
    equiv: { 'http-equiv': 'Content-Type', content: 'text/html; charset=UTF-8' },
  },
}

useMeta(metaData)

const modal = ref(false);
const clientName = ref('');
const clientNumber = ref();
const checkbox = ref(false);

const onSubmit = () => {
  const formData = {
    name: clientName.value,
    phone: clientNumber.value,
  }

  axios.post('/', formData)
    .then(response => {
      console.log(response.data)
    })
    .catch(err => {
      console.log(err)
    })
};
</script>

<style></style>