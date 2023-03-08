<template>
  <q-page class="bg-grey-3 column">
    
    <q-list
    separator bordered>
      

      <q-item 
      @click="task.done = !task.done"
      clickable
      :class="{ 'done bg-green-2': task.done }"
      v-for="task in tasks" 
      :key="task.title"
      v-ripple>
        <q-item-section avatar>
          <q-checkbox class="no-pointer-events" v-model="task.done" val="teal" color="teal" />
        </q-item-section>
        <q-item-section>
          <q-item-label> {{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section
        v-if="task.done" side>
          <q-icon name="task_alt"></q-icon>
        </q-item-section>
      </q-item>

      
    </q-list>
  </q-page>
</template>

<script>

export default {
  data() {
    return {
      tasks: [
        {
          title: 'hello1',
          done: false,
        },
        {
          title: 'hello2',
          done: false,
        },
        {
          title: 'hello3',
          done: false,
        },
      ]
    }
  }
}

</script>

<style lang="sass">
.done
  .q-item__label
    text-decoration: line-through
    color: grey
</style>