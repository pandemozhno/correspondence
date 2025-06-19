<script setup>
import cButton from './components/cButton.vue'
import cList from './components/cList.vue'
import cInput from './components/cInput.vue'
import { ref, reactive } from "vue"

const pull = ref([])
const result = reactive({})

const resultInput = ref(null)
const pullInput = ref(null)

const resultSelected = ref(null)
const pullSelected = ref(null)

const toResult = () => {
  result[resultSelected.value] = pull.value[pullSelected.value]
  pull.value.splice(pull.value[pullSelected.value], 1)
}

const toPull = () => {
  pull.value.push(result[resultSelected.value])
  result[resultSelected.value] = null
}

const save = () => {
  localStorage.setItem('correcpondence', JSON.stringify({
    result,
    pull: pull.value
  }))
}

const load = () => {
  const loaded = localStorage.getItem('correcpondence')
  const parsed = JSON.parse(loaded)
  pull.value = pull.value.concat(parsed.pull)
  Object.assign(result, parsed.result)
}


</script>

<template>
  <header class="header">
    <h1>Correspondence</h1>
    <div style="margin-left: auto;">
      <!-- <cButton @click="save" style="margin-right: 1rem;">Импорт</cButton>
      <cButton @click="load" style="margin-right: 3rem;">Экспорт</cButton> -->
      <cButton @click="save" style="margin-right: 1rem;">Сохранить</cButton>
      <cButton @click="load">Загрузить</cButton>
    </div>
  </header>

  <main class="main">
    <div class="result">
      <h2>Результат</h2>
      <div>
        <cInput v-model="resultInput" style="margin-right: 1rem;" />
        <cButton @click="result[resultInput] = null">Добавить</cButton>
      </div>
      <cList style="margin: 2rem 0;" :items="result" v-model:selected="resultSelected"/>
      <cButton @click="toPull">Вернуть в список</cButton>
    </div>

    <div class="pull">
      <div class="h" style="margin-bottom: 2rem;">
        <h2>Список</h2>
        <cButton style="margin-left: 1rem;" @click="toResult">Привязать к результату</cButton>
      </div>
      
      <div>
        <cInput v-model="pullInput" style="margin-right: 1rem;"/>
        <cButton @click="pull.push(pullInput)">Добавить</cButton>
      </div>
      <cList style="margin: 2rem 0;" :items="pull" v-model:selected="pullSelected"/>
      
    </div>
  </main>
</template>

<style scoped>
#app {
  display: flex;
  flex-direction: column;
}
.header {
  display: flex;
  padding: 1rem;
}

.main {
  padding: 1rem;
  justify-content: space-around;
}
.pull {
  margin-top: 2rem;
}
.v {
  display: flex;
  flex-direction: column;
}
.h {
  display: flex;
}
</style>
