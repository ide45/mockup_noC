<template>
  <h1>HOLA</h1>

  <div class="box">
    <p v-for="item in list" :key="item" class="fish">
      <img :src="item[str].src" v-bind:alt="item[str].alt"> <br>
      {{item["Species Name"]}} <br>
      {{remove(item?.Location)}} <br> <br>
    </p>
  </div>
  <button>PRESIONA</button>
</template>

<script>
import axios from "axios"
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      list: [],
      str: "Species Illustration Photo",
    }
  },
  created() {
    this.fetch()
  },
  methods: {
    fetch() {
      axios.get(`https://www.fishwatch.gov/api/species`).then(response => {
        console.log("Success")
        //console.log(response.data[0])

        this.list = response.data
      }).catch(()=> {
        console.log("Error")
      });
    },
    remove(locate) {
      return locate?.replace(/<ul>|<li>/g, "").replace("</li>", "").replace("</ul>", "").replace(".</li>", "");
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.box {
  margin-inline: 1em;
  display: flex;
  flex-direction: column;
  flex-flow: wrap;
  justify-content: center;
  gap: 3em;
}

.fish {
  border: #42b983 solid 3px;
  background-color: bisque;
  box-shadow: 0 10px 15px rgba(0, 0, 0, 0.095);
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
img {
  width: 50%;
}
</style>
