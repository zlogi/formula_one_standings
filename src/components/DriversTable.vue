<template>
  <div class="table">
    <h1>Standings 2019</h1>
    <table class="table-border" selectable>
      <thead>
        <tr class="heading">
          <th scope="col" class="position">#</th>
          <th scope="col" class="points">Pts</th>
          <th scope="col" class="driver">Driver</th>
          <th scope="col" class="constructor">Construtor</th>
        </tr>
      </thead>
      <tbody>
        <tr
          class="table-content"
          v-for="placement in standingsDriver"
          :key="placement.position"
          @click="goToAppModal(placement)"
        >
          <td class="position">{{ placement.position }}</td>
          <td class="points">{{ placement.points }}</td>
          <td class="driver">
            {{ placement.Driver.givenName }}
            {{ placement.Driver.familyName }}
          </td>
          <td class="constructor">{{ placement.Constructors[0].name }}</td>
        </tr>
      </tbody>
    </table>
    <transition name="fade">
      <div class="modal" v-if="placement">
        <div class="modal__backdrop" @click="placement = null" />

        <div class="modal__dialog">
          <div class="modal__header">
            <slot name="header" />
            <button
              type="button"
              class="modal__close"
              @click="placement = null"
            >
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 352 512">
                <path
                  fill="currentColor"
                  d="M242.72 256l100.07-100.07c12.28-12.28 12.28-32.19 0-44.48l-22.24-22.24c-12.28-12.28-32.19-12.28-44.48 0L176 189.28 75.93 89.21c-12.28-12.28-32.19-12.28-44.48 0L9.21 111.45c-12.28 12.28-12.28 32.19 0 44.48L109.28 256 9.21 356.07c-12.28 12.28-12.28 32.19 0 44.48l22.24 22.24c12.28 12.28 32.2 12.28 44.48 0L176 322.72l100.07 100.07c12.28 12.28 32.2 12.28 44.48 0l22.24-22.24c12.28-12.28 12.28-32.19 0-44.48L242.72 256z"
                ></path>
              </svg>
            </button>
          </div>

          <div class="modal__body">
            <h1>
              {{ placement.Driver.givenName }} {{ placement.Driver.familyName }}
            </h1>
            <hr />
            <p>DoB: {{ placement.Driver.dateOfBirth }}</p>
            <p>Nationality: {{ placement.Driver.nationality }}</p>
            <p>Number: {{ placement.Driver.permanentNumber }}</p>
            <a :href="placement.Driver.url" target="_blank">{{ placement.Driver.url }}</a>
          </div>

          <div class="modal__footer">
            <slot name="footer" />
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "Table",
  props: ["standingsDriver"],
  data() {
    return {
      placement: null,
    };
  },
  methods: {
    goToAppModal(placement) {
      this.placement = placement;
    },
  },
};
</script>

<style lang="scss">
.table {
  margin-left: 100px;
}

.position,
.points,
.driver,
.constructor {
  text-align: center;
}

.position {
  background-color: black;
  color: white;
  width: 30px;
}
.points {
  width: 80px;
  background-color: rgb(236, 236, 15);
  color: black;
  border: 1px solid white;
}
.driver {
  width: 300px;
  background-color: purple;
  color: white;
  border: 1px solid white;
  cursor: pointer;
}
.constructor {
  width: 300px;
  background-color: rgb(236, 236, 15);
  color: black;
  border: 1px white solid;
}
.modal {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 9;
  overflow-x: hidden;
  overflow-y: auto;
  &__backdrop {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background-color: rgba(0, 0, 0, 0.3);
    z-index: 1;
  }
  &__dialog {
    position: relative;
    width: 600px;
    background-color: #ffffff;
    border-radius: 5px;
    margin: 50px auto;
    display: flex;
    flex-direction: column;
    z-index: 2;
    @media screen and (max-width: 992px) {
      width: 90%;
    }
  }
  &__close {
    width: 30px;
    height: 30px;
  }
  &__header {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    padding: 20px 20px 10px;
  }
  &__body {
    padding: 10px 20px 10px;
    overflow: auto;
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
  &__footer {
    padding: 10px 20px 20px;
  }
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
