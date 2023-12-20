<template>
  <div>
    <!-- Display Posts (commented out for simplicity) -->
    <!-- <div v-for="post in posts" :key="post.id" style="border: 1px dashed; margin-bottom: 5px;">
      {{ post.title }}
    </div> -->
    
    {{ helloWorld.value }}
    <br />
    Date: {{ date }}
    <br />
    Day: {{ getDay() }}
    <br />
    Month: {{ getMonth() }}
    <br />
    <input type="text" v-model="input" @input="handleChange" />
    <button @click="changeTheWorld">Change The World</button>
  </div>
</template>

<script>
import useHelloWorld from '@/components/useHelloWorld'; // Adjust the path accordingly

export default {
  setup() {
    const helloWorld = useHelloWorld();

    const data = {
      posts: [],
      input: '',
      date: new Date(),
    };

    const methods = {
      async fetchData() {
        try {
          const response = await fetch('https://jsonplaceholder.typicode.com/todos?limit=5');
          const data = await response.json();
          console.log(data);
          data.posts = data;
        } catch (error) {
          console.error(error);
        }
      },
      handleChange(event) {
        data.input = event.target.value;
      },
      changeTheWorld() {
        helloWorld.setValue(data.input);
      }
    };

    const computed = {
      getDay() {
        return data.date.getDate();
      },
      getMonth() {
        return data.date.getMonth();
      },
    };

    const mounted = () => {
      methods.fetchData();
    };

    return {
      helloWorld,
      ...data,
      ...methods,
      ...computed,
      mounted,
    };
  },
};
</script>

<style>
#app {
  text-align: center;
  box-sizing: border-box;
  background-color: rgba(22, 27, 27, 0.596);
  border-radius: 0.5rem;
  height: 300px;
  padding: 15px;
}
body {
  background-color: #ffff;
  font-size: 30px;
  font-family:Arial, Helvetica, sans-serif;
  padding: 10px;
}
button {
  font-size: 19px;
  margin-top: 15px;
  margin-left: 5px;
  border-radius: 18px 0 ;
}
</style>
