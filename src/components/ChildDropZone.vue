<template>
  <div
    class="dropzone child-dropzone flex flex-center shadow-20"
    @dragenter="dragEnter"
    @dragleave="dragLeave"
    @dragover="dragOver"
    @drop="drop"
    style="width: 300px; height: 300px; position: relative"
  >
    <div
      class="z-top flex dropzone-overlay text-white"
      v-if="enterCount !== 0"
    >
      <div>
        <div class="text-h5 text-bold q-pt-lg text-center">
          Загрузка файлов
        </div>
        <div class="text-caption q-pa-lg text-center">
          Поддерживаются форматы PDF, XLS, XLSX, DOC, DOCX
        </div>
      </div>
    </div>

    <q-card bordered flat class="flex column flex-center">
      <q-card-section>
        <div>
          Загружено: {{ count }}
        </div>
      </q-card-section>
      <q-card-actions align="center">
        <q-btn unelevated color="primary" label="Сброс" @click="count = 0"/>
      </q-card-actions>
    </q-card>
  </div>
</template>

<script>
export default {
  name: 'ChildDropZone',

  data () {
    return {
      enterCount: 0,
      count: 0
    }
  },

  methods: {
    drop (event) {
      event.preventDefault()
      this.count++
      this.enterCount = 0
    },

    dragEnter (event) {
      event.preventDefault()
      this.enterCount++
    },

    dragLeave (event) {
      event.preventDefault()
      this.enterCount--
    },

    dragOver (event) {
    }
  }
}
</script>

<style lang="sass" scoped>

.child-dropzone
  background: #ffffff
  margin-top: 50px
  color: black

</style>
