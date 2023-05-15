<template>
  <div>
    <default-header/>
    <nuxt/>
    <v-modal v-slot="payload" name="DeckFormModal">
      <div class="modal_body">
        <h2>{{ payload && payload.payload ? 'Edit a Deck' : 'Create a New Deck' }}</h2>
        <DeckForm :deck="payload.payload" @submit="onSubmit"/>
      </div>
    </v-modal>
    <default-footer/>
  </div>
</template>
<script>

import DeckForm from "@/components/Decks/DeckForm";
import DefaultHeader from "~/components/Header/DefaultHeader";
import DefaultFooter from "@/components/Footer/DefaultFooter";

export default {
  components: {DefaultFooter, DefaultHeader, DeckForm},
  methods: {
    onSubmit(deckData) {
      if (deckData && !deckData.id) {
        this.$store.dispatch('addDeck', deckData)
          .then(() => this.$modal.close({name: 'DeckFormModal'}))
      } else {
        this.$store.dispatch('editDeck', deckData)
          .then(() => this.$modal.close({name: 'DeckFormModal'}))
      }
    }
  }
}
</script>
