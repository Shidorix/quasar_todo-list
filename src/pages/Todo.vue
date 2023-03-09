<template>
  <q-page class="bg-grey-3 column">
    
    <q-list
    separator bordered>
      

      <q-item 
      @click="task.done = !task.done"
      clickable
      :class="{ 'done bg-green-2': task.done }"
      v-for="(task, index) in tasks" 
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
        <!-- Событие клик не будет всплывать дальше -->
        <q-btn
        @click.stop='deleteTask(index)' 
         unelevated round color="secondary" icon="delete" />
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
  },
  methods: {
    deleteTask(index) {
      this.$q
      .dialog({
        title: 'Подтвердить',
        message: 'Действительно ли ты хочешь удалить задачу?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1);
        this.$q
        .notify({
          message: 'Задача удалена',
          color: 'green'
        })
      });


      
    },

  }
}

</script>

<style lang="sass">
.done
  .q-item__label
    text-decoration: line-through
    color: grey
</style>