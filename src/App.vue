<script setup>
import {ref} from 'vue'
import story_data from './resources/story/data.json'

const header = ref('Input Text Example')
const fillText = ref([])
let point = "begining"

const newText = ref("")

const setup = () => {
  for(let story in story_data["begining"]["text"])
  {
    fillText.value.push({
      id: fillText.value.length + 1,
      label: story_data["begining"]["text"][story]
    })
  }
}

setup()


const executeAction = () => {
  
  console.log(point)
  console.log(fillText)
  let content = false
  point = story_data[point][newText.value]
  console.log(point)
  if(!point)
  {
    console.log("Acciónn no reconocida")
  }
  else{
    for(let story in story_data[point]["text"])
    {
      content = true
      fillText.value.push(
        {
          id: fillText.value.length + 1,
          label: story_data[point]["text"][story]
        }
      )
    }
  }
  console.log(fillText)
  newText.value = ""
}
</script>

<template>
 <div class="header">
  <h1>{{ header }}</h1>
  <p
    v-for="(item) in fillText"
    :key=item.id
    class="static-class"
  >
    {{item.label}}
  </p>
  <form
    class="add-item-form"
    @load="setup"
    @submit.prevent="executeAction"  
  >
    <input 
      type="text"
      v-model.trim="newText"
      placeholder="Write an Action"
    />
    <button
      class="btn btn-primary"
    >
      Agregar Texto
    </button>
      
  </form>
 </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
