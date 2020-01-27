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
            tableName="east"
          />
        </transition>
        <transition name="fade">
          <table v-if="tabLeague">
            <thead>
              <th></th>
              <th></th>
              <th class="hover" @click="objSort('teamName')">
                <div>
                  <span> Team Name </span>
                  <img
                    src="/img/sort-amount-up-alt-solid.svg"
                    alt=""
                    :class="{
                      sortisactive:
                        teamNameOrder != 'pending' && sortByName === 'teamName'
                    }"
                    v-if="
                      sortByName !== 'teamName' ||
                        (sortByName == 'teamName' && teamNameOrder == 'pending')
                    "
                  />
                  <img
                    :class="{
                      sortisactive:
                        teamNameOrder != 'pending' && sortByName === 'teamName'
                    }"
                    :src="
                      teamNameOrder === 'asc' && sortByName === 'teamName'
                        ? '/img/sort-amount-up-alt-solid.svg'
                        : teamNameOrder === 'desc' && sortByName === 'teamName'
                        ? '/img/sort-amount-down-alt-solid.svg'
                        : ''
                    "
                    alt=""
                    v-else
                  />
                </div>
              </th>
              <th class="hover" @click="objSort('wins')">
                <div>
                  <span>Wins</span>
                  <img
                    src="/img/sort-amount-up-alt-solid.svg"
                    alt=""
                    :class="{
                      sortisactive:
                        teamNameOrder != 'pending' && sortByName === 'wins'
                    }"
                    v-if="
                      sortByName !== 'wins' ||
                        (sortByName == 'wins' && teamNameOrder == 'pending')
                    "
                  />
                  <img
                    :class="{
                      sortisactive:
                        teamNameOrder != 'pending' && sortByName === 'wins'
                    }"
                    :src="
                      teamNameOrder === 'asc' && sortByName === 'wins'
                        ? '/img/sort-amount-up-alt-solid.svg'
                        : teamNameOrder === 'desc' && sortByName === 'wins'
                        ? '/img/sort-amount-down-alt-solid.svg'
                        : ''
                    "
                    alt=""
                    v-else
                  />
                </div>
              </th>
              <th class="hover">
                <div>
                  <span>Losses</span>
                  <img
                    src="../../public/img/sort-amount-up-alt-solid.svg"
                    alt=""
                  />
                </div>
              </th>

              <th class="hover">
                <div>
                  <span>Win PCT</span>
                  <img
                    src="../../public/img/sort-amount-up-alt-solid.svg"
                    alt=""
                  />
                </div>
              </th>
              <th class="hover">
                <div>
                  <span>GB</span>
                  <img
                    src="../../public/img/sort-amount-up-alt-solid.svg"
                    alt=""
                  />
                </div>
              </th>

              <th></th>
            </thead>
            <transition-group name="list-complete" tag="tbody">
              <tr
                v-for="team in nba"
                :key="team.teamId"
                class="list-complete-item"
                :class="{ isTop8: team.top8 }"
              >
                <td>{{ team.confRank }}</td>
                <td class="image">
                  <img :src="team.logo" alt="" />
                </td>
                <td>
                  {{ team.teamSitesOnly.teamName }}
                  {{ team.teamSitesOnly.teamNickname }}
                </td>
                <td>{{ team.win }}</td>
                <td>{{ team.loss }}</td>
                <td>{{ team.winPctV2 }}%</td>
                <td>{{ team.gamesBehind }}</td>
                <td>
                  <a class="learnMoreButton" :href="team.espn">Learn More</a>
                </td>
              </tr>
            </transition-group>
          </table>
        </transition>
        <transition name="fade">
          <table v-if="tabWest">
            <thead>
              <th></th>
              <th></th>
              <th class="hover" @click="objSort('teamName')">
                <div>
                  <span> Team Name </span>
                  <img
                    src="/img/sort-amount-up-alt-solid.svg"
                    alt=""
                    :class="{
                      sortisactive:
                        teamNameOrder != 'pending' && sortByName === 'teamName'
                    }"
                    v-if="
                      sortByName !== 'teamName' ||
                        (sortByName == 'teamName' && teamNameOrder == 'pending')
                    "
                  />
                  <img
                    :class="{
                      sortisactive:
                        teamNameOrder != 'pending' && sortByName === 'teamName'
                    }"
                    :src="
                      teamNameOrder === 'asc' && sortByName === 'teamName'
                        ? '/img/sort-amount-up-alt-solid.svg'
                        : teamNameOrder === 'desc' && sortByName === 'teamName'
                        ? '/img/sort-amount-down-alt-solid.svg'
                        : ''
                    "
                    alt=""
                    v-else
                  />
                </div>
              </th>
              <th class="hover" @click="objSort('wins')">
                <div>
                  <span>Wins</span>
                  <img
                    src="/img/sort-amount-up-alt-solid.svg"
                    alt=""
                    :class="{
                      sortisactive:
                        teamNameOrder != 'pending' && sortByName === 'wins'
                    }"
                    v-if="
                      sortByName !== 'wins' ||
                        (sortByName == 'wins' && teamNameOrder == 'pending')
                    "
                  />
                  <img
                    :class="{
                      sortisactive:
                        teamNameOrder != 'pending' && sortByName === 'wins'
                    }"
                    :src="
                      teamNameOrder === 'asc' && sortByName === 'wins'
                        ? '/img/sort-amount-up-alt-solid.svg'
                        : teamNameOrder === 'desc' && sortByName === 'wins'
                        ? '/img/sort-amount-down-alt-solid.svg'
                        : ''
                    "
                    alt=""
                    v-else
                  />
                </div>
              </th>
              <th class="hover">
                <div>
                  <span>Losses</span>
                  <img
                    src="../../public/img/sort-amount-up-alt-solid.svg"
                    alt=""
                  />
                </div>
              </th>

              <th class="hover">
                <div>
                  <span>Win PCT</span>
                  <img
                    src="../../public/img/sort-amount-up-alt-solid.svg"
                    alt=""
                  />
                </div>
              </th>
              <th class="hover">
                <div>
                  <span>GB</span>
                  <img
                    src="../../public/img/sort-amount-up-alt-solid.svg"
                    alt=""
                  />
                </div>
              </th>

              <th></th>
            </thead>
            <transition-group name="list-complete" tag="tbody">
              <tr
                v-for="team in tempWest"
                :key="team.teamId"
                class="list-complete-item"
                :class="{ isTop8: team.top8 }"
              >
                <td>{{ team.confRank }}</td>
                <td class="image">
                  <img :src="team.logo" alt="" />
                </td>
                <td>
                  {{ team.teamSitesOnly.teamName }}
                  {{ team.teamSitesOnly.teamNickname }}
                </td>
                <td>{{ team.win }}</td>
                <td>{{ team.loss }}</td>
                <td>{{ team.winPctV2 }}%</td>
                <td>{{ team.gamesBehind }}</td>
                <td>
                  <a class="learnMoreButton buttonWest" :href="team.espn"
                    >Learn More</a
                  >
                </td>
              </tr>
            </transition-group>
          </table>
        </transition>
      </div>
    </div>
  </div>
