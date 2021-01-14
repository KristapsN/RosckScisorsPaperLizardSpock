<template>
  <div class="container">
    <div v-if="popupOpen || startPopup">
      <Popup
        :mesage="mesage"
        :description="description"
        :close="false"
        @closePopup="closePopup"
      />
    </div>
    <div class="row center-xs center-md">
      <div class="col-md-12 col-xs-12">
        <div class="mainBar">
          <div class="col-xs-4">
            <h2 class="score">Your money: {{ myScore }}€</h2>
          </div>
          <div class="col-xs-4">
          <h2 class="score">{{ oneGameResult }}</h2>
          </div>
          <div class="col-xs-4">
          <h2 class="score">Computers money: {{ opponentScore }}€</h2>
          </div>
        </div>
      </div>
    </div>
    <div class="row center-xs">
      <div class="col-md-8 col-xs-12">
        <div v-if="myCardToShow" class="singleCardWrapper">
          <OnBoardCard
            :image="cardDeck[OpponentCard -1].image"
          />
        </div>
           <div v-else class="singleCardWrapper">
          <h4 class="placeholderCards">Computer card</h4>
        </div>
      </div>
    </div>
    <div class="row center-xs ">
      <div class="col-md-8 col-xs-12">
         <div v-if="myCardToShow" class="margin--botom--40 singleCardWrapper">
          <OnBoardCard
            :image="cardDeck[myCardToShow -1].image"
          />
         </div>
        <div v-else class="singleCardWrapper margin--botom--40 ">
          <h4 class="placeholderCards">Your card</h4>
        </div>
      </div>
    </div>
    <div class="row center-md centered-xs">
      <div v-for="card in cardDeck" :key="card.id" class="col-md-2 center-md col-xs-6 center-xs " >
        <DeckCard :image="card.image" :id="card.id" @choseCard="choseCard" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import DeckCard from './components/deckCard.vue';
import OnBoardCard from './components/onBoardCard.vue';
import Popup from './components/popup.vue';

type CardDeck = {
  id: number;
  image: string;
};
type Data = {
  cardDeck: CardDeck[];
  myCardToShow: number;
  OpponentCard: number;
  sumOfCards: number;
  myScore: number;
  opponentScore: number;
  aiDatabase: number[];
  popupOpen: boolean;
  mesage: string;
  startPopup: boolean;
  description: string;
};

export default defineComponent({
  components: {
    DeckCard,
    OnBoardCard,
    Popup,
  },
  data(): Data {
    return {
      cardDeck: [
        { id: 1, image: '/img/hand-scissors-regular.9debd0a8.svg' },
        { id: 2, image: '/img/hand-paper-regular.f6299cd9.svg' },
        { id: 3, image: '/img/hand-rock-regular.c1cf6256.svg' },
        { id: 4, image: '/img/hand-lizard-regular.f09e60f9.svg' },
        { id: 5, image: '/img/hand-spock-regular.e9170004.svg' },
      ],
      myCardToShow: 0,
      OpponentCard: 0,
      sumOfCards: 0,
      myScore: 5,
      opponentScore: 5,
      aiDatabase: [1, 2, 3, 4, 5],
      popupOpen: false,
      mesage: 'Are you 18 or older?',
      startPopup: true,
      description: 'This game involves gamling, continue only if you are 18 or older!',
    };
  },
  methods: {
    closePopup() {
      this.popupOpen = false;
      this.startPopup = false;
      console.log(this.popupOpen);
      this.myScore = 5;
      this.opponentScore = 5;
      this.myCardToShow = 0;
      this.OpponentCard = 0;
    },

    choseCard(id: number) {
      this.myCardToShow = id;
      if (id > 1) {
        this.aiDatabase.push(id - 1);
      } else { this.aiDatabase.push(5); }

      this.OpponentCard = this.aiDatabase[
        Math.floor(Math.random() * this.aiDatabase.length - 1 + 1)
      ];

      this.sumOfCards = this.myCardToShow + this.OpponentCard;
      if (this.oneGameResult === 'Win') {
        this.myScore += 1;
        this.opponentScore -= 1;
      } else if (this.oneGameResult === 'Lose') {
        this.opponentScore += 1;
        this.myScore -= 1;
      }

      if (this.myScore <= 0) {
        this.popupOpen = true;
        this.mesage = 'Unfortunatly you are out of money';
        this.description = 'Would you like to have another try?';
      } else if (this.opponentScore <= 0) {
        this.popupOpen = true;
        this.mesage = 'Congratulations, you Won!';
        this.description = 'Would you like to win again?';
      }
    },
  },
  computed: {
    oneGameResult() {
      let result = '';
      switch (this.myCardToShow) {
        case 1:
          if (this.sumOfCards === 3 || this.sumOfCards === 5) {
            result = 'Win';
          } else if (this.sumOfCards === 4 || this.sumOfCards === 6) {
            result = 'Lose';
          } else {
            result = 'Tie';
          }
          break;
        case 2:
          if (this.sumOfCards === 5 || this.sumOfCards === 7) {
            result = 'Win';
          } else if (this.sumOfCards === 3 || this.sumOfCards === 6) {
            result = 'Lose';
          } else {
            result = 'Tie';
          }
          break;
        case 3:
          if (this.sumOfCards === 4 || this.sumOfCards === 7) {
            result = 'Win';
          } else if (this.sumOfCards === 5 || this.sumOfCards === 8) {
            result = 'Lose';
          } else {
            result = 'Tie';
          }
          break;
        case 4:
          if (this.sumOfCards === 9 || this.sumOfCards === 6) {
            result = 'Win';
          } else if (this.sumOfCards === 7 || this.sumOfCards === 5) {
            result = 'Lose';
          } else {
            result = 'Tie';
          }
          break;
        case 5:
          if (this.sumOfCards === 6 || this.sumOfCards === 8) {
            result = 'Win';
          } else if (this.sumOfCards === 7 || this.sumOfCards === 9) {
            result = 'Lose';
          } else {
            result = 'Tie';
          }
          break;
        default:
          result = '';
          break;
      }
      return result;
    },
  },
});
</script>

<style lang="scss" src="./style.scss"></style>
