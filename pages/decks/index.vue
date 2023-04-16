<template>
  <div>
    <div class="ct">
      <div class="d_flex justify_content_between my_3">
        <h3> List of your decks:</h3>
        <button class="btn btn_success" @click.prevent="openModal">Create a deck</button>
      </div>
      <ul class="decks-list">
        <DeckList
          v-for="deck in decks"
          :id="deck.id"
          :key="deck.id"
          :name="deck.name"
          :description="deck.description"
          :thumbnail="deck.thumbnail"/>
      </ul>
    </div>
    <v-modal name="CreateDeckModal">
      <div class="modal_body">
        <h2>Create a new Deck </h2>
        <DeckForm @submit="onSubmit"/>
      </div>
    </v-modal>
  </div>
</template>

<script>
import axios from 'axios'

import DeckList from "@/components/Decks/DeckList";
import DeckForm from "~/components/Decks/DeckForm";

export default {
  components: {DeckForm, DeckList},
  computed: {
    decks() {
      return this.$store.getters.decks;
    }
  },
  methods: {
    openModal() {
      this.$modal.open({name: 'CreateDeckModal'})
    },
    onSubmit(deckData) {
      axios.post('https://nuxt-learning-english-69f0f-default-rtdb.asia-southeast1.firebasedatabase.app/decks.json', deckData)
        .then((data) => {
          // eslint-disable-next-line no-console
          console.log(data)
        })
        .catch((e) => {
          // eslint-disable-next-line no-console
          console.log(e)
        })
    }
  }
}
</script>

<style lang="scss">
.decks-list {
  .deck {
    display: block;
  }

  li {
    margin-bottom: 1rem;

    &:last-child {
      margin-bottom: 0;
    }
  }

  .deck-card {
    display: flex;
    flex-direction: row;
    height: 250px;

    img {
      width: 250px;
      height: auto;
    }
  }
}

.modal_body {
  background-color: white;
  padding: 1rem;
}
</style>
