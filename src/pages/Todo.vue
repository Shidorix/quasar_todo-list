<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-accent">
      <q-input class="col" placeholder="Добавьте задачу" filled bg-color="white" v-model="newTask" label="Задача" dense @keyup.enter="addTask">

        <template v-slot:append>
          <q-btn @click="addTask" round dense flat icon="add" />
        </template>

      </q-input>
    </div>
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
    <div v-if="!tasks.length" class="no-task absolute-center column items-center">
      <q-icon
      name="sentiment_dissatisfied"
      size="150px"
      color="accent"
      />
      <div class="text-h4 text-accent text-center"> Сейчас нет никаких задач  </div>
    </div>
  </q-page>
</template>

<script>

export default {
  data() {
    return {
      newTask: '',
      tasks: [
        // {
        //   title: 'hello1',
        //   done: false,
        // },
        // {
        //   title: 'hello2',
        //   done: false,
        // },
        // {
        //   title: 'hello3',
        //   done: false,
        // },
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
    addTask() {
      this.tasks.push({
        title: this.newTask,
        done: false,
      })
      this.newTask = '';
    },
    
  }
}

</script>

<style lang="sass">
.done
  .q-item__label
    text-decoration: line-through
    color: grey

.no-task
  opacity: 0.5    
</style>