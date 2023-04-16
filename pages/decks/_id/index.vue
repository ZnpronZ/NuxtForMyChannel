<template>
  <section>
    <div class="r">
      <div class="ct text_center">
        <h3>Deck #{{ $route.params.id }}: {{ deck.name }}</h3>
        <div class="tools">
          <button class="btn btn_success">Start now</button>
          <button class="btn btn_primary" @click.prevent="openModal">Create a card</button>
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
  validate(context) {
    return /^[0-9]$/.test(context.params.id)
  },
  asyncData(context) {
    return new Promise((resolve, reject) => {
      // eslint-disable-next-line nuxt/no-timing-in-fetch-data
      setTimeout(() => {
        resolve({
          deck: {
            _id: 1,
            name: `Learn English by deck ${context.params.id}`,
            description: 'Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry\'s standard dummy text ever since the 1500s,',
            thumbnail: 'https://s3.ap-south-1.amazonaws.com/blogassets.leverageedu.com/media/uploads/2022/11/17105928/importance-of-education.jpg'
          },
        })
      }, 1500)
    }).then((data) => {
      return data
    }).catch((e) => {
      // eslint-disable-next-line no-console
      console.log(e)
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
    openModal() {
      this.$modal.open({name: 'CreateCardModal'})
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
