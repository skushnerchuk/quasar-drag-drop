<template>
  <div
    class="dropzone child-dropzone flex flex-center shadow-20"
    style="width: 300px; height: 300px; position: relative"
    @dragenter="dragEnter"
    @dragleave="dragLeave"
    @dragover="dragOver"
    @drop="drop"
  >
    <div
      v-if="enterCount !== 0"
      class="z-top flex dropzone-overlay text-white"
    >
      <div>
        <div class="text-h5 text-bold q-pt-lg text-center">
          File upload
        </div>
        <div class="text-caption q-pa-lg text-center">
          Supported only:  XLS, XLSX
        </div>
      </div>
    </div>

    <q-card bordered class="flex column flex-center" flat>
      <q-card-section>
        <div>
          Uploaded: {{ files.length }}
        </div>
      </q-card-section>
      <q-card-actions align="center">
        <q-btn color="primary" label="Reset" unelevated @click="files = []"/>
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
      files: [],
      allowedExt: /(\.xls|\.xlsx)$/i,
      maxSize: 3 * 1024 * 1024, // 3 Mb
      maxFiles: 1
    }
  },

  methods: {
    drop (event) {
      event.preventDefault()
      const files = event.dataTransfer.files
      if (!files || this.files.length + files.length > this.maxFiles) {
        return
      }
      for (const item of files) {
        if (!this.isFileExist(item) && this.isSupportedFile(item)) {
          this.files.push(item)
        }
      }
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
    },

    isSupportedFile (fileObj) {
      return this.isSupportedType(fileObj) && this.isSupportedSize(fileObj)
    },

    isFileExist (fileObj) {
      for (const item of this.files) {
        if (item.name === fileObj.name &&
          item.size === fileObj.size &&
          item.lastModifiedDate.toString() === fileObj.lastModifiedDate.toString()
        ) {
          return true
        }
      }
    },

    isSupportedType (fileObj) {
      return this.allowedExt.exec(fileObj.name);
    },

    isSupportedSize (fileObj) {
      return fileObj <= this.maxSize
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
