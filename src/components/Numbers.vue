<!--
All variables, class names and function names are almost identical. I have renamed them to be more descriptive allowing 
for easier reading of the code.
-->
<template>
  <div class="mainContainer">
    <div class="Numbercontainer">
      <div class="number" :id="'number-'+number" v-for="number in n()" :key="number" @mouseover="hover(number)" @mouseout="reset">
        {{number}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data()
  {
    return {
      limit: this.$parent.limit,
      allallNumbers: []
    }
  },
  watch: {
    ['$parent.limit'](newLimit)
    {
      this.limit = newLimit;
    }
  },
  methods: {
    n()
    {
      let allNumbers = [];
      //Changed range to be from 1 not 0 as per README instructions. Also changed var to let to match with the rest of the code.
        for (let i = 1; i < this.limit; i++) {
          allNumbers = [...allNumbers, i];
          }
          return allNumbers.sort(() => Math.random() - 0.5)
    },
    hover(number)
    {
      const numberSelect = document.querySelectorAll('.number');

      for(let i = 0; i < numberSelect.length; i++)
      {
        const num = numberSelect[i].textContent.trim();
        if(number % num === 0)
        {
          numberSelect[i].classList.add('active')
          //Removed the console.log. Final code shouldnt contain console.logs
        }
      }
    },
    reset()
    {
      const numberSelect = document.querySelectorAll('.number');
      numberSelect.forEach(num => num.classList.remove('active'))
    }
  }
}
</script>

<!--
Styling for additional containers to make numbers easier to read. Also changed background and highlight colours 
to be less...violent on the eyes.
-->
<style scoped>
  .mainContainer{
  margin: 2em 0 0 0;
  display: flex;
  align-items: center;
  }
  .Numbercontainer {
    display: flex-wrap-column;
    justify-content: center;
    width: 50%;
  }
	.number {
		display: inline-block;
		padding: 10px;
		background-color: rgb(244, 244, 244);
		margin: 8px;
	}
	.active {
		background-color: rgba(149, 254, 154, 0.811);
	}
</style>
