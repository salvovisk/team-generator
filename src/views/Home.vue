<template>
  <!-- :style="player.selected ? 'selected' : ''" -->
  <WelcomeMsg v-show="MsgIsVisible" @close-msg="handleMsgClosing" />

  <section class="selectionSection" v-show="playerSelectionIsVisible">
    <div class="carouselCards">
      <div
        v-for="player in players"
        :key="player.id"
        :class="[
          findActivePlayer(player) ? 'isActive' : '',
          'playerSelectorContainer',
        ]"
      >
        <div @click="toggleSelectedPlayer(player)" class="cardBody">
          <img :src="player.avatar" alt="operator" class="cardImg" />
          <div class="cardTextWrapper">
            <h4
              :class="[
                findActivePlayer(player) ? 'isActive-text' : '',
                'cardTextTitle',
              ]"
              class="cardTextTitle"
            >
              {{ player.name }}
            </h4>
          </div>
        </div>
      </div>
    </div>
    <div class="btnConfirm">
      <button
        class="defaultBtn"
        v-show="confirmBtnIsVisible"
        @click="handleTeamGenerator"
      >
        Confirm
      </button>
    </div>
  </section>
  <section class="generatedTeams">
    <div
      class="generatedTeamWrapper"
      v-for="(team, teamKey) of teamsGenerated"
      :key="teamKey"
    >
      <h2>TEAM {{ teamKey + 1 }}</h2>
      <div class="teamsWrapper">
        <ul v-for="(player, playerKey) of team" :key="playerKey">
          <div class="playerInTeamsWrapper">
            <div @click="toggleSelectedPlayer(player)" class="cardBodysm">
              <img :src="player.avatar" alt="operator" class="cardImgsm" />
              <div class="cardTextWrappersm">
                <h4>
                  {{ player.name }}
                </h4>
              </div>
            </div>
          </div>
        </ul>
      </div>
    </div>
  </section>
  <div class="resetBtn">
    <button
      class="defaultBtn"
      v-show="resetBtnIsVisible"
      @click="resetTeamGenerator"
    >
      Reset
    </button>
  </div>
</template>

