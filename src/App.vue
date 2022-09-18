<template>
  <div class="layout">
     <div>
        <input type="checkbox" name="" id="selectAll" v-model="checkboxSelectAll" @click="checkboxSelectAll = 'selectAll'">
        <label for="selectAll">SelectAll</label>
     </div>
     <div>
     </div>
     <div v-for="(item, key) in checkboxList" :key="key">
        <input type="checkbox" :id="`checkbox-${key}`" v-model="checkboxList[key]" @click="checkboxClick">
        <label :for="`checkbox-${key}`">checkbox-{{key}}</label>
     </div>
  </div>
</template>

<script>
  export default {
      data() {
         return {
            checkboxList:[],
            checkedNum:0           
         }
      },
      mounted(){
         this.checkboxList = Array(3).fill(false);
      },        
      computed:{
         checkboxSelectAll: {
          
          get() {             
             return this.checkedNum > 0 && this.checkboxList.length === this.checkedNum ? true : false;
          },
          set(value) {                  
          
            if(!value || value !== 'selectAll') {              
              return;
            } 
            if(this.checkboxList.every(Boolean)) {
              this.checkboxList.fill(false);
              this.checkedNum = 0;
            } else {
              this.checkedNum = this.checkboxList.length;
              this.checkboxList.fill(true);                
            }             
          }           
        }    
      },
      methods:{       
        checkboxClick(event) {
           if(event.target.checked) {
               this.checkedNum++;         
           } else {
               this.checkedNum--;           
           }

        }
      }
     

  }
</script>

<style lang="scss" scoped>
  .layout{
     margin: 50px;
  }
  div{
    margin-bottom: 10px;
  }
  label, input{
    cursor: pointer;
  }
</style>