</template>
<style lang="scss">
.tabGroup {
  margin-bottom: 1rem;
  button.tab {
    background: white;
    padding: 1rem;
    font-weight: bold;
    border: none;
    &:first-of-type {
      border-top-left-radius: 10px;
      border-bottom-left-radius: 10px;
    }
    &.active {
      background: rgb(0, 110, 255);
      color: white;
    }
    &.activeWest {
      background: rgb(255, 0, 0);
      color: white;
    }
    &:last-of-type {
      border-top-right-radius: 10px;
      border-bottom-right-radius: 10px;
    }
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: all 0.3s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
  transition: all 0.3s;
}
.list-complete-item {
  transition: all 1s;
  margin-right: 10px;
}
.list-complete-enter, .list-complete-leave-to
/* .list-complete-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
.list-complete-leave-active {
  position: absolute;
}
.isTop8 {
  background: linear-gradient(
    180deg,
    rgba(147, 230, 255, 0.145) 0%,
    rgba(151, 231, 251, 0.18) 100%
  );

  border: 1px solid white;
  position: relative;
  z-index: 1;
  margin: 1rem;
  font-weight: 700;
  &:hover {
    td {
      background: darken(rgba(151, 231, 251, 0.18), 2);
    }
  }
}
.home {
  height: 100%;
}
.tableWrapper {
  display: flex;
  min-height: 1166px;
  align-items: flex-start;
  height: 100%;
  flex-direction: column;
  background: #fff;
  box-shadow: 0px 20px 54px -13px rgba(0, 0, 0, 0.15);
  border-radius: 1rem;
  margin: auto;
  max-width: 1200px;
  h1 {
    margin: 0;
    padding: 2rem 3rem;
  }
}
table {
  width: 100%;
  border-collapse: collapse;
  font-size: 14px;

  tr {
    border-bottom: 1px solid #eee;
    &:hover {
      td {
        background: darken(#fff, 2);
      }
    }
  }
  td {
    padding: 0.2rem 0;
    .learnMoreButton {
      background: rgb(0, 132, 255);
      color: white;
      text-decoration: none;
      padding: 0.5rem 1rem;
      box-shadow: 0px 10px 14px -13px rgba(0, 0, 0, 0.35);
      border-radius: 1rem;
      font-size: 14px;
      display: block;
      max-width: 50px;
      margin: auto;
      transform: translateY(0px);
      transition: transform 0.2s;

      &:hover {
        transition: transform 0.2s;

        transform: translateY(-3px);
      }
      &.buttonWest {
        background: rgb(255, 0, 0);
      }
    }
    &.image {
      width: 50px;
    }
  }
  th {
    padding: 1rem;
    div {
      display: flex;
      width: 100%;
      justify-content: center;
      img {
        width: 15px;
        margin-left: 1rem;
        opacity: 0.15;
        transition: all 0.2s;

        &.sortisactive {
          opacity: 1;
          transition: all 0.2s;
        }
      }
    }

    &.hover {
      cursor: pointer;
      &:hover {
        background: darken(#ffffff, 5);
      }
    }
  }
  img {
    width: 45px;
  }
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
      .get(`http://localhost:8080/api.json`)
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
