<template>
  <main>
    <h1>Szakkörök</h1>
    <div class="split">
      <div class="left">
        <table class="table col-6">
          <thead>
            <tr>
              <th scope="col">Diák</th>
              <th scope="col">Osztály</th>
              <th scope="col">Szakkör</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="tanulo in tanulok" :key="tanulo.id">
              <td>{{ tanulo.nev }}</td>
              <td>{{ tanulo.osztaly }}</td>
              <td>
                <select v-model="tanulo.kivalasztottSzakkor" @change="addTanuloToSzakkor(tanulo)">
                  <option v-for="szakkor in szakkorok" :key="szakkor.id" :value="szakkor.nev">
                    {{ szakkor.nev }}
                  </option>
                </select>
              </td>
            </tr>
          </tbody>
        </table>
      </div>

      <div class="right">
        <div class="card" v-for="(tanulok, szakkor) in szakkorFeladatok" :key="szakkor">
          <div class="card-body">
            <h5 class="card-title">{{ szakkor }}</h5>
            <p v-if="tanulok.length">
              Tanulók: {{ tanulok.join(', ') }}
            </p>
            <p v-else>Nincs tanuló ebben a szakkörben</p>
          </div>
        </div>
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">Még nincs szakköre</h5>
            <p v-if="nemSzakkor.length">
              Tanulók: {{ nemSzakkor.join(', ') }}
            </p>
            <p v-else>Minden tanulónak van szakköre.</p>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      tanulok: [
        { id: 1, nev: "Lars Johansen", osztaly: "13b", Szakkor: "" },
        { id: 2, nev: "Ingrid Haugland", osztaly: "9c", Szakkor: "" },
        { id: 3, nev: "Ole Nilsen", osztaly: "13d", Szakkor: "" },
        { id: 4, nev: "TSigrid Bjørnsen", osztaly: "10d", Szakkor: "" },
        { id: 5, nev: "Erik Andersen", osztaly: "11h", Szakkor: "" },
        { id: 6, nev: "Solveig Haugen", osztaly: "11h", Szakkor: "" },
        { id: 7, nev: "Magnus Lund", osztaly: "9f", Szakkor: "" },
        { id: 8, nev: "Hakon Kristoffersen", osztaly: "12d", Szakkor: "" },
        { id: 9, nev: "Kari Pedersen", osztaly: "10c", Szakkor: "" },
        { id: 10, nev: "Bjørn Halvorsen", osztaly: "12g", Szakkor: "" },
      ],
      szakkorok: [
        { id: 1, nev: "Football" },
        { id: 2, nev: "Dráma" },
        { id: 3, nev: "Cigánykodás" },
        { id: 3, nev: "Kertészet" }
      ],
      szakkorFeladatok: {
        Football: [],
        Dráma: [],
        Cigánykodás: [],
        Kertészet: [],
      }
    };
  },
  computed: {
    nemSzakkor() {
      return this.tanulok
        .filter(tanulo => !tanulo.kivalasztottSzakkor)
        .map(tanulo => tanulo.nev);
    }
  },
  methods: {
    addTanuloToSzakkor(tanulo) {
      for (let szakkor in this.szakkorFeladatok) {
        const index = this.szakkorFeladatok[szakkor].indexOf(tanulo.nev);
        if (index !== -1) {
          this.szakkorFeladatok[szakkor].splice(index, 1);
        }
      }

      if (tanulo.kivalasztottSzakkor) {
        this.szakkorFeladatok[tanulo.kivalasztottSzakkor].push(tanulo.nev);
      }
    }
  }
};
</script>

<style scoped>
.table {
  max-width: 600px;
}

h1 {
  text-align: center;
  border: 4px black solid;
  transition: transform 0.3s ease-in-out;
}

h1:hover {
  animation: moveSideToSide 0.5s ease-in-out infinite alternate;
}

@keyframes moveSideToSide {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(20px);
  }
}

.split {
  display: flex;
}

.left {
  flex: 40%;
  margin-right: 20px;
  border-right: 2px solid black; 
  padding-right: 10px; 
  /* RGB világító keret */
  border: 5px solid;
  border-image: linear-gradient(90deg, red, yellow, green, cyan, blue, magenta, red);
  border-image-slice: 1;
  animation: rgb-border 5s infinite;
}

.right {
  flex: 60%;
  border: 5px solid;
  border-image: linear-gradient(90deg, red, yellow, green, cyan, blue, magenta, red);
  border-image-slice: 1;
  animation: rgb-border 5s infinite;
}

@keyframes rgb-border {
  0% {
    border-image: linear-gradient(90deg, red, yellow, green, cyan, blue, magenta, red);
  }
  50% {
    border-image: linear-gradient(90deg, magenta, red, yellow, green, cyan, blue, magenta);
  }
  100% {
    border-image: linear-gradient(90deg, blue, magenta, red, yellow, green, cyan, blue);
  }
}

</style>
