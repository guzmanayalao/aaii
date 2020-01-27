/* eslint-disable prettier/prettier */
<template>
  <table>
    <thead>
      <th></th>
      <th></th>
      <th class="hover" @click="objSort('teamName')">
        <div>
          <span>Team Name</span>
          <img
            src="/img/sort-amount-up-alt-solid.svg"
            alt
            :class="{
              sortisactive:
                teamNameOrderProp != 'pending' && sortByNameProp === 'teamName'
            }"
            v-if="
              sortByNameProp !== 'teamName' ||
                (sortByNameProp == 'teamName' && teamNameOrderProp == 'pending')
            "
          />
          <img
            :class="{
              sortisactive:
                teamNameOrderProp != 'pending' && sortByNameProp === 'teamName'
            }"
            :src="
              teamNameOrderProp === 'asc' && sortByNameProp === 'teamName'
                ? '/img/sort-amount-up-alt-solid.svg'
                : teamNameOrderProp === 'desc' && sortByNameProp === 'teamName'
                ? '/img/sort-amount-down-alt-solid.svg'
                : ''
            "
            alt
            v-else
          />
        </div>
      </th>
      <th class="hover" @click="objSort('wins')">
        <div>
          <span>Wins</span>
          <img
            src="/img/sort-amount-up-alt-solid.svg"
            alt
            :class="{
              sortisactive:
                teamNameOrderProp != 'pending' && sortByNameProp === 'wins'
            }"
            v-if="
              sortByNameProp !== 'wins' ||
                (sortByNameProp == 'wins' && teamNameOrderProp == 'pending')
            "
          />
          <img
            :class="{
              sortisactive:
                teamNameOrderProp != 'pending' && sortByNameProp === 'wins'
            }"
            :src="
              teamNameOrderProp === 'asc' && sortByNameProp === 'wins'
                ? '/img/sort-amount-up-alt-solid.svg'
                : teamNameOrderProp === 'desc' && sortByNameProp === 'wins'
                ? '/img/sort-amount-down-alt-solid.svg'
                : ''
            "
            alt
            v-else
          />
        </div>
      </th>
      <th class="hover" @click="objSort('losses')">
        <div>
          <span>Losses</span>
          <img
            src="/img/sort-amount-up-alt-solid.svg"
            alt
            :class="{
              sortisactive:
                teamNameOrderProp != 'pending' && sortByNameProp === 'losses'
            }"
            v-if="
              sortByNameProp !== 'losses' ||
                (sortByNameProp == 'losses' && teamNameOrderProp == 'pending')
            "
          />
          <img
            :class="{
              sortisactive:
                teamNameOrderProp != 'pending' && sortByNameProp === 'losses'
            }"
            :src="
              teamNameOrderProp === 'asc' && sortByNameProp === 'losses'
                ? '/img/sort-amount-up-alt-solid.svg'
                : teamNameOrderProp === 'desc' && sortByNameProp === 'losses'
                ? '/img/sort-amount-down-alt-solid.svg'
                : ''
            "
            alt
            v-else
          />
        </div>
      </th>
      <th class="hover" @click="objSort('winPct')">
        <div>
          <span>Win PCT</span>
          <img
            src="/img/sort-amount-up-alt-solid.svg"
            alt
            :class="{
              sortisactive:
                teamNameOrderProp != 'pending' && sortByNameProp === 'winPct'
            }"
            v-if="
              sortByNameProp !== 'winPct' ||
                (sortByNameProp == 'winPct' && teamNameOrderProp == 'pending')
            "
          />
          <img
            :class="{
              sortisactive:
                teamNameOrderProp != 'pending' && sortByNameProp === 'winPct'
            }"
            :src="
              teamNameOrderProp === 'asc' && sortByNameProp === 'winPct'
                ? '/img/sort-amount-up-alt-solid.svg'
                : teamNameOrderProp === 'desc' && sortByNameProp === 'winPct'
                ? '/img/sort-amount-down-alt-solid.svg'
                : ''
            "
            alt
            v-else
          />
        </div>
      </th>
      <th class="hover" @click="objSort('gb')">
        <div>
          <span>GB</span>
          <img
            src="/img/sort-amount-up-alt-solid.svg"
            alt
            :class="{
              sortisactive:
                teamNameOrderProp != 'pending' && sortByNameProp === 'gb'
            }"
            v-if="
              sortByNameProp !== 'gb' ||
                (sortByNameProp == 'gb' && teamNameOrderProp == 'pending')
            "
          />
          <img
            :class="{
              sortisactive:
                teamNameOrderProp != 'pending' && sortByNameProp === 'gb'
            }"
            :src="
              teamNameOrderProp === 'asc' && sortByNameProp === 'gb'
                ? '/img/sort-amount-up-alt-solid.svg'
                : teamNameOrderProp === 'desc' && sortByNameProp === 'gb'
                ? '/img/sort-amount-down-alt-solid.svg'
                : ''
            "
            alt
            v-else
          />
        </div>
      </th>

      <th></th>
    </thead>
    <transition-group name="list-complete" tag="tbody" v-if="tableName == 'east'">
      <tr
        v-for="team in tempEast"
        :key="team.teamId"
        class="list-complete-item"
        :class="{ isTop8: team.top8 }"
      >
        <td>{{ team.confRank }}</td>
        <td class="image">
          <img :src="team.logo" alt />
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
          <a class="learnMoreButton" :href="team.espn">ESPN</a>
        </td>
      </tr>
    </transition-group>
    <transition-group name="list-complete" tag="tbody" v-if="tableName == 'west'">
      <tr
        v-for="team in tempWest"
        :key="team.teamId"
        class="list-complete-item"
        :class="{ isTop8: team.top8 }"
      >
        <td>{{ team.confRank }}</td>
        <td class="image">
          <img :src="team.logo" alt />
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
          <a class="learnMoreButton" :href="team.espn">ESPN</a>
        </td>
      </tr>
    </transition-group>
  </table>
