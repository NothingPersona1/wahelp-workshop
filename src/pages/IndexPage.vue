<template>
  <q-page class="flex flex-start column">
    <div class="container q-py-xl q-mx-auto">

      <div>
        <img class="logo" src="~assets/images/wahelp-logo.svg" />
      </div>

      <div class="offer flex column">
        <div class="offer_date flex">
          <div class="offer_date__item flex items-center">
            Бесплатный вебинар
          </div>
          <div class="offer_date__item flex items-center">
            01 января <span class="q-px-sm">•</span> 12:00 МСК
          </div>
        </div>

        <h1 class="offer_caption">Как <span class="text-whaccent">запустить</span> свой чат с клиентами прямо в журнале
          записи Yclients</h1>
      </div>

      <div class="cta flex column">
        <q-btn class="cta_button" unelevated color="accent" text-color="primary" label="Зарегистрироваться"
          @click="modal = true" />

        <div class="cta_subtitle flex row no-wrap">
          <q-icon size="1.4rem" name="fa fa-gift" />
          Зарегистрируйся и мы тебя погладим по головке
        </div>
      </div>

      <img class="anton desktop-only" src="~assets/images/anton2.png" alt="">

      <div class="info desktop-only flex row no-wrap">
        <div class="info_icon bg-primary q-pa-md"><q-icon size="1.5rem" color="dark" name="fa fa-square-check" />
        </div>
        <div>
          <p class="info_title">Заголовок о том, что будет</p>
          <p class="info_subtitle">Текст о том, что было, есть и еще только будет на данном вебинаре</p>
        </div>
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
import { useQuasar, useMeta } from 'quasar'
import { ref } from 'vue'
import axios from 'axios'

const $q = useQuasar()
$q.screen.setSizes({ sm: 500, md: 700, lg: 1000, xl: 2000 })

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