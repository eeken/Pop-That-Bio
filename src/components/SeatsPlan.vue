<template>
  <div class="container-fluid">
    <div class="title-text">
      <h4 class>Platser</h4>
    </div>
    <hr class="hr-style" />
    <div class="seats-info">
      <div class="gray-circle"></div>
      <div>
        <span>Ledig</span>
      </div>
      <div class="purple-circle"></div>
      <div>
        <span>Upptagen</span>
      </div>
    </div>

    <div class="grid">
      <div class="row seats-grid" v-for="(blockRow, row) in seatsGrid" :key="row">
        <div class="all-blocks" v-for="(block, col) in blockRow" :key="col">
          <div class="seats" v-if="block==='S'" @click="getPosition(col, row)"></div>
        </div>
      </div>
    </div>

    <div class="row seat-position" v-if="seatPosition != 0">
      <h6>Parkett, rad {{seatPosition[0].x}}, plats {{seatPosition[0].y}}</h6>
    </div>

    <div class="buttons">
      <router-link :to="'/movies/' + movieDetail.slug + '/ticket'">
        <button class="btn btn-small waves-effect waves-light">Tillbaka</button>
      </router-link>
      <router-link to="/">
        <button class="btn btn-small waves-effect waves-light" @click="completeBooking">Fortsätt</button>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  // props: ['numberOfChildren', 'numberOfAdults', 'numberOfSeniors'],
  data() {
    return {
      seatsPerRow: [8, 9, 10, 10, 10, 10, 12, 12],
      movies: this.$store.getters.movies,
      movieDetail: [],
      seatPosition: [],
      seatBooked: false,
      seatsGrid: []
    };
  },
  methods: {
    getPosition(x, y) {
      let position = {x:y+1, y:x+1}
      this.seatPosition.push(position)
    },
    createSeatsGrid() {
      for (let i = 0; i < this.seatsPerRow.length; i++) {
        let rows = new Array(this.seatsPerRow[i]);
        this.seatsGrid.push(rows.fill("S"));
      }
      return this.seatsGrid;
    },
    getMovie() {
      this.movies.forEach(movie => {
        if (movie.slug == this.$route.params.slug) {
          this.movieDetail = movie;
        }
      });
    },
    completeBooking() {
      let bookingNumber =
        Math.floor(Math.random() * 1000) +
        "-" +
        Math.floor(Math.random() * 100000);
      let tickets = this.$store.getters.tickets;
      let booking = {
        collection: "bookings",
        bookingNumber: bookingNumber,
        numberOfAdults: tickets.numberOfAdults,
        numberOfChildren: tickets.numberOfChildren,
        numberOfSeniors: tickets.numberOfSeniors
      };
      this.$store.dispatch("sendToFirebase", booking);
      alert("Bokningsnummer: " + bookingNumber);
    }
  },
  created() {
    this.getMovie();
    this.createSeatsGrid();
  }
};
</script>


<style lang="css" scoped>
.container-fluid {
  padding-bottom: 3%;
}
.title-text {
  text-align: center;
  color: rgb(204, 9, 113);
}

/* SEATS INOF */
.seats-info {
  display: flex;
  justify-content: center;
  margin: 1.9% auto;
}
.gray-circle,
.purple-circle,
.blue-circle {
  margin: 0 0.5% 0 0.5%;
  width: 20px;
  height: 20px;
  background: #ddd;
  border: 1px solid #8e8e8e;
  border-radius: 50%;
}
.gray-circle {
  background: #ddd;
}
.purple-circle {
  background: rgb(204, 9, 113);
}
.blue-circle {
  background: rgba(111, 111, 241, 0.699);
}
/* STYLE TO GRID */

.seats-grid {
  display: flex;
  justify-content: center;
}
.all-blocks {
  position: relative;
  border-bottom-right-radius: 15px;
  border-bottom-left-radius: 15px;
}
.seats{
  justify-content: center;
  width: 23px;
  height: 20px;
  margin: 0 3px;
  border: 1px solid #8e8e8e;
  background: #ddd;
  border-bottom-right-radius: 15px;
  border-bottom-left-radius: 15px;
}

.seats:hover {
  cursor: pointer;
  background: rgb(204, 9, 113);
}

.seat-position {
  text-align: center;
}

.buttons {
  display: flex;
  justify-content: center;
  margin: 0 1% 3% 1%;
}

.btn {
  background: rgba(202, 8, 112, 0.692);
  margin-left: 10px;
  margin-right: 10px;
}

.hr-style {
  border: 0;
  min-width: 90%;
  max-width: 1%;
  height: 1px;
  margin: 0 auto 10px auto;
  background: #fff;
  background: -webkit-linear-gradient(left, #fff, rgb(204, 9, 113), #fff);
}
</style>