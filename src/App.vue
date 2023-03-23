<template>
  <div id="app">
    <HeaderView />
    <div class="board">
      <div class="lane">
        <h2 class="lane-title">Backlog</h2>
          <Container group-name="trello" 
          @drag-start="handleDragStart('backlog', $event)" 
          @drop="handleDrop('backlog', $event)"
          :get-child-payload="getChildPayload"
          :drop-placeholder="{className: 'placeholder'}">

            <Draggable v-for="card in cards.backlog" :key="card.id">
              <div class="card">{{ card.text }}</div>
            </Draggable>
          </Container>
      </div>
      <div class="lane">
        <h2 class="lane-title">Dev</h2>
        <Container 
        group-name="trello" 
        @drag-start="handleDragStart('dev', $event)" 
        @drop="handleDrop('dev', $event)"
        :get-child-payload="getChildPayload"
        :drop-placeholder="{className: 'placeholder'}">
            <Draggable v-for="card in cards.dev" :key="card.id">
              <div class="card">{{ card.text }}</div>
            </Draggable>
          </Container>
      </div>
      <div class="lane">
        <h2 class="lane-title">Testes</h2>
        <Container group-name="trello" 
        @drag-start="handleDragStart('testes', $event)" 
        @drop="handleDrop('testes', $event)"
        :get-child-payload="getChildPayload"
        :drop-placeholder="{className: 'placeholder'}">
            <Draggable v-for="card in cards.testes" :key="card.id"> 
              <div class="card">{{ card.text }}</div>
            </Draggable>
          </Container>
      </div>
    </div>
  </div>
  
</template>

<script>
import HeaderView from './components/HeaderView.vue';
import initialCards from './initialCards';
import { Container, Draggable } from 'vue-smooth-dnd';

export default {
  name: 'App',
  components: {
    HeaderView,
    Container,
    Draggable
  },
  data: () => ({
    cards: {
      backlog: initialCards.backlog,
      dev: initialCards.dev,
      testes: initialCards.testes,
      fechados: []
    },
    dragginCard: {
      lane: '',
      index: -1,
      cardData: {},
    }
  }),
  methods: {
    handleDragStart(lane,dragResult) {
      const { payload, isSource } = dragResult;

      if(isSource) {
        this.dragginCard = {
          lane,
          index: payload.index,
          cardData: {
            ...this.cards[lane][payload.index]
          }
        }
      }
    },
    handleDrop(lane,dropResult) {
      const {removedIndex, addedIndex} = dropResult;

      if(lane == this.dragginCard.lane && removedIndex == addedIndex) {
        return;
      }

      if(removedIndex !== null) {
        this.cards[lane].splice(removedIndex,1);
      }

      if(addedIndex !== null) {
        this.cards[lane].splice(addedIndex, 0, this.dragginCard.cardData)
      }

    },
    getChildPayload(index) {
      return {
        index,
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.board {
        display: flex;
        justify-content: flex-start;
        margin: 1.2rem 0.8rem;
        align-items: flex-start;
    }

.lane {
    background: var(--color-grey);
    width: 23rem;
    border-radius: 0.8rem;
    box-shadow: 0 0.1rem 0.2rem 0 rgba(33, 33, 33, 0.1);
    margin: 0 0.8rem;
    padding: 0. 0.7rem;
}

.lane-title {
  padding: 0.8rem 0.5rem;
  margin-bottom: 0.6rem;
}

.card {
        background: var(--color-white);
        padding: 1.4rem;
        border-radius: 0.4rem;
        box-shadow: 0 1px rgba(9, 30, 66, 0.25);
        margin-bottom: 0.8rem;
        font-size: 1.6rem;
        cursor: pointer;
    }
.placeholder {
  background: rgba(33, 33, 33, 0.08);
  border-radius: 0.4rem;
  transform: scaleY(0.86);
  transform-origin: 0% 0%;

}
</style>
