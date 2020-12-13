<template>
  <div class="home">
    <portal to="header-right" v-if="hide">
      <button class="back-button" @click="hideDetails">
        <font-awesome-icon icon="chevron-left" />
      </button>
    </portal>
    <div class="main-info" :class="{ hide: hide }">
      <SearchContainer />
      <div class="card-container">
        <div class="card">
          <div class="top" v-if="stopPlace2" @click="showDetails">
            {{ stopPlace1.properties.name }} - {{ stopPlace2.properties.name }}
          </div>
          <div class="bottom" v-if="departures">
            <span class="departure-title">Neste avganger:</span>
            <div class="all-departures">
              <span
                class="departure"
                v-for="(departure, $index) in departures"
                :key="$index"
                >{{ departure.expectedDepartureTime | moment("HH:mm") }}</span
              >
            </div>
          </div>
        </div>
      </div>
    </div>
    <Details
      class="details"
      :class="{ show: hide }"
      :selected-route="selectedRoute"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import createEnturService, { TypeName } from "@entur/sdk";
import Details from "@/components/Details";
import _ from "lodash";
import SearchContainer from "../components/SearchContainer.vue";
const service = createEnturService({ clientName: "ferryTimes-magnus_grande" });
export default {
  name: "Home",
  components: { Details, SearchContainer },
  computed: {},
  data() {
    return {
      stopPlace1: null,
      stopPlace1Id: null,
      stopPlace2: null,
      stopPlace2Id: null,
      departures: null,
      hide: false,
      selectedRoute: null,
    };
  },
  methods: {
    hideDetails() {
      this.hide = false;
      setTimeout(() => {
        this.selectedRoute = null;
      }, 300);
    },
    showDetails() {
      this.hide = true;
      this.selectedRoute = {
        from: this.stopPlace1,
        to: this.stopPlace2,
        departures: this.departures,
      };
    },
  },
  async mounted() {
    const temp1 = await service.getFeatures("Linge");
    this.stopPlace1 = _.find(temp1, (stop) => {
      return stop.properties.category.includes("harbourPort");
    });
    console.log(this.stopPlace1);
    this.stopPlace1Id = this.stopPlace1.properties.id;
    const temp2 = await service.getFeatures("Eidsdal");
    this.stopPlace2 = _.find(temp2, (stop) => {
      return stop.properties.category.includes("harbourPort");
    });
    this.stopPlace2Id = this.stopPlace2.properties.id;
    this.departures = await service.getDeparturesBetweenStopPlaces(
      this.stopPlace1Id,
      this.stopPlace2Id
    );
    console.log(this.departures);
  },
};
</script>
<style lang="scss" scoped>
.home {
  display: flex;
  height: calc(100vh - 84px);
  width: 100vw;
  position: relative;
  .details {
    width: 100vw;
    min-width: 100vw;
    transition: left 0.4s ease-in-out;
    position: absolute;
    left: 100vw;
    &.show {
      left: 0;
    }
  }
  .main-info {
    width: 100vw;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    transition: left 0.4s ease-in-out;
    position: absolute;
    left: 0;
    &.hide {
      left: -100vw;
    }
    .search-container {
      height: 20%;
    }
    .card-container {
      height: 80%;
      background: white;
      .card {
        width: calc(100% - 24px);
        background: white;
        height: 80px;
        display: flex;
        flex-direction: column;
        border-radius: 6px;
        margin: 12px;
        box-shadow: 0px 5px 8px 3px rgba(0, 0, 0, 0.16);
        color: black;
        .top,
        .bottom {
          height: 32px;
          font-size: 18px;
          text-align: left;
          margin: 8px;
        }
        .top {
          text-transform: uppercase;
        }
        .bottom {
          font-size: 14px;
          line-height: 32px;
          display: flex;
          justify-content: space-between;
          .departure-title {
            white-space: nowrap;
            width: 30%;
          }
          .all-departures {
            width: 70%;
            overflow: auto;
            .departure {
              margin-right: 4px;
            }
          }
        }
      }
    }
  }
}
.back-button {
  height: 44px;
  background: transparent;
  border: none;
  color: white;
  font-size: 22px;
}
</style>