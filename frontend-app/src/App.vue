<template>
   <div class="text-search">
    <h1>
      Search 
    </h1>

    <div class="search-bar">
      <input type="text" v-model="searchText" placeholder="Search for article">
      <button @click="search()">Search</button>
    </div>

    <div class="results">
      <span>{{ searchResults.length }} was found</span>
      <div v-for="(result, index) in searchResults" :key="index">
        <h2 v-html="result.title"></h2>
        <p v-html="result.content"></p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      articles: [
        {
          title: "How to build an SAP in Vue 3 using npm?",
          content: "This is a sample article about building an SAP in Vue 3 using npm",
        },
        {
          title: "Why Tailwind is better than Bootstrap?",
          content: "Tailwind is better than Bootstrap because it is more customizable and has more features",
        },
        {
          title: "Are you more of backend or frontend developer?",
          content: "Frontend developer is responsible for building the UI and UX of a website but backend is responsible for the logic of the website"
        }
      ],
      searchText: "",
      searchResults: [],
      searchResultsLength: 0
    }
  },

  methods: {
    search() {
      this.searchResults = [];
      this.articles.forEach((element) => {
        if(element.title.toLowerCase().includes(this.searchText.toLowerCase())) {
          const markedTitle = element.title.replace(new RegExp(this.searchText, 'gi'), (match) => `<mark>${match}</mark>`);
          this.searchResults.push({
            title: markedTitle,
            content: element.content
          })
        } else if (element.content.toLowerCase().includes(this.searchText.toLowerCase())) {
          const markedContent = element.content.replace(new RegExp(this.searchText, 'gi'), (match) => `<mark>${match}</mark>`);
          this.searchResults.push({
            title: element.title,
            content: markedContent
          })
        }
      });
      console.log(this.searchResults)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 20px;
  padding: 10px;
}

.search-bar {
  display: flex;
  flex-direction: row;
}

.search-bar input{
  width: 500px;
  padding: 9px;
  font-size: large;
  margin: 5px;
}
</style>
