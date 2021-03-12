<template>
  <q-page class="flex flex-center">
    <div
      class="flex flex-center absolute-full"
      id="base"
      @dragenter="dragEnter"
      @dragleave="dragLeave"
      @dragover="dragOver"
      @drop="drop"
    >
      <div class="row q-gutter-lg">
        <child-drop-zone :class="[enterCount !== 0 ? 'dropzone-border' : '']"/>
        <child-drop-zone :class="[enterCount !== 0 ? 'dropzone-border' : '']"/>
      </div>
    </div>
  </q-page>
</template>

<script>
import ChildDropZone from 'components/ChildDropZone'
export default {
  name: 'PageIndex',

  components: { ChildDropZone },

  data () {
    return {
      enterCount: 0,
      activeId: ''
    }
  },

  computed: {
    dragState () {
      return this.enterCount !== 0
    }
  },

  methods: {
    dragEnter (event) {
      if (this.activeId === 'base') {
        event.dataTransfer.dropEffect = 'none'
      } else {
        event.dataTransfer.dropEffect = 'copy'
      }
      event.preventDefault()
      this.enterCount++
    },

    dragLeave (event) {
      event.preventDefault()
      this.enterCount--
    },

    dragOver (event) {
      this.activeId = event.target.id
      if (this.activeId === 'base') {
        event.dataTransfer.dropEffect = 'none'
      } else {
        event.dataTransfer.dropEffect = 'copy'
      }
      event.preventDefault()
    },

    drop (event) {
      this.enterCount = 0
    }
  }

}

</script>
