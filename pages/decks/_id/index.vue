<template>
  <section>
    <div class="r">
      <div class="ct text_center">
        <h3>Deck: {{ deck.name }}</h3>
        <div class="tools">
          <button class="btn btn_success">Start now</button>
          <button class="btn btn_primary" @click.prevent="openModal('CreateCardModal')">Create a card</button>
          <button class="btn btn_warning" @click.prevent="openModal('DeckFormModal')">Edit Deck</button>
        </div>
        <hr class="divide">
        <div class="r">
          <card-list v-for="card in cards" :key="card._id" :keyword="card.keyword" :picture="card.picture"/>
        </div>
      </div>
    </div>
    <v-modal name="CreateCardModal">
      <div class="modal_body">
        <h2>Create a new Card </h2>
        <form action="">
          <div class="form_group">
            <label for="">Name:</label>
            <input class="form_control" type="text" placeholder="Please enter name deck">
          </div>
          <div class="form_group">
            <label for="">Description:</label>
            <textarea class="form_control" placeholder="Please enter description deck"/>
          </div>
          <div class="form_group">
            <label for="">Thumbnail:</label>
            <input type="file">
          </div>
          <div class="form_group d_flex justify_content_end">
            <button class="btn btn_danger" @click.prevent="closeModal">Close</button>
            <button class="btn btn_success ml_3" @click.prevent="createDeck">Create</button>
          </div>
        </form>
      </div>
    </v-modal>
  </section>
</template>
<script>
import CardList from "@/components/Cards/CardList";

export default {
  components: {CardList},
  asyncData(context) {
    return context.app.$axios.$get(
      process.env.baseApiUrl + `/decks/${context.params.id}.json`
    )
      .then((data) => {
        return {
          deck: data
        }
      })
      .catch((e) => {
        context.error(e)
      })
  },
  data() {
    return {
      cards: [
        {
          _id: 1,
          picture: 'https://thietkenoithatatz.com/wp-content/uploads/2022/10/8-don-vi-chuyen-thiet-ke-thi-cong-shop-thoi-trang-ha-noi-1.jpg',
          keyword: 'Road'
        },
        {
          _id: 2,
          picture: 'https://thietkenoithatatz.com/wp-content/uploads/2022/10/8-don-vi-chuyen-thiet-ke-thi-cong-shop-thoi-trang-ha-noi-1.jpg',
          keyword: 'Road'
        },
        {
          _id: 3,
          picture: 'https://thietkenoithatatz.com/wp-content/uploads/2022/10/8-don-vi-chuyen-thiet-ke-thi-cong-shop-thoi-trang-ha-noi-1.jpg',
          keyword: 'Road'
        },
        {
          _id: 4,
          picture: 'https://thietkenoithatatz.com/wp-content/uploads/2022/10/8-don-vi-chuyen-thiet-ke-thi-cong-shop-thoi-trang-ha-noi-1.jpg',
          keyword: 'Road'
        },
        {
          _id: 5,
          picture: 'https://thietkenoithatatz.com/wp-content/uploads/2022/10/8-don-vi-chuyen-thiet-ke-thi-cong-shop-thoi-trang-ha-noi-1.jpg',
          keyword: 'Road'
        },
        {
          _id: 6,
          picture: 'https://thietkenoithatatz.com/wp-content/uploads/2022/10/8-don-vi-chuyen-thiet-ke-thi-cong-shop-thoi-trang-ha-noi-1.jpg',
          keyword: 'Road'
        }
      ]
    }
  },
  methods: {
    closeModal() {
      this.$modal.close({name: 'CreateCardModal'})
    },
    openModal(name) {
      if (name === 'CreateCardModal') {
        this.$modal.open({name: 'CreateCardModal'})
      } else if (name === 'DeckFormModal') {
        this.$modal.open({name: 'DeckFormModal', payload: {...this.deck, id: this.$route.params.id}})
      }
    }
  }
}
</script>

<style lang="scss">
section {
  padding-top: 3rem;

  .card {
    padding: 1rem;

    img {
      width: 60%;
    }
  }

  .divide {
    margin: 2rem 0;
  }
}

.modal_body {
  background-color: white;
  padding: 1rem;
}
</style>
