<template>
  <b-container class="bg-white">
    <div class="border-bottom  border_success display-4 pl-4">
      Респонденты
    </div>
    <div class="text-secondary monospace">
      <strong>
        Добавить опрос
      </strong>
    </div>
    <b-form>
      <div v-for="(poll, pollIndex) in polls" :key="pollIndex" >
        <div class="border m-1 p-2">
          <b-form-group>
            <b-form-select v-model="poll.condition" :options="options"></b-form-select>
          </b-form-group>

          <div v-if="poll.condition === 'age'">
            <div v-for="(age, ageIndex) in poll.ages" :key="ageIndex">
              <b-row class="w-100">
                <b-col>Даипазон</b-col>
                <b-col cols="1">
                  от:
                </b-col>
                <b-col>
                  <b-form-input v-model="age.first" class="inline-block"></b-form-input>
                </b-col>
                <b-col cols="1">до:</b-col>
                <b-col>
                  <b-form-input v-model="age.second" class="inline-block"></b-form-input>
                </b-col>
                <b-col cols="1" class="text-danger cursor-pointer text-center" @click="delAge(pollIndex, age.id)">Удалить</b-col>
              </b-row>
            </div>
            <b-button @click="addAge(pollIndex)">Добавить</b-button>
          </div>

          <div v-if="poll.condition === 'status'">
            <div v-for="(status, index) in poll.status" :key="index" class="p-2">
              <b-row>
                <b-col>
                  <b-form-select v-model="status.curent" :options="statusOptions"></b-form-select>
                </b-col>
                <b-col cols="1">
                  <span cols="1" class="text-danger cursor-pointer text-center" @click="delStatus(pollIndex, status.id)">Удалить</span>
                </b-col>
              </b-row>
            </div>
            <b-button @click="addStatus(pollIndex)">Добавить</b-button>
          </div>

          <div v-if="poll.condition === 'types'">
            <div v-for="(type, key) in poll.types" :key="key" class="p-2">
              <b-row>
                <b-col>
                  <b-form-select v-model="type.curent" :options="typesOptions"></b-form-select>
                </b-col>
                <b-col cols="1">
                  <span cols="1" class="text-danger cursor-pointer text-center" @click="delType(pollIndex, type.id)">Удалить</span>
                </b-col>
              </b-row>
            </div>
            <b-button @click="addType(pollIndex)">Добавить</b-button>
          </div>

          <div v-if="polls.length >= 2" class="text-right">
            <b-button variant="danger" @click="del(poll.id)">Удалить</b-button>
          </div>
        </div>
      </div>
      <div class="text-center border border-success
      p-3 border rounded text-success cursor-pointer" @click="addPoll">
        <h3>+</h3>
        <div>Добаыить новое условие</div>
      </div>
      <b-form-group class="text-right m-2">
        <b-button @click="add">Добавить</b-button>
      </b-form-group>
    </b-form>
  </b-container>
</template>

<script>
  export default {
    data(){
      return{
        polls:[
          {
            id: new Date().getTime(),
            condition: null,
            ages: [
              {
                id: new Date().getTime(),
                first: 0,
                second: 0
              }
            ],
            types: [
              {
                id: new Date().getTime(),
                curent: null
              }
            ],
            status: [{
              id: new Date().getTime(),
              curent: null
              }]
          }
        ],
        options: [
          {value: null, text: "Выберите условие"},
          {value: 'types', text: "Тип карты лояльности"},
          {value: 'status', text: "Статус карты лояльности"},
          {value: 'age', text: "Возраст респондента"},
        ],
        typesOptions: [
          {value: null, text: 'Виберите тип карты'},
          {value: 'gold', text: 'Gold'},
          {value: 'silver', text: 'Silver'},
        ],
        statusOptions: [
          {value: null, text: 'Статус карты'},
          {value: 'active', text: 'Активна'},
          {value: 'deactive', text: 'Пасивна :)'},
        ]
    }
  },
  methods: {
    add() {
      console.log(this.polls);
    },
    addPoll() {
      this.polls.push({
            id: new Date().getTime(),
            condition: null,
             ages: [
              {
                id: new Date().getTime(),
                first: 0,
                second: 0
              }
            ],
            types: [{
              id: new Date().getTime(),
              curent: null
            }],
            status: [{
              id: new Date().getTime(),
              curent: null
            }]
      })
    },
    del(id) {
      this.polls = this.polls.filter(poll => poll.id !== id)
    },
    delAge(index, id) {
      this.polls[index].ages = this.polls[index].ages.filter(age => age.id !== id)
    },
    delStatus(index, id) {
      this.polls[index].status = this.polls[index].status.filter(status => status.id !== id)
    },
    delType(index, id) {
      this.polls[index].types = this.polls[index].types.filter(type => type.id !== id)
    },
    addStatus(index) {
      this.polls[index].status.push({
        id: new Date().getTime(),
        curent: null
        })
    },
    addAge(index) {
      this.polls[index].ages.push({
        id: new Date().getTime(),
          first: 0,
          second: 0
        })
    },
    addType(index) {
      this.polls[index].types.push({
        id: new Date().getTime(),
        curent: null
        })
    }
  }
}
</script>

<style lang="scss" scoped>

</style>