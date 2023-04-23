<template>
  <div>
    <default-header/>
    <nuxt/>
    <v-modal v-slot="payload" name="DeckFormModal">
      <div class="modal_body">
        <h2>{{ payload && payload.payload ? 'Edit a Deck' : 'Create a New Deck'}}</h2>
        <DeckForm :deck="payload.payload" @submit="onSubmit"/>
      </div>
    </v-modal>
    <default-footer/>
  </div>
</template>
<script>

import axios from "axios";


import DeckForm from "@/components/Decks/DeckForm";
import DefaultHeader from "~/components/Header/DefaultHeader";
import DefaultFooter from "@/components/Footer/DefaultFooter";

export default {
  components: {DefaultFooter, DefaultHeader, DeckForm},
  methods: {
    onSubmit(deckData) {
      if (deckData && !deckData.id) {
        axios.post('https://nuxt-learning-english-69f0f-default-rtdb.asia-southeast1.firebasedatabase.app/decks.json', deckData)
          .then((data) => {
            // eslint-disable-next-line no-console
            console.log(data)
          })
          .catch((e) => {
            // eslint-disable-next-line no-console
            console.log(e)
          })
      } else {
        const deckId = deckData.id
        axios.put('https://nuxt-learning-english-69f0f-default-rtdb.asia-southeast1.firebasedatabase.app/decks/' + deckId + '.json',
          deckData)
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
}
</script>
