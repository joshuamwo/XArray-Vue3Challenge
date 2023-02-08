<template>
  <div class="flex-container">
    <input
      v-for="index in myArray.length + 1"
      :key="index - 1"
      :value="myArray[index - 1]"
      @input="onInput($event.target.value, index - 1)"
      placeholder="+ element to array"
    />

    <pre>{{ myArray }}</pre>
  </div>
</template>

<style>
/* style the inputs container */
.flex-container {
  display: flex;
  flex-direction: column;
}
</style>

<script>
export default {
  //fetching props and emits
  props: ['myArray'],
  emits: ['update:myArray'],
  methods: {
    onInput(value, index) {
      try {
        //create a shallow copy of myArray
        let myArrayCopy = [...this.myArray];
        myArrayCopy[index] = value;
        //emit filtered myArrayCopy to remove empty elements from array
        this.$emit(
          'update:myArray',
          myArrayCopy.filter((e) => e != '')
        );
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
