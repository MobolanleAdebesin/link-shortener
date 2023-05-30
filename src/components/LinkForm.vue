<template>
  <div class="col-start-3">
    <form @submit.prevent="$emit('submit-link', encodeURI(url))">
      <div>
        <label class="text-blue-400 font-bold" for="LinkInput">{{
          labelText
        }}</label>
        <input
          class="mx-2 p-1 border-2 border-gray-200 text-center"
          name="LinkInput"
          type="text"
          :placeholder="placeholderText"
          v-model="url"
        />
      </div>
      <div>
        <input
          class="border-2 border-yellow-300 p-3 my-3 bg-yellow-300 hover:bg-yellow-200 font-bold rounded-md drop-shadow-md cursor-pointer"
          type="submit"
          :value=" buttonText"
        />
      </div>
    </form>
  </div>
</template>

<script>
    export default{
        props: {
            labelText: String, 
            placeholderText: String, 
            buttonText: String, 
        },
        data(){
            return{
                url: ''
            }
        }, 
    }
</script>
