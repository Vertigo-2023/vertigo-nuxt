<template>
  <nav class="sidebar" :class="isSidebarClosed?'close':''">
    <header>
      <div class="image-text">
        <span class="image">
          <img src="../assets/logo.png" alt="" :class="isSidebarClosed? 'close-image':'show-image'">
        </span>
      </div>
    </header>

    <div class="menu-bar">
      <p class='toggle' @click="toggleSidebar()"> > </p>
      <div class="menu">
        <ul class="menu-links">
          <li class="nav-link" v-for="question in this.questions">
            <a :href="question.id">
              <span class="text nav-text" style="white-space: pre-line">{{ question.name }}</span>
            </a>
          </li>

        </ul>
      </div>
    </div>
  </nav>
  <div class="content" :class="isSidebarClosed?'close-content':'show-content'">
    <div class="questions">
      <p style="margin-top: 25px;font-size: 45px"> {{ currentQuestion.question }}</p>
      <div class="question-options">
        <button v-for="option in currentQuestion.options"  @click="this.updateQuestion(option.option_value as number)">{{ option.name }}</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import {Question} from "~/interfaces/question";

export default defineComponent({
  name: "outil",
  data: () => {
    return {
      isSidebarClosed: false as boolean,
      currentQuestion: {} as Question,
      questions: [
        {
          id: 0,
          name: "Urgences",
          question: "Allez aux urgences vite !",
          options: [
            {
              name: "Compris !",
              option_value: 0,
            }
          ]
        },
        {
          id: 1,
          name: "Questionnaire patient",
          question: "Avez vous accès au questionnaire patient ?",
          options: [
            {
              name: "oui",
              option_value: 1,
            },
            {
              name: "non",
              option_value: 2,
            }
          ]
        },
        {
          id: 2,
          name: "Drapaux rouges",
          question: "Vérifiez les drapeaux rouges",
          options: [
            {
              name: "Un drapeau rouge présent",
              option_value: 0
            },
            {
              name: "Aucun drapeau rouge présent",
              option_value: 3
            }
          ]
        },
        {
          id: 3,
          name: "Vertige maitenant ?",
          question: "Le patient à-t-il des vertiges maitenant",
          options: [
            {
              name: "oui",
              option_value: 4
            },
            {
              name: "non",
              option_value: 5
            },
          ]
        },
        {
          id: 4,
          name: "HINTS",
          question: `Vous aurez besoin :\n- Examen neurlogique- Examen ORL- DIX et Allpike- HINTS`,
          options: [
            {
              name: "suivant",
              option_value: 6,
            }
          ]
        },
        {
          id: 6,
          name: "HINTS - confirmation",
          question: `L'un des HINTS était-il positif ?`,
          options: [
            {
              name: "oui",
              option_value: 0,
            },
            {
              name: "non",
              option_value: 9,
            }
          ]
        },
        {
          id: 5,
          name: "Nystagmus spontanné",
          question: "Le patient souffre-t-il de nystagmus spontanné ?",
          options: [
            {
              name: "Vertical",
              option_value: 4,
            },
            {
              name: "Horizonto-rotatoire",
              option_value: 7,
            },
            {
              name: "Non",
              option_value: 7
            }
          ]
        }
      ] as Question[]
    };
  },
  methods: {
    toggleSidebar() {
      this.isSidebarClosed = !this.isSidebarClosed;
      console.log(this.isSidebarClosed)
    },
    updateQuestion(idCible: number){
      this.currentQuestion = this.questions.find((question: { id: number; }) => question.id === idCible) as Question
      console.log(idCible)
    }
  },
  computed:{

  },
  mounted() {
    this.currentQuestion = this.questions.find((question: { id: number; }) => question.id == 1) as Question
  }
})
</script>

<style>
.question-options {
  display: flex;
  flex-direction: row;
  justify-content: center;
}

.question-options button {
  background-color: #31d8de;
  border: none;
  border-radius: 5px;
  width: 300px;
  padding: 7px;
  margin: 1em;
  font-size: 30px;
  color: black;
  box-shadow: 0 6px 18px -5px rgb(49, 216, 222);
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}

:root {
  /* ===== Colors ===== */
  --body-color: #e4e9f7;
  --sidebar-color: #96caff;
  --primary-color: #695cfe;
  --toggle-color: #96caff;
  --text-color: #000;

  /* ====== Transition ====== */
  --tran-03: all 0.2s ease;
  --tran-03: all 0.3s ease;
  --tran-04: all 0.3s ease;
  --tran-05: all 0.3s ease;
}

body {
  min-height: 100vh;
  background-color: var(--body-color);
  transition: var(--tran-05);
}

::selection {
  background-color: var(--primary-color);
  color: #fff;
}

/* ===== Sidebar ===== */
.sidebar {
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 250px;
  padding: 10px 14px;
  background: var(--sidebar-color);
  transition: var(--tran-05);
  z-index: 100;
}

