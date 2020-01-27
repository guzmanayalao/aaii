/* eslint-disable prettier/prettier */
<template>
  <table>
    <thead>
      <th></th>
      <th></th>
      <th class="hover" @click="objSort('teamName')">
        <div>
          <span>Team</span>
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
      <th class="hover" :class="{'hideMobile': toggleColumn == true}" @click="objSort('wins')">
        <div>
          <span>W</span>
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
      <th class="hover" :class="{'hideMobile': toggleColumn == true}" @click="objSort('losses')">
        <div>
          <span>L</span>
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
      <th class="hover" :class="{'hideMobile': toggleColumn == false}" @click="objSort('winPct')" >
        <div class="smallCell">
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
      <th class="hover" :class="{'hideMobile': toggleColumn == false}" @click="objSort('gb')">
        <div class="smallCell">
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
      <th class="hideMobile"></th>
      <th class="hover showMobile" @click="toggleColumn = !toggleColumn">
          <img src="/img/ellipsis-h-solid.svg">
      </th>
    </thead>
    <transition-group name="list-complete" tag="tbody">
      <tr
        v-for="team in tempEast"
        :key="team.teamId"
        class="list-complete-item"
        :class="{ isTop8: team.top8, 'west': tabWest, 'league': tabLeague }"
      >
        <td>{{ team.confRank }}</td>
        <td class="image">
          <img :src="team.logo" alt />
        </td>
        <td>
          <a :href="team.espn" class="link">
              {{ team.teamSitesOnly.teamName }}
              {{ team.teamSitesOnly.teamNickname }}
          </a>

        </td>
        <td :class="{'hideMobile': toggleColumn === true}">{{ team.win }}</td>
        <td :class="{'hideMobile': toggleColumn === true}">{{ team.loss }}</td>
        <td :class="{'hideMobile': toggleColumn === false}">{{ team.winPctV2 }}%</td>
        <td :class="{'hideMobile': toggleColumn === false}">
            <div class="smallCell">{{ team.gamesBehind }}</div>
        </td>
        <td class="hideMobile" :class="{'hideMobile': toggleColumn === false }">
          <a class="learnMoreButton" :class="{'buttonWest': tabWest === true, 'buttonWhite': tabLeague === true }" :href="team.espn">ESPN</a>
        </td>
        <td class="showMobile"></td>
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
    tabWest: {
      type: Boolean
    },
    tabLeague: {
      type: Boolean
    }

  },
  data() {
    return {
      count: 0,
      sort: false,
      teamNameOrderProp: this.teamNameOrder,
      sortByNameProp: this.sortByName,
      toggleColumn: false
    };
  },
  methods: {
    objSort(sortBy) {
      if (this.sortByNameProp != sortBy && this.sort === true) {
        this.tempEast = JSON.parse(JSON.stringify(this.east));
        this.count = 0;
        this.sort = false;
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
              parseInt(a.win) > parseInt(b.win) ? 1 : -1
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

<style lang="scss">
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
  &.west {
    background: rgba(255,0,0,0.05);
    &:hover {
      background: darken(rgba(255,0,0,0.05), 2);
    }
  }
  &.league {
    background: rgba(0,0,0,0.05);
    &:hover {
      background: darken(rgba(0,0,0,0.05), 2);
    }

  }
  &:hover {
    td {
      background: darken(rgba(151, 231, 251, 0.18), 2);
      transition: all 0.4s;
    }
  }
}
.showMobile {
  display: none; 
  @media screen and (max-width: 600px) {
    display: table-cell;
  }
  img {
    width: 10px;
  }
}
.hideMobile {
  @media screen and (max-width: 600px) {
    display: none;
  }
}

.tableWrapper {
  display: flex;
  align-items: flex-start;
  flex-direction: column;
  background: #fff;
  box-shadow: 0px 20px 54px -13px rgba(0, 0, 0, 0.15);
  border-radius: 1rem;
  margin: auto;
  max-width: 1200px;
  overflow-x: hidden;
      @media screen and (max-width: 600px) {
        border-radius: 0;
      }

  h1 {
    margin: 0;
    padding: 2rem 3rem;
    @media screen and (max-width: 600px) {
        padding: 1rem;
        font-size: 17px;
        margin: auto;
        text-align: center;
    }
  }
}
table {
  width: 100%;
  border-collapse: collapse;
  font-size: 14px;
  @media screen and (max-width: 600px) {
    font-size: 11px;
  }
  tr {
    border-bottom: 1px solid #eee;
    transition: all 0.2s;

    &:hover {
      td {
        background: darken(#fff, 2);
        transition: all 0.2s;

      }
    }
  }
  td {
    padding: 0.2rem 0;
    > a.link{
        color: black;
        &:link,
        &:visited,
        &:active {
          color: black;
        }
      }
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
      &.buttonWhite {
        background: white;
        color: black;
      }
      
    }
    &.image {
      width: 50px;
    }
  }
  th {
    padding: 1rem;
    @media screen and (max-width: 600px) {
      padding: .5rem .2rem;
    }
    div {
      display: flex;
      width: 100%;
      justify-content: center;
      height: 20px;
      img {
        width: 15px;
        margin-left: 1rem;
        opacity: 0.15;
        transition: all 0.2s;
        @media screen and (max-width: 600px) {
          width: 10px;
        }
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
    @media screen and (max-width: 600px) {
          width: 30px;
        }
  }
}
</style>
