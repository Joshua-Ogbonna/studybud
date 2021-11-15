<template>
  <div class="sign-up">
    <app-header />

    <div class="main__section">
      <SideComponent />
      <div class="form__area">
        <component :is="currentComponent[currentStep].component" />
        <div class="action__button">
          <button class="next" @click="nextPage" v-show="currentStep < 2">
            Next
          </button>
          <button class="complete" v-show="currentStep === 2">
            Complete Sign up
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SideComponent from "@/components/Auth/SideComponent";
import Details from "@/components/SignUpSteps/Details";
import Choice from "@/components/SignUpSteps/Choice";
import Learner from "@/components/SignUpSteps/Learner";
import Mentor from "@/components/SignUpSteps/Mentor";

export default {
  components: {
    SideComponent,
    Details,
    Choice,
    Learner,
    Mentor,
  },
  data() {
    return {
      
      currentStep: 0,
      showComplete: false,
      showNext: true,
      choice: "mentor",
    };
  },
  methods: {
    nextPage() {
      if (this.currentStep < this.currentComponent.length - 1) {
        this.currentStep += 1;
      } else {
        this.currentStep = this.currentComponent.length - 1;
      }
    },
  },
  computed: {
    currentComponent() {
      return [
        { name: "Details", component: Details },
        { name: "Choice", component: Choice },
        {
          name: "ChoiceOption",
          component: this.choice === "learner" ? Learner : Mentor,
        },
      ];
    },
  },
};
</script>

<style scoped>
.main__section {
  display: flex;
  margin-top: 78px;
}
.form__area {
  width: 50%;
}
.action__button {
  padding: 0px 70px 30px;
}
.action__button button {
  width: 35%;
  height: 56px;
}
.action__button .prev {
  border: 1px solid #e12313;
  color: #e12313;
}
.action__button .next,
.complete {
  border: none;
  background: #0d41e1;
  color: #fff;
  border-radius: 10px;
}
@media (min-width: 320px) and (max-width: 812px) {
  .main__section {
    display: block;
    margin-top: 78px;
  }
  .form__area {
    width: 100vw;
  }
  .action__button button {
    width: 100%;
    height: 56px;
  }
  .action__button {
    padding: 0px 20px 30px;
  }
}
</style>
