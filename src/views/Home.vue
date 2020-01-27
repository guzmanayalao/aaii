<template>
  <div class="home">
    <div>
      <div class="tabGroup">
        <button
          class="tab"
          @click="(tabEast = false), (tabWest = true), (tabLeague = false)"
          :class="{ activeWest: tabWest == true }"
        >
          West
        </button>
        <button
          class="tab"
          @click="(tabEast = false), (tabWest = false), (tabLeague = true)"
        >
          League
        </button>
        <button
          class="tab"
          @click="(tabEast = true), (tabWest = false), (tabLeague = false)"
          :class="{ active: tabEast == true }"
        >
          East
        </button>
      </div>

      <div class="tableWrapper">
        <h1 v-if="tabEast">Eastern Conference</h1>
        <h1 v-if="tabWest">Western Conference</h1>
        <h1 v-if="tabLeague">League</h1>
        <transition name="fade">
          <DataTable
            v-if="tabEast"
            :east="east"
            :tempEast="tempEast"
            :sortByName="sortByName"
            :teamNameOrder="teamNameOrder"
          />
        </transition>
        <transition name="fade">
          <DataTable
            v-if="tabLeague"
            :east="nba"
            :tempEast="tempNBA"
            :sortByName="sortByName"
            :teamNameOrder="teamNameOrder"
            :tabLeague="tabLeague"
          />
        </transition>
        <transition name="fade">
          <DataTable
            v-if="tabWest"
            :east="west"
            :tempEast="tempWest"
            :sortByName="sortByName"
            :teamNameOrder="teamNameOrder"
            :tabWest="tabWest"
          />
        </transition>
      </div>
    </div>
  </div>
</template>
<style lang="scss">
.tabGroup {
  margin-bottom: 1rem;
  display: inline-block;
  box-shadow: 0px 5px 5px -1px rgba(0, 0, 0, 0.15);
  border-radius: 10px;
  button.tab {
    background: white;
    padding: 1rem;
    font-weight: bold;
    border: none;
    &:hover {
      background: darken(white, 5);
    }
    &:first-of-type {
      border-top-left-radius: 10px;
      border-bottom-left-radius: 10px;
    }
    &.active {
      background: rgb(0, 110, 255);
      color: white;
      &:hover {
        background: darken(rgb(0, 110, 255), 5);
      }
    }
    &.activeWest {
      background: rgb(255, 0, 0);
      color: white;
      &:hover {
        background: darken(rgb(255, 0, 0), 5);
      }
    }
    &:last-of-type {
      border-top-right-radius: 10px;
      border-bottom-right-radius: 10px;
    }
  }
}
.home {
  margin-bottom: 3rem;
}


</style>
<script>
// @ is an alias to /src
import axios from "axios";
import DataTable from "@/components/DataTable.vue";

export default {
  name: "home",
  components: { DataTable },
  data() {
    return {
      nba: {},
      tempNBA: {},
      erros: [],
      standings: {},
      teams: [],
      east: {},
      tempEast: {},
      west: {},
      tempWest: {},
      count: 0,
      teamNameOrder: "pending",
      sortByName: "teamName",
      tabEast: true,
      tabWest: false,
      tabLeague: false,
      sort: false
    };
  },
  methods: {},
  mounted() {
    //Initial Ajax Request
    axios
      .get(`/api.json`)
      .then(response => {
        // JSON responses are automatically parsed.

        this.east = JSON.parse(
          JSON.stringify(response.data.league.standard.conference.east)
        );
        this.west = JSON.parse(
          JSON.stringify(response.data.league.standard.conference.west)
        );

        //Add logo To dataset
        this.east.forEach(function(team) {
          team.logo = `//cdn.nba.net/assets/logos/teams/secondary/web/${team.teamSitesOnly.teamTricode}.svg`;
          team.espn = `https://www.espn.com/nba/team/_/name/${team.teamSitesOnly.teamTricode}/${team.teamSitesOnly.teamName}-${team.teamSitesOnly.teamCode}`;
          if (team.confRank <= 8) {
            team.top8 = true;
          }
        });
        this.west.forEach(function(team) {
          team.logo = `//cdn.nba.net/assets/logos/teams/secondary/web/${team.teamSitesOnly.teamTricode}.svg`;
          team.espn = `https://www.espn.com/nba/team/_/name/${team.teamSitesOnly.teamTricode}/${team.teamSitesOnly.teamName}-${team.teamSitesOnly.teamCode}`;
          if (team.confRank <= 8) {
            team.top8 = true;
          }
        });

        this.nba = [
          ...JSON.parse(
            JSON.stringify(response.data.league.standard.conference.east)
          ),
          ...JSON.parse(
            JSON.stringify(response.data.league.standard.conference.west)
          )
        ];
        this.nba.forEach(function(team) {
          team.logo = `//cdn.nba.net/assets/logos/teams/secondary/web/${team.teamSitesOnly.teamTricode}.svg`;
          team.espn = `https://www.espn.com/nba/team/_/name/${team.teamSitesOnly.teamTricode}/${team.teamSitesOnly.teamName}-${team.teamSitesOnly.teamCode}`;
          if (team.confRank <= 8) {
            team.top8 = true;
          }
        });
        this.nba.sort((a, b) => (a.winPctV2 > b.winPctV2 ? -1 : 1));
        //todo needs tempNBA?
        this.tempEast = JSON.parse(JSON.stringify(this.east));
        this.tempWest = JSON.parse(JSON.stringify(this.west));
        this.tempNBA = JSON.parse(JSON.stringify(this.nba));

      })
      .catch(e => {
        this.errors.push(e);
      });
  },
  created() {
    // async / await version (created() becomes async created())
    //
    // try {
    //   const response = await axios.get(`http://jsonplaceholder.typicode.com/posts`)
    //   this.posts = response.data
    // } catch (e) {
    //   this.errors.push(e)
    // }
  }
};
</script>
