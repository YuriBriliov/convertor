<template>
   <form @submit.prevent>
      <h4>
        Конвертор валют
      </h4>
      <input 
       v-model="post.val1"
       class="input_valute"
       type="number"
       placeholder="сумма"
      />
      <div class="currancy_values">
        <div class="currancy_item">
          Конвертировать из:
          <select v-model="targetCurr.curr1" class="section_input">
            <option v-for="item of currency" :key="item.key">{{item.key}}</option>
          </select>
        </div>
        <!-- <input 
        v-model="post.val2"
        class="input_valute"
        type="number"
        placeholder="сумма"
        /> -->
        <div class="currancy_item">
          Конвертировать в:
          <select v-model="targetCurr.curr2" class="section_input">
            <option v-for="item of currency" :key="item.key">{{item.key}}</option>
          </select>
        </div>
      </div>
      <button class="btn" @click="createPost">конвертировать</button>
    </form>
</template>

<script>
export default {
  data(){
    return {
      currency: [],
      targetCurr:{
        curr1: '',
        curr2: '',
        currValue1: null,
        currValue2: null
      },
      post: {
        val1: ''
      }
    }
  },
  methods: {
    createPost(){
      this.currency.forEach((item)=>{
        if(item.key === this.targetCurr.curr1){
          this.targetCurr.currValue1 = item.value
        }else if(item.key === this.targetCurr.curr2){
          this.targetCurr.currValue2 = item.value
        }
      })
      this.post.id = Date.now()
      this.post.curr1 = this.targetCurr.curr1
      this.post.curr2 = this.targetCurr.curr2
      this.post.result = 
      (`Результат: ${Math.round(parseFloat(this.targetCurr.currValue2 / this.targetCurr.currValue1 * this.post.val1) * 100) / 100}`)
      this.$emit('create', this.post)
      this.post = {
        val1: ''
      }
    },
    async getCurrency(){
      try {
        const response = await fetch('http://api.exchangeratesapi.io/v1/latest?access_key=8022019c26ddde5fe6f23a3817bf7a8a')
        const semiValue = await response.json()
        for (const key in semiValue.rates) {
          this.currency.push({key, value: semiValue.rates[key]})
        }
      } catch (error) {
        console.log(error)
      }
    }
  },
  created() {
    this.getCurrency()
  }
}
</script>

<style scoped>
  form{
    display: flex;
    flex-direction: column;
  }
  .btn {
    align-self: flex-end;
    margin-top: 15px;
    padding: 7px 12px;
    background: none;
    color: teal;
    border: 1px solid teal;
  }
  .input_valute {
    width: 100%;
    border: 1px solid teal;
    padding: 10px;
    margin-top: 15px;
  }
  .section_input {
    width: 50%;
    border: 1px solid teal;
    padding: 5px;
    margin-top: 5px;
  }

  .currancy_item {
    max-width: 400px;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
</style>
