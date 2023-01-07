<script >
import { store } from '../store.js';
export default {
  data() {
    return {
      active: {},
      store,
    }
  },
  methods: {
    // metodo per visualizzare bandiere in base alla lingua
    displayLanguage(language) {
      if (language === 'en') {
        return '<img class="flag" src="https://flagcdn.com/16x12/gb.png" alt="uk-flag" />';
      }
      else if (language === 'it') {
        return '<img class="flag" src="https://flagcdn.com/16x12/it.png" alt="it-flag" />';
      }
      else {
        return language;
      }
    },
    rating(voteAverage) {
      let vote = Math.round(voteAverage / 2);
      return vote;
    }
  }
}
</script>