</template>

<script>
export default {
  name: "DataTable",
  props: {
    east: {
      type: [Array, Object]
    },
    tempEast: {
      type: [Array, Object]
    },
    sortByName: {
      type: String
    },
    teamNameOrder: {
      type: String
    },
    tableName: {
      type: String
    }
  },
  data() {
    return {
      count: 0,
      sort: false,
      teamNameOrderProp: this.teamNameOrder,
      sortByNameProp: this.sortByName
    };
  },
  methods: {
    objSort(sortBy) {
      if (this.sortByNameProp != sortBy && this.sort === true) {
        this.tempEast = JSON.parse(JSON.stringify(this.east));
        this.count = 0;
        this.sort = false;
        console.log(this.sortByNameProp, sortBy);
      }
      this.sortByNameProp = sortBy;
      this.count++;
      if (this.count === 3) {
        this.tempEast = JSON.parse(JSON.stringify(this.east));
        this.count = 0;
        this.sort = false;
        this.teamNameOrderProp = "pending";
      } else {
        if (this.sort) {
          this.tempEast.reverse();
          this.teamNameOrderProp = "desc";
        } else {
          if (sortBy === "teamName") {
            this.tempEast.sort((a, b) =>
              a.teamSitesOnly.teamName > b.teamSitesOnly.teamName ? 1 : -1
            );
          } else if (sortBy === "wins") {
            this.tempEast.sort((a, b) =>
              parseFloat(a.winPct) > parseFloat(b.winPct) ? 1 : -1
            );
          } else if (sortBy === "losses") {
            this.tempEast.sort((a, b) =>
              parseInt(a.loss) > parseInt(b.loss) &&
              parseInt(a.win) > parseInt(b.win)
                ? -1
                : 1
            );
          } else if (sortBy === "winPct") {
            this.tempEast.sort((a, b) =>
              parseFloat(a.winPct) > parseFloat(b.winPct) ? 1 : -1
            );
          } else if (sortBy === "gb") {
            this.tempEast.sort((a, b) =>
              parseFloat(a.gamesBehind) > parseFloat(b.gamesBehind) ? 1 : -1
            );
          }
          this.teamNameOrderProp = "asc";
        }
        this.sort = true;
      }
      return;
    }
  },
  created() {
    this.east = this.east;
    this.tempEast = this.tempEast;
    this.tempEast = JSON.parse(JSON.stringify(this.east));
  }
};
</script>

<style></style>
