<template>
  <q-page class="bg-grey-3 column">
    
    <q-list>

      <q-item tag="label" v-ripple
      v-for="task in tasks" :key="task.title">
        <q-item-section avatar>
          <q-checkbox v-model="color" val="teal" color="teal" />
        </q-item-section>
        <q-item-section>
          <q-item-label> {{ task.title }}</q-item-label>
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

