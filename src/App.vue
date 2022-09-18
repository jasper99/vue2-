<template>
  <div class="layout">
     <div>
        <input type="checkbox" name="" id="selectAll" v-model="checkboxSelectAll">
        <label for="selectAll">SelectAll</label>
     </div>
    
     <div v-for="(item, key) in checkboxList" :key="key">
        <input type="checkbox" :id="`checkbox-${key}`" v-model="checkboxList[key]" >
        <label :for="`checkbox-${key}`">checkbox-{{key}}</label>
     </div>
     <div>{{checkboxSelectAll}}- {{checkboxList}}</div>
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
             return this.checkboxList.length && this.checkboxList.filter(Boolean).length === this.checkboxList.length;
          },
          set(value) {              
             
            this.checkboxList = value? Array(3).fill(true) : Array(3).fill(false);  
          }           
        }    
      },
     

  }
</script>

<style lang="scss" scoped>
  .layout{
     margin: 50px;
  }
  div{
    margin-bottom: 20px;
  }
 
  
  label{
    padding: 8px 12px;
    background-color: #1abc9c;
    border-radius: 5px;
    color: #FFF;
    opacity: .7;
    cursor: pointer;
    margin-bottom: 15px;
    
  }
  [type="checkbox"]{
    display: none;
    &:checked+label{
      opacity: 1;
    }
    &#selectAll + label{
      background-color: #f1c40f;
    }
  }
</style>