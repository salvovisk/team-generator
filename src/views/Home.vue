<template>
  <!-- :style="player.selected ? 'selected' : ''" -->
  <WelcomeMsg v-show="MsgIsVisible" @close-msg="handleMsgClosing" />

  <div class="carouselCards">
    <div
      class="playerSelectorContainer"
      v-for="player in players"
      :key="player.id"
      :class="[player.selected ? 'isActive' : '', 'playerSelectorContainer']"
    >
      <div @click="toggleSelectedPlayer(player.id)" class="cardBody">
        <img :src="player.avatar" alt="operator" class="cardImg" />
        <div class="cardTextWrapper">
          <h4
            :class="[player.selected ? 'isActive-text' : '', 'cardTextTitle']"
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
      v-show="handleBtnShow()"
      @click="handleTeamGenerator"
    >
      Confirm
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
      MsgIsVisible: true,
      selectedPlayer: [],
      players: [
        {
          id: 0,
          name: "Paolo Brosio",
          avatar: require("../assets/avatar/operator1.jpeg"),
          selected: false,
        },
        {
          id: 1,
          name: "Bruno Vespa",
          avatar: require("../assets/avatar/operator2.jpeg"),
          selected: false,
        },
        {
          id: 2,
          name: "Majin Pingu",
          avatar: require("../assets/avatar/operator6.jpeg"),
          selected: false,
        },
        {
          id: 3,
          name: "Papa Ratzinger",
          avatar: require("../assets/avatar/operator3.jpeg"),
          selected: false,
        },
        {
          id: 4,
          name: "Pippo Baudo",
          avatar: require("../assets/avatar/operator4.jpeg"),
          selected: false,
        },
        {
          id: 5,
          name: "Dov'è Bugo",
          avatar: require("../assets/avatar/operator5.jpeg"),
          selected: false,
        },
        {
          id: 6,
          name: "Luca Giurato",
          avatar: require("../assets/avatar/operator1.jpeg"),
          selected: false,
        },
        {
          id: 7,
          name: "Pazzo Cane",
          avatar: require("../assets/avatar/operator7.jpeg"),
          selected: false,
        },
        {
          id: 8,
          name: "MassiCape",
          avatar: require("../assets/avatar/operator3.jpeg"),
          selected: false,
        },
        {
          id: 9,
          name: "Orietta Berti",
          avatar: require("../assets/avatar/operator2.jpeg"),
          selected: false,
        },
        {
          id: 10,
          name: "Alberto B.",
          avatar: require("../assets/avatar/operator7.jpeg"),
          selected: false,
        },
      ],
      teamsGenerated: [],
    };
  },
  methods: {
    handleMsgClosing() {
      this.MsgIsVisible = !this.MsgIsVisible;
    },
    toggleSelectedPlayer(id) {
      this.players[id].selected = !this.players[id].selected;
      this.selectedPlayer.push(this.players[id]);
    },

    handleBtnShow() {
      const selectedPlayers = this.players.filter(
        (key) => key.selected === true
      );
      if (selectedPlayers.length >= 5) {
        return true;
      }
    },
    handleTeamGenerator() {
      const selectedPlayers = this.selectedPlayer;
      const selectedPlayersNames = selectedPlayers
        .map((i) => i.name)
        .join(", ");

      const confirmMsg = `Are you sure you want to generate teams from these players: ${selectedPlayersNames}`;

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
          console.log(this.teamsGenerated);
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
          default:
            chunkArray(shuffle, 3);
        }
      }
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
</style>