<script>
import WelcomeMsg from "../components/WelcomeMsg.vue";
export default {
  components: {
    WelcomeMsg,
  },
  data() {
    return {
      playerSelectionIsVisible: true,
      MsgIsVisible: true,
      selectedPlayer: [],
      resetBtnIsVisible: false,
      confirmBtnIsVisible: false,
      teamsNumb: null,
      players: [
        {
          id: 0,
          name: "Paolo Brosio",
          avatar: require("../assets/avatar/operator1.jpeg"),
        },
        {
          id: 1,
          name: "Bruno Vespa",
          avatar: require("../assets/avatar/operator2.jpeg"),
        },
        {
          id: 2,
          name: "Majin Pingu",
          avatar: require("../assets/avatar/operator6.jpeg"),
        },
        {
          id: 3,
          name: "Papa Ratzinger",
          avatar: require("../assets/avatar/operator3.jpeg"),
        },
        {
          id: 4,
          name: "Pippo Baudo",
          avatar: require("../assets/avatar/operator4.jpeg"),
        },
        {
          id: 5,
          name: "Dov'è Bugo",
          avatar: require("../assets/avatar/operator5.jpeg"),
        },
        {
          id: 6,
          name: "Luca Giurato",
          avatar: require("../assets/avatar/operator1.jpeg"),
        },
        {
          id: 7,
          name: "Pazzo Cane",
          avatar: require("../assets/avatar/operator7.jpeg"),
        },
        {
          id: 8,
          name: "MassiCape",
          avatar: require("../assets/avatar/operator3.jpeg"),
        },
        {
          id: 9,
          name: "Orietta Berti",
          avatar: require("../assets/avatar/operator2.jpeg"),
        },
        {
          id: 10,
          name: "Alberto B.",
          avatar: require("../assets/avatar/operator7.jpeg"),
        },
      ],
      teamsGenerated: [],
    };
  },
  computed: {
    itemsLength() {
      return this.selectedPlayer.length;
    },
  },
  watch: {
    itemsLength() {
      if (this.selectedPlayer.length > 4) {
        this.confirmBtnIsVisible = true;
      }
      if (this.selectedPlayer.length < 5) {
        this.confirmBtnIsVisible = false;
      }
    },
  },
  methods: {
    toggleConfirmBtn() {
      this.confirmBtnIsVisible = true;
    },
    handleMsgClosing() {
      this.MsgIsVisible = !this.MsgIsVisible;
    },
    toggleSelectedPlayer(player) {
      if (this.selectedPlayer.includes(player)) {
        let toRemove = player;
        this.selectedPlayer = this.selectedPlayer.filter(
          (item) => item !== toRemove
        );
      } else {
        this.selectedPlayer.push(player);
      }
    },
    handleConfirmBtnShow() {
      if (this.selectedPlayer.length <= 5) {
        return false;
      } else return true;
    },
    findActivePlayer(player) {
      if (this.selectedPlayer.includes(player)) {
        return true;
      } else return false;
    },
    handleTeamGenerator() {
      const selectedPlayers = this.selectedPlayer;
      const selectedPlayersNames = selectedPlayers
        .map((i) => i.name)
        .join(", ");

      const confirmMsg = `Sicuro di voler creare dei team con i seguenti player: ${selectedPlayersNames}?`;

      if (window.confirm(confirmMsg)) {
        let shuffle = selectedPlayers.sort(() => Math.random() - 0.5);

        const chunkArray = (myArray, divider) => {
          this.teamsGenerated = [];
          let i = 0;
          let arrayLen = myArray.length;
          let tempArray = [];
          for (i = 0; i < arrayLen; i += divider) {
            let divide = myArray.slice(i, i + divider);
            tempArray.push(divide);
          }
          this.teamsGenerated.push(...tempArray);
          this.teamsNumb = this.teamsGenerated.length;
          this.playerSelectionIsVisible = false;
          this.resetBtnIsVisible = true;
          this.MsgIsVisible = false;
          return tempArray;
        };
        switch (selectedPlayers.length) {
          case 5:
            {
              chunkArray(shuffle, 3);
            }
            break;
          case 6:
            {
              chunkArray(shuffle, 3);
            }
            break;
          case 7:
            {
              chunkArray(shuffle, 4);
            }
            break;
          case 8:
            {
              chunkArray(shuffle, 4);
            }
            break;
          case 9:
            {
              chunkArray(shuffle, 3);
            }
            break;
          case 10:
            {
              chunkArray(shuffle, 4);
            }
            break;
          case 11:
            {
              chunkArray(shuffle, 4);
            }
            break;
          default:
            chunkArray(shuffle, 3);
        }
      }
    },
    resetTeamGenerator() {
      this.MsgIsVisible = true;
      this.playerSelectionIsVisible = true;
      this.teamsNumb = 0;
      this.selectedPlayer = [];
      this.teamsGenerated = [];
      this.resetBtnIsVisible = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.teams-number-selection {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;

  & input {
    width: 40px;
    text-align: center;
  }
}
/* .selectionSection {
  display: flex;
  flex-direction: column;
  align-items: center;
  @media (min-width: 768px) {
    flex-direction: row;
}
} */
.carouselCards {
  color: black;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  max-width: 100%;
  scroll-snap-type: x mandatory;
  overflow-x: scroll;
  scroll-behavior: smooth;
  padding: 10px 0 10px 40px;
  &::-webkit-scrollbar {
    display: none;
    -ms-overflow-style: none; /* IE and Edge */
    scrollbar-width: none; /* Firefox */
  }
  @media (min-width: 768px) {
    padding-left: 20px;
    justify-content: center;
    flex-direction: row;
    flex-wrap: wrap;
  }
}

.playerSelectorContainer {
  margin-top: 15px;
  margin-right: 20px;
  height: 180px;
  width: 128px;
  border-radius: 12px;
  box-shadow: 0 0 10px 1px rgba(25, 25, 25, 0.5);
  padding: 25px;
  background-color: white;
  transition: all 0.2s ease-in-out;
  perspective: 1000px;
  transform-style: preserve-3d;
  @media (min-width: 768px) {
    margin-bottom: 10px;
    margin-right: 20px;
    cursor: pointer;
  }
}

.isActive {
  transform: translateY(-10px);
  background-color: #1d3557;
}
.isActive-text {
  color: white;
}
.cardTextTitle {
  transition: all 0.2s ease-in-out;
  perspective: 1000px;
  transform-style: preserve-3d;
}
.cardBody {
  min-height: 140px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}
.cardImg {
  height: 128px;
  width: 128px;
  border-radius: 50px;
  object-fit: cover;
}

.btnConfirm {
  display: flex;
  justify-content: center;
}
.defaultBtn {
  margin-top: 25px;
  min-width: 200px;
  min-height: 60px;
  height: max-content;
  background-color: #1d3557;
  border: none;
  border-radius: 8px;
  color: white;
  font-size: 20px;
  text-decoration: none;
  text-align: center;
  transition: background 250ms ease-in-out, transform 150ms ease;
  -webkit-appearance: none;
  -moz-appearance: none;
  &:hover {
    background: #0053ba;
    cursor: pointer;
  }
  &:active {
    transform: scale(0.9);
  }
  &:focus {
    outline: none;
  }
}
.generatedTeams {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  align-items: center;
  text-align: center;
  @media (min-width: 768px) {
    flex-direction: row;
    align-items: baseline;
  }
}
.generatedTeamWrapper {
  max-width: 100vw;
  min-width: 100vw;
  @media (min-width: 768px) {
    min-width: 30vw;
    margin-right: 20px;
  }
}
.teamsWrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  & ul {
    padding-bottom: 25px;
    border-bottom: solid 1px #1d3557;
  }
}
.playerInTeamsWrapper {
  height: 64px;
}

.cardBodysm {
  display: flex;
  flex-direction: row;
  justify-content: left;
  align-items: center;
}
.cardImgsm {
  height: 64px;
  width: 64px;
  border-radius: 25px;
  object-fit: cover;
  margin-right: 25px;
}
.cardTextWrappersm {
  & h4 {
    font-size: 20px;
  }
}
.resetBtn {
  display: flex;
  justify-content: center;
}
</style>