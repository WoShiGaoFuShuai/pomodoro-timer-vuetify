<template>
  <v-app>
    <v-main>
      <Pomodoro-timer
        @settingsModal="settingsModalToggle"
        @sendTabs="recieveTabs"
        :updatedTimers="updatedTimers"
      />
      <Settings-modal
        :settingsModal="settingsModal"
        @closeModal="closeModal"
        :tabs="tabs"
        @submitModal="modalSubmitted($event)"
      />
    </v-main>
  </v-app>
</template>

<script>
import PomodoroTimer from "./components/Pomodoro-timer.vue";
import SettingsModal from "./components/Settings-modal.vue";

export default {
  name: "App",

  components: {
    PomodoroTimer,
    SettingsModal,
  },

  data() {
    return {
      settingsModal: false,
      tabs: [
        {
          name: "Pomodoro",
          icon: "mdi-timer-sand",
          totalSeconds: 25 * 60,
        },
        {
          name: "Short Break",
          icon: "mdi-coffee-outline",
          totalSeconds: 5 * 60,
        },
        {
          name: "Long Break",
          icon: "mdi-bed",
          totalSeconds: 10 * 60,
        },
      ],
      updatedTimers: {},
    };
  },
  methods: {
    settingsModalToggle() {
      this.settingsModal = !this.settingsModal;
    },
    closeModal() {
      this.settingsModal = false;
    },
    recieveTabs(recievedTabs) {
      this.tabs = recievedTabs;
    },
    modalSubmitted(updatedTimers) {
      this.updatedTimers = updatedTimers;
    },
  },
};
</script>

<style lang="scss"></style>
