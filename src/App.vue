<template>
  <div id="app">
    <VueGPicker
      :clientId="'1027461693281-5d7gmo87k26vm8h9jv28b5q1jl7d6au4.apps.googleusercontent.com'"
      :developerKey="'AIzaSyAcNwETZM1qWE4S_x0l-TgiV4EI-XXsTTo'"
      :scope="['https://www.googleapis.com/auth/drive.readonly']"
      :onChange="data => console.log('on change:', data)"
      :multiselect="true"
      :navHidden="false"
      :authImmediate="false"
      :upload="true"
      :mimeTypes="['image/png', 'image/jpeg', 'image/jpg']"
      :viewId="'DOCS'">
      <button>VueGPicker</button>
    </VueGPicker>
  </div>
</template>

<script>
import VueGPicker from './components/VueGPicker.vue'

export default {
  name: 'app',
  components: {
    VueGPicker
  }
}
</script>

