<template>
  <q-page class="flex flex-center" :style="this.changeBgColor">
    <q-icon
      class="fas fa-angle-double-left absolute all-pointer-events"
      size="80px"
      color="black"
      style="top: 50%; left: 15px; cursor: pointer; opacity: 20%; z-index: 1"
      @click="getSelectedPokeInfo(-1)"
      @keypress.arrow-left="getSelectedPokeInfo(-1)"
    />

    <q-icon
      class="fas fa-angle-double-right absolute all-pointer-events"
      size="80px"
      color="black"
      style="top: 50%; right: 15px; cursor: pointer; opacity: 20%; z-index: 1"
      @click="getSelectedPokeInfo(+1)"
      @keydown.arrow-left="getSelectedPokeInfo(+1)"
    />
    <div class="q-pa-md row items-center no-wrap q-gutter-md">
      <q-card
        style="max-width: 80vw; background-color: rgba(255, 0, 0, 0)"
        flat
      >
        <q-img
          style="max-width: 80vw"
          spinner-color="white"
          :src="this.selectedPokeImg"
        />

        <q-card-section>
          <div class="text-h4 text-center">
            <q-chip
              style="opacity: 60%"
              flat
              text-color="black"
              size="lg"
              dense
              >{{ this.selectedPokeIdShow }}</q-chip
            >
            {{ this.selectedPokeName }}
          </div>
          <div class="text-subtitle2 text-center">
            <q-chip
              class="glossy"
              v-for="(item, i) in this.selectedPokeTypes"
              :key="i"
              text-color="white"
              :style="{ 'background-color': this.typeColor[item.type.name] }"
              >{{ this.firstToUp(item.type.name) }}</q-chip
            >
          </div>
          <div class="text-h9 text-center">
            <q-chip
              class="glossy"
              size="md"
              color="red-4"
              text-color="white"
              dense
            >
              <q-avatar
                class="text-weight-medium glossy"
                color="red"
                text-color="white"
                style="opacity: 75%"
                >H</q-avatar
              >
              {{ (this.selectedPokeData.height * 0.1).toFixed(1) }}m
            </q-chip>
            <q-chip
              dense
              class="glossy"
              size="md"
              color="red-4"
              text-color="white"
            >
              <q-avatar
                class="text-weight-medium glossy"
                color="red"
                text-color="white"
                style="opacity: 75%"
                >W</q-avatar
              >
              {{ (this.selectedPokeData.weight * 0.1).toFixed(1) }}kg
            </q-chip>
          </div>

          <div class="text-h4 text-center q-mt-sm">
            <q-chip
              class="absolute"
              style="opacity: 60%; left: -10%"
              flat
              text-color="black"
              size="sm"
              dense
              >HP</q-chip
            >

            <q-linear-progress
              class="absolute q-mt-xs"
              stripe
              rounded
              size="15px"
              :value="this.selectedPokeStatsHp * 0.01"
              color="white"
            >
              <p
                class="absolute text-center text-caption text-weight-bold"
                style="color: black; left: 50%; top: -15%; opacity: 50%"
              >
                {{ this.selectedPokeStatsHp }}
              </p>
            </q-linear-progress>
          </div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <div class="text-h4 text-center q-mt-sm">
            <q-chip
              class="absolute"
              style="opacity: 60%; left: -10%"
              flat
              text-color="black"
              size="sm"
              dense
              >ATK</q-chip
            >

            <q-linear-progress
              class="absolute q-mt-xs"
              stripe
              rounded
              size="15px"
              :value="this.selectedPokeStatsAtk * 0.01"
              color="white"
            >
              <p
                class="absolute text-center text-caption text-weight-bold"
                style="color: black; left: 50%; top: -15%; opacity: 50%"
              >
                {{ this.selectedPokeStatsAtk }}
              </p>
            </q-linear-progress>
          </div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <div class="text-h4 text-center q-mt-sm">
            <q-chip
              class="absolute"
              style="opacity: 60%; left: -10%"
              flat
              text-color="black"
              size="sm"
              dense
              >DEF</q-chip
            >

            <q-linear-progress
              class="absolute q-mt-xs"
              stripe
              rounded
              size="15px"
              :value="this.selectedPokeStatsDef * 0.01"
              color="white"
            >
              <p
                class="absolute text-center text-caption text-weight-bold"
                style="color: black; left: 50%; top: -15%; opacity: 50%"
              >
                {{ this.selectedPokeStatsDef }}
              </p>
            </q-linear-progress>
          </div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <div class="text-h4 text-center q-mt-sm">
            <q-chip
              class="absolute"
              style="opacity: 60%; left: -10%"
              flat
              text-color="black"
              size="sm"
              dense
              >Sp Atk</q-chip
            >

            <q-linear-progress
              class="absolute q-mt-xs"
              stripe
              rounded
              size="15px"
              :value="this.selectedPokeStatsSpAtk * 0.01"
              color="white"
            >
              <p
                class="absolute text-center text-caption text-weight-bold"
                style="color: black; left: 50%; top: -15%; opacity: 50%"
              >
                {{ this.selectedPokeStatsSpAtk }}
              </p>
            </q-linear-progress>
          </div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <div class="text-h4 text-center q-mt-sm">
            <q-chip
              class="absolute"
              style="opacity: 60%; left: -10%"
              flat
              text-color="black"
              size="sm"
              dense
              >Sp Def</q-chip
            >

            <q-linear-progress
              class="absolute q-mt-xs"
              stripe
              rounded
              size="15px"
              :value="this.selectedPokeStatsSpDef * 0.01"
              color="white"
            >
              <p
                class="absolute text-center text-caption text-weight-bold"
                style="color: black; left: 50%; top: -15%; opacity: 50%"
              >
                {{ this.selectedPokeStatsSpDef }}
              </p>
            </q-linear-progress>
          </div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <div class="text-h4 text-center q-mt-sm">
            <q-chip
              class="absolute q-mr-xl"
              style="opacity: 60%; left: -10%"
              flat
              text-color="black"
              size="sm"
              dense
              >SPD</q-chip
            >

            <q-linear-progress
              class="absolute q-mt-xs"
              stripe
              rounded
              size="15px"
              :value="this.selectedPokeStatsSpd * 0.01"
              color="white"
            >
              <p
                class="absolute text-center text-caption text-weight-bold"
                style="color: black; left: 50%; top: -15%; opacity: 50%"
              >
                {{ this.selectedPokeStatsSpd }}
              </p>
            </q-linear-progress>
          </div>
        </q-card-section>
      </q-card>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import axios from "axios";

