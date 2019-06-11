<template>
  <div 
    id="quote-box" 
    :class="'container-fluid ' + bgcol"
  >
    <img 
      src="./assets/kanye2-512.png" 
      class="kanye-icon" 
      alt="logo"
    />
    <div class="row-fluid w-100 container-quote-and-buttons">
      <div class="col-12 col-lg-7">
        <div class="quote-box">
          <div id="text" class="quote-paragraph">
            {{kanyeQuoteFormatted}}
          </div>
          <span id="author" class="author-span">Kanye West</span>
        </div>
        <div class="button-row">
          <div class="social-links">
            <a 
              id="tweet-quote" 
              class="btn btn-social" 
              :href="'http://twitter.com/intent/tweet?text=' + kanyeQuoteFormatted + ' – Kanye West'" 
              rel="noopener noreferrer" 
              target="_blank"
            >
              <font-awesome-icon :icon="['fab', 'twitter']"/>
            </a>
          </div>
          <button
            class="btn"
            id="new-quote"
            @click="getQuote"
          >
            {{buttonLabel}}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'app',

  data() {
    return {
      kanyeQuote: '',
      loading: 0
    }
  },

  mounted() {
    this.getQuote();
  },

  computed: {
    bgcol() {
      return this.loading ? 'bgcolor-' + Math.floor(Math.random() * 5) : 'bgcolor-' + Math.floor(Math.random() * 5);
    },
    buttonLabel() {
      return this.loading ? 'Kanye\'s thinking …' : 'Keep \'em coming Kanye!';
    },
    kanyeQuoteFormatted() {
      return '"'+this.kanyeQuote+'"';
    }
  },

  methods: {
    getQuote() {
      let promise = fetch(`https://api.kanye.rest`);
      this.loading = 1;
      promise.then(res => res.json().then(result => {
        this.kanyeQuote = result.quote != '' ? result.quote : 'erm… nothing here.';
        this.loading = 0;
      }).catch(error => alert(error)))
    }
  }
}
</script>


