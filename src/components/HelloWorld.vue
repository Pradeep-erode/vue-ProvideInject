<template>

  <div class="hello">
    <h1>{{ newname }}</h1>
    <firstchild childname="friek" secondChild='Manol' />
    <firstchild childname="Geoge" secondChild='hive' />
    <firstchild childname="Geoge" secondChild='hive' />
    <firstchild :childname='childname' secondChild='hive' />
    <!-- <h1>{{ msg }}</h1> -->
    <div>
      <label for="">Normal data return type and Computed -setter and getter</label>
      <h1>{{ fullname }}</h1>
      <h1>{{ firstname }}</h1>
      <h1>{{ lastname }}</h1>
      <h1>{{ getsetname }}</h1>
      <label for="">Get name worked on computed setter property</label>
      <button @click="getsetfullname">GetName</button>
    </div>
    <div>
      <label for="">Normal computed property</label>
      <h1 @click="methodname">{{ methodimplement }}</h1>
      <h1 @click="methodnameOr">{{ methodimplement2 }}</h1>
    </div>
    <div>
      <label for="">push items through push on click method</label>
      <button @click="items.push({
        itemnum: 3,
        title: 'radio',
        price: 3000
      })">Add Item</button>
      <h1>{{ items.reduce((tot, pri) => (tot = tot + pri.price), 0) }}</h1>
    </div>

    <label for="">if condition in h1 tag for amount graeter than 2000 product</label>
    <div v-for="elem in items" :key="elem.itemnum">
      <div>
        <h1 v-if="elem.price > 2000"> {{ elem.title }} {{ elem.price }}</h1>
      </div>

    </div>
    <label for="">Get rs-1000 rs product in computed method - filter</label>
    <div v-for="exp in expensiveitems" :key="exp.itemnum">
      <h1> {{ exp.title }} {{ exp.price }}</h1>
    </div>

    <div>
      <label for="">Normal watch</label>
      <h1> total Volume (0-10) {{ volume }}</h1>
      <button @click="volume += 2">Increase</button>
      <button @click="volume -= 2">Decrease</button>
    </div>
    <div>
      <label for="">Immediate watch - to make hit of watcher on page load</label>
      <input type="text" v-model="myaddresss" />
      <div>
        <label for="">Deep watch for object with numof property</label>
        <input type="text" v-model="movieinfo.moviename" />
        <input type="text" v-model="movieinfo.moviehero" />
      </div>
      <label for="">Deep watch for Array</label>
      <!-- <button type="text" @click="movielist = movielist.concat('Rocketry')">Add movie</button> -->
      <button type="text" @click="movielist.push('yanai')">Add movie</button>
    </div>

    <label for="">props and custom Component event</label>

    <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
    </p>
  </div>
</template>

<script>
import firstchild from './Child1.vue'

import { provide } from 'vue'

export default {
  name: 'HelloWorld',
  setup() {
    provide('Comp_Name', {
      firstname: '',
      lastname: ''
    })
  },
  // we can pass directly to child through below and we cannot access deepname outside this
  //and if we want to use in the child component only we can Use 'provide' as object 
  //   provide:{
  // deepname:'Cat'
  //   },
  //for passing to child as a dynamic access deepname outside this we can use - below,
  //and if we to use it in child component and parent component also we use 'provide' as a function
  provide() {
    return {
      deepname: this.newname
    }

  },
  props: {
    msg: String,
    childresn: String
  },
  data() {
    return {
      newname: 'hi I am provide and Inject',
      childname: 'Dynamic',
      methodimplement: 'click me as a object',
      methodimplement2: 'click me as function',
      firstname: this.msg + ' return data type ',
      lastname: '',
      volume: 0,
      myaddresss: '',
      movieinfo: {
        moviename: '',
        moviehero: ''
      },
      movielist: ['villain', 'maari'],
      items: [
        {
          itemnum: 1,
          title: 'tv',
          price: 1000
        },
        {
          itemnum: 2,
          title: 'Fride',
          price: 8000
        }

      ]
    }
  },
  components: {
    firstchild
  },
  methods: {
    methodname() {
      this.methodimplement = 'I am function Method property'
    },
    // or 
    methodnameOr: function () {
      this.methodimplement2 = 'I am object Method property'
    },
    getsetfullname() {
      this.getsetname = 'IamfirstnameBYComputedsetter IamlastnameBYComputedsetter'
    }
  },
  computed: {
    getsetname: {
      get() {
        return this.msg + ' computed property Getter'
      },
      set(val) {

        const value = val.split(' ')
        this.firstname = value[0]
        this.lastname = value[1]
      }
    },

    fullname: function () {
      return this.msg + ' computed property'
    },
    expensiveitems() {
      return this.items.filter(items => items.price >= 1000)
    }
  },
  watch: {
    volume(newValue, oldValue) {
      if (newValue > oldValue && newValue === 8) {
        alert('too more value')
      }
    },
    myaddresss: {
      handler(newas) {
        // we can use this watch for search like datatable
        console.log(newas)
      },
      immediate: true
    },
    movieinfo: {
      handler(newinfo) {
        console.log('the movie info is =' + newinfo.moviename + ' ' + newinfo.moviehero)
      },
      deep: true
    },
    movielist: {
      handler(newinfo) {
        console.log('Updated movie title is =' + newinfo)
      },
      deep: true
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
</style>