export default defineComponent({
  name: "Pokédex",

  data: () => ({
    baseUrlSearch: "https://pokeapi.co/api/v2/pokemon/",
    baseUrl: "https://pokeapi.co/api/v2",
    totalPoke: null,
    selectedPoke: "https://pokeapi.co/api/v2/pokemon/1/",
    selectedPokeId: null,
    selectedPokeData: {},
    selectedPokeImg: null,
    selectedPokeName: null,
    selectedPokeTypes: null,
    selectedPokeIdShow: null,
    selectedPokeStatsHp: null,
    selectedPokeStatsAtk: null,
    selectedPokeStatsDef: null,
    selectedPokeStatsSpAtk: null,
    selectedPokeStatsSpDef: null,
    selectedPokeStatsSpd: null,
    changeBgColor: null,
    pokeMax: 898,
    proxPoke: null,
    typeColor: {
      bug: "#3b9950",
      dark: "#5a5979",
      dragon: "#63c9d9",
      electric: "#fbfb72",
      fairy: "#ea1369",
      fighting: "#ef6138",
      fire: "#fd4c5a",
      flying: "#93b2c7",
      ghost: "#906790",
      grass: "#26cb4f",
      ground: "#6e491f",
      ice: "#86d2f5",
      normal: "#ca98a7",
      poison: "#9b69d9",
      psychic: "#f81c91",
      rock: "#8b3e21",
      steel: "#41be94",
      water: "#1552e2",
    },
  }),

  methods: {
    getSelectedPokeInfo(data) {
      if (this.selectedPokeId == this.pokeMax && data == +1) {
        this.proxPoke = this.baseUrlSearch + 1;
      } else if (this.selectedPokeId == 1 && data == -1) {
        this.proxPoke = this.baseUrlSearch + this.pokeMax;
      } else {
        this.proxPoke = this.baseUrlSearch + (this.selectedPokeId + data);
      }

      axios({
        method: "get",
        url: this.proxPoke,
      })
        .then((res) => {
          //this.loading.active = false;
          if (res.data != null) {
            console.log(res.data);
            this.selectedPokeData = res.data;
            this.selectedPokeImg =
              res.data.sprites.other["official-artwork"].front_default;
            this.selectedPokeName = this.firstToUp(res.data.name);
            this.selectedPokeTypes = res.data.types;
            this.selectedPokeId = res.data.id;
            this.getSelectedPokeIdShow(res.data.id);
            this.selectedPokeStatsHp = res.data.stats[0].base_stat;
            this.selectedPokeStatsAtk = res.data.stats[1].base_stat;
            this.selectedPokeStatsDef = res.data.stats[2].base_stat;
            this.selectedPokeStatsSpAtk = res.data.stats[3].base_stat;
            this.selectedPokeStatsSpDef = res.data.stats[4].base_stat;
            this.selectedPokeStatsSpd = res.data.stats[5].base_stat;
            this.changeBgColor =
              "background: linear-gradient(to top, " +
              this.typeColor[res.data.types[0].type.name] +
              ", rgb(255, 255, 255))";
          } else {
            // this.$router.push({ path: "/login" });
          }
        })
        .catch((err) => {
          // this.$router.push({ path: "/login" });
        });
    },

    firstToUp(string) {
      return string.charAt(0).toUpperCase() + string.slice(1);
    },

    getTotalPokes(count) {
      axios({
        method: "get",
        url: `${this.baseUrl}/pokemon/?limit=${count}`,
      })
        .then((res) => {
          //this.loading.active = false;
          if (res.data != null) {
            console.log(res);
            this.totalPoke = res.data.results;
          } else {
            // this.$router.push({ path: "/login" });
          }
        })
        .catch((err) => {
          // this.$router.push({ path: "/login" });
        });
    },

    async getPokedata(url) {
      await axios({
        method: "get",
        url: url,
      })
        .then((res) => {
          //this.loading.active = false;
          if (res.data != null) {
            console.log(res.data);
            this.selectedPokeData = res.data;
            this.selectedPokeImg =
              res.data.sprites.other["official-artwork"].front_default;
            this.selectedPokeName = this.firstToUp(res.data.name);
            this.selectedPokeTypes = res.data.types;
            this.selectedPokeId = res.data.id;
            this.getSelectedPokeIdShow(res.data.id);
            this.selectedPokeStatsHp = res.data.stats[0].base_stat;
            this.selectedPokeStatsAtk = res.data.stats[1].base_stat;
            this.selectedPokeStatsDef = res.data.stats[2].base_stat;
            this.selectedPokeStatsSpAtk = res.data.stats[3].base_stat;
            this.selectedPokeStatsSpDef = res.data.stats[4].base_stat;
            this.selectedPokeStatsSpd = res.data.stats[5].base_stat;
            this.changeBgColor =
              "background: linear-gradient(to top, " +
              this.typeColor[res.data.types[0].type.name] +
              ", rgb(255, 255, 255))";
          } else {
            // this.$router.push({ path: "/login" });
          }
        })
        .catch((err) => {
          // this.$router.push({ path: "/login" });
        });
    },

    getSelectedPokeIdShow(id) {
      if (id < 10) this.selectedPokeIdShow = "#00" + id;
      if (id > 9 && id < 100) this.selectedPokeIdShow = "#0" + id;
      if (id > 99) this.selectedPokeIdShow = "#" + id;
    },
  },

  mounted() {
    axios({
      method: "get",
      url: `${this.baseUrl}/pokemon/`,
    })
      .then((res) => {
        //this.loading.active = false;
        if (res.data != null) {
          this.getTotalPokes(res.data.count);
          // console.log(res.data.count);
          // console.log(Cookies.getAll());
        } else {
          // this.$router.push({ path: "/login" });
        }
      })
      .catch((err) => {
        // this.$router.push({ path: "/login" });
      });

    // axios({
    //   method: "get",
    //   url: this.selectedPoke,
    // })
    //   .then((res) => {
    //     //this.loading.active = false;
    //     if (res.data != null) {
    //       console.log(res);
    //       this.selectedPokeData = res.data;
    //       // console.log(res.data.count);
    //       // console.log(Cookies.getAll());
    //     } else {
    //       // this.$router.push({ path: "/login" });
    //     }
    //   })
    //   .catch((err) => {
    //     // this.$router.push({ path: "/login" });
    //   });

    this.getPokedata(this.selectedPoke);
  },
});
</script>
