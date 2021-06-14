<template>
  <section>
    <div class="welcomeMsg">
      <h3 class="welcomeMsg-h3">
        Benvenuto nel miglior Team Generator che ci sia!
      </h3>
      <p class="welcomeMsg-parag">
        Premi su un giocatore per selezionarlo, non appena ne selezioni almeno
        5, avrai la possibilità di generare le squadre!
      </p>
    </div>
  </section>
</template>

<script>
export default {};
</script>


<style lang="scss" scoped>
section {
  display: flex;
  justify-content: center;
}
.welcomeMsg {
  position: relative;
  width: 80vw;
  height: fit-content;
  border-radius: 9px;
  border: solid 1px #cacaca;
  padding: 15px 5px;
  text-align: center;
  box-shadow: 0 0 10px 10px rgba(0, 0, 0, 0.1);
  &-h3 {
    font-size: 20px;
  }
  .fas {
    font-size: 20px;
    position: absolute;
    top: 10px;
    right: 10px;
    opacity: 0.5;
    cursor: pointer;
    color: rgb(196, 36, 36);

    transition: all 0.35s ease-in-out;
    outline: none;

    &:hover,
    &:focus {
      color: rgb(196, 36, 36);
      outline: none;
      background: transparent;
      border: 1px solid transparent;
      opacity: 1;
      transform: rotate(90deg);
    }
  }
}
</style>