.close {
  width: 0;
}

/* ===== Reusable code - Here ===== */
.sidebar li {
  height: 50px;
  list-style: none;
  display: flex;
  align-items: center;
  margin-top: 10px;
}

.sidebar header .image,
.sidebar .icon {
  min-width: 60px;
  border-radius: 6px;
}

.sidebar .icon {
  min-width: 60px;
  border-radius: 6px;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
}

.sidebar .text,
.sidebar .icon {
  color: var(--text-color);
  transition: var(--tran-03);
}

.sidebar .text {
  font-size: 17px;
  font-weight: 500;
  white-space: nowrap;
  opacity: 1;
}

nav .close .text {
  opacity: 0;
}

/* =========================== */

.sidebar header {
  position: relative;
}

.sidebar header .image-text {
  display: flex;
  align-items: center;
}

.sidebar header .logo-text {
  display: flex;
  flex-direction: column;
}

header .image-text .name {
  margin-top: 2px;
  font-size: 18px;
  font-weight: 600;
}

header .image-text .profession {
  font-size: 16px;
  margin-top: -2px;
  display: block;
}

.sidebar header .image {
  display: flex;
  align-items: center;
  justify-content: center;
}

.close-image {
  transform: translateX(-150%);
  transition: 0.3s;
}

.show-image {
  transform: translateX(0);
  transition: 0.3s;
}

.sidebar header .image img {
  margin-left: 45px;
  width: 120px;
  border-radius: 6px;
}

header .close {
  visibility: collapse;
}

.sidebar .toggle {
  position: absolute;
  top: 50%;
  right: -20px;
  transform: translateY(-50%) rotate(180deg);
  height: 50px;
  width: 50px;
  background-color: var(--toggle-color);
  color: var(--text-color);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 30px;
  cursor: pointer;
  transition: var(--tran-05);
}

.sidebar .toggle::after {
  background-color: red;
  border-radius: 50%;
  content: "  ";
}

body.dark .sidebar header .toggle {
  color: var(--text-color);
}

.close .toggle {
  transform: translateY(-50%) rotate(0deg);
}

.sidebar .menu {
  margin-top: 40px;
}

.sidebar li.search-box {
  border-radius: 6px;
  background-color: var(--primary-color-light);
  cursor: pointer;
  transition: var(--tran-05);
}

.sidebar li.search-box input {
  height: 100%;
  width: 100%;
  outline: none;
  border: none;
  background-color: var(--primary-color-light);
  color: var(--text-color);
  border-radius: 6px;
  font-size: 17px;
  font-weight: 500;
  transition: var(--tran-05);
}

.sidebar li a {
  list-style: none;
  height: 100%;
  background-color: transparent;
  display: flex;
  align-items: center;
  height: 100%;
  width: 100%;
  border-radius: 6px;
  text-decoration: none;
  transition: var(--tran-03);
}

.sidebar li a:hover {
  background-color: var(--primary-color);
}

.sidebar li a:hover .icon,
.sidebar li a:hover .text {
  color: var(--sidebar-color);
}

body.dark .sidebar li a:hover .icon,
body.dark .sidebar li a:hover .text {
  color: var(--text-color);
}

.sidebar .menu-bar {
  height: calc(100% - 55px);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  overflow-y: scroll;
}

.menu-bar::-webkit-scrollbar {
  display: none;
}

.sidebar .menu-bar .mode {
  border-radius: 6px;
  background-color: var(--primary-color-light);
  position: relative;
  transition: var(--tran-05);
}

.menu-bar .mode .sun-moon {
  height: 50px;
  width: 60px;
}

.mode .sun-moon i {
  position: absolute;
}

.mode .sun-moon i.sun {
  opacity: 0;
}

body.dark .mode .sun-moon i.sun {
  opacity: 1;
}

body.dark .mode .sun-moon i.moon {
  opacity: 0;
}

.home {
  position: absolute;
  top: 0;
  top: 0;
  left: 250px;
  height: 100vh;
  width: calc(100% - 250px);
  background-color: var(--body-color);
  transition: var(--tran-05);
}

.home .text {
  font-size: 30px;
  font-weight: 500;
  color: var(--text-color);
  padding: 12px 60px;
}

.sidebar.close ~ .home {
  left: 78px;
  height: 100vh;
  width: calc(100% - 78px);
}

body.dark .home .text {
  color: var(--text-color);
}

.content {
  width: auto;
  margin-top: 80px;
  margin-left: 50px;
  margin-right: 50px;
  box-shadow: 0 6px 18px -5px rgb(5, 5, 5);
}

.questions {
  margin-right: 150px;
  margin-top: 250px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
}

.close-content {
  transform: translateX(0);
  transition: 0.3s;
}

.show-content {
  transform: translateX(12%);
  transition: 0.3s;
}
</style>