<template>
  <div id="app">
    <HeaderView />
    <div class="board">
      <div class="lane">
        <h2 class="lane-title">Backlog</h2>
          <Container group-name="trello" @drag-start="handleDragStart" @drop="handleDrop">
            <Draggable v-for="card in cards.dev" :key="card.id">
              <div class="card">{{ card.text }}</div>
            </Draggable>
          </Container>
      </div>
      <div class="lane">
        <h2 class="lane-title">Dev</h2>
        <Container group-name="trello" @drag-start="handleDragStart" @drop="handleDrop">
            <Draggable v-for="card in cards.dev" :key="card.id">
              <div class="card">{{ card.text }}</div>
            </Draggable>
          </Container>
      </div>
      <div class="lane">
        <h2 class="lane-title">Testes</h2>
        <Container group-name="trello" @drag-start="handleDragStart" @drop="handleDrop">
            <Draggable v-for="card in cards.dev" :key="card.id"> 
              <div class="card">{{ card.text }}</div>
            </Draggable>
          </Container>
      </div>
      <div class="lane">
        <h2 class="lane-title">Fechado</h2>
        <Container group-name="trello" @drag-start="handleDragStart" @drop="handleDrop">
            <Draggable v-for="card in cards.dev" :key="card.id">
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
    }
  }),
  methods: {
    handleDragStart(dragResult) {
      console.log(dragResult)

    },
    handleDrop() {

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
    }

.lane {
    background: var(--color-grey);
    width: 23rem;
    height: 30rem;
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
</style>
