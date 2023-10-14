<template>
  <div class="container">
    <div class="cookiesContent" id="cookiesPopup">
      <svg xmlns="http://www.w3.org/2000/svg" height="5em" viewBox="0 0 640 512"><path d="M64 96c0-35.3 28.7-64 64-64H512c35.3 0 64 28.7 64 64V352H512V96H128V352H64V96zM0 403.2C0 392.6 8.6 384 19.2 384H620.8c10.6 0 19.2 8.6 19.2 19.2c0 42.4-34.4 76.8-76.8 76.8H76.8C34.4 480 0 445.6 0 403.2zM288 160c0-8.8 7.2-16 16-16h32c8.8 0 16 7.2 16 16v48h48c8.8 0 16 7.2 16 16v32c0 8.8-7.2 16-16 16H352v48c0 8.8-7.2 16-16 16H304c-8.8 0-16-7.2-16-16V272H240c-8.8 0-16-7.2-16-16V224c0-8.8 7.2-16 16-16h48V160z"/></svg>
      <p>Vous êtes : </p>
      <div class="btn-container">
        <button class="medic" @click="$router.push('outil')">Professionel de santé</button>
        <button class="patient"> Patient </button>
      </div>
    </div>
  </div>
  <div class="gray"></div>
</template>

<script lang="ts">
export default defineComponent({
  name:"questions",
  data: () => {
    return{

    }
  },
  methods:{

  },
  mounted(){

  }
})
</script>

<style scoped>
body {
  font-family: "Roboto", sans-serif;
  padding: 0;
  margin: 0;
  background-color: red;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.gray{
  position: fixed;
  z-index: 2;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(25, 25, 25, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}
.cookiesContent {
  transition: 0.3s;
  z-index: 10;
  position: absolute;
  top:25%;
  left:40%;
  width: 320px;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #fff;
  color: #000;
  text-align: center;
  border-radius: 20px;
  padding: 30px;
  button.close {
    width: 30px;
    font-size: 20px;
    color: #c0c5cb;
    align-self: flex-end;
    background-color: transparent;
    border: none;
    margin-bottom: 10px;
  }
  img {
    width: 82px;
    margin-bottom: 15px;
  }
  p {
    margin-bottom: 25px;
    font-size: 18px;
  }
  button.medic {
    background-color: #31d8de;
    border: none;
    border-radius: 5px;
    width: auto;
    padding: 14px;
    font-size: 16px;
    color: black;
    box-shadow: 0 6px 18px -5px rgb(49, 216, 222);
    margin-right: 15px;
  }
  button.patient {
    background-color: #ed6755;
    border: none;
    border-radius: 5px;
    width: auto;
    padding: 14px;
    font-size: 16px;
    color: white;
    box-shadow: 0px 6px 18px -5px rgba(237, 103, 85, 1);
  }
}
.btn-container{
  display: flex;
  flex-direction: row;
  margin-bottom: 15px;
}
.slide-down{
  --size:15px;
  animation: slide-down 0.3s linear;
}
.is-medic{
  padding-top: 15px;
}
svg{
  fill:#1c71d8
}

@keyframes slide-down {
  0% {
    visibility: visible;
    height: 0;
  }

  50%{
    visibility: visible;
    height: var(--heigh);
  }

  100% {
    visibility: visible;
    height: var(--halfHeigh);
  }
}

</style>