<template>
  <div class="container">
    <article>
      <header>
        <div class="progress">
          <div
            class="progress-step"
            v-for="(step, index) in steps"
            :key="index"
            :class="{ active: index === startStep }"
          >
            {{ index + 1 }}
          </div>
        </div>
      </header>
      <section :class="animation">
        <h2>{{ steps[startStep].title }}</h2>
        <div class="input-fields">
          <div
            class="input-container"
            v-for="(field, index) in steps[startStep].fields"
            :key="index"
          >
            <input
              type="text"
              :class="{ 'invalid-input': !field.valid }"
              v-model="field.value"
              required
            />
            <label class="input-label">{{ field.label }}</label>
          </div>
        </div>
        <div class="buttons">
          <button v-if="startStep + 1 < steps.length - 1" @click="checkInputs">
            next
          </button>
          <button
            v-if="startStep + 1 === steps.length - 1"
            @click="checkInputs"
          >
            done
          </button>
        </div>
      </section>
    </article>
  </div>
</template>

<script>
export default {
  data() {
    return {
      animation: 'animate-in',
      startStep: 0,
      steps: [
        {
          title: 'Personal Information',
          fields: [
            {
              label: 'firstName',
              value: '',
              valid: true,
              pattern: /.+/,
            },
            {
              label: 'lastName',
              value: '',
              valid: true,
              pattern: /.+/,
            },
            {
              label: 'email',
              value: '',
              valid: true,
              pattern: /^[^\s@]+@[^\s@]+\.[^\s@]+$/,
            },
          ],
        },
        {
          title: 'Work Experience',
          fields: [
            {
              label: 'Job title',
              value: '',
              valid: true,
              pattern: /.+/,
            },
            {
              label: 'Company name',
              value: '',
              valid: true,
              pattern: /.+/,
            },
            {
              label: 'Date start',
              value: '',
              valid: true,
              pattern: /.+/,
            },
            {
              label: 'Date end',
              value: '',
              valid: true,
              pattern: /.+/,
            },
          ],
        },
        {
          title: 'Education',
          fields: [
            {
              label: 'Course name',
              value: '',
              valid: true,
              pattern: /.+/,
            },
            {
              label: 'Institution name',
              value: '',
              valid: true,
              pattern: /.+/,
            },
            {
              label: 'Date start',
              value: '',
              valid: true,
              pattern: /.+/,
            },
            {
              label: 'Date end',
              value: '',
              valid: true,
              pattern: /.+/,
            },
          ],
        },
        {
          title: 'Thank you for finishing all Information ?',
        },
      ],
    }
  },
  methods: {
    nextForm() {
      this.animation = 'animate-out'
      setTimeout(() => {
        this.animation = 'animate-in'
        this.startStep++
      }, 900)
    },
    checkInputs() {
      let valid = true

      this.steps[this.startStep].fields.forEach((field) => {
        if (!field.pattern.test(field.value)) {
          valid = false
          field.valid = false
        } else {
          field.valid = false
        }
      })
      if (valid) {
        this.nextForm()
      } else {
        this.animation = 'animate-invalid'
        setTimeout(() => {
          this.animation = ''
        }, 500)
      }
    },
  },
}
</script>

<style lang="scss" scoped>
* {
  padding: 0;
  margin: 0;
}
@mixin flexBox() {
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  @include flexBox();
  width: 100%;
  min-height: 100vh;
  background-color: lightcoral;
}
article {
  display: flex;
  margin: 10px;
  width: calc(100% - 20px);
  max-width: 720px;
  min-height: 480px;
  perspective: 1000px;
  header {
    @include flexBox();
    width: 60px;
    height: 480px;
    background: #fff;
    border-right: 2px dashed lightcoral;
    box-shadow: 0 15px 30px rgba(0, 0, 0, 0.3), 0 10px 10px rgba(0, 0, 0, 0.2);
    border-top-left-radius: 6px;
    border-bottom-left-radius: 6px;
  }
  .progress-step {
    @include flexBox();
    position: relative;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    margin-bottom: 20px;
    color: #fff;
    background-color: lightcoral;
    font-weight: bold;
    &.active {
      background: lightcoral;
      ~ .progress-step {
        color: #555;
        background-color: #ccc;
      }
      ~ .progress-step::before {
        background-color: #ccc;
      }
    }
    &::before {
      content: '';
      position: absolute;
      top: -20px;
      width: 2px;
      height: 20px;
      background-color: lightcoral;
      z-index: 10;
    }
    &:first-child::before {
      display: none;
    }
  }
  section {
    @include flexBox();
    flex-direction: column;
    width: 100%;
    background-color: #fff;
    box-shadow: 0 15px 30px rgba(0, 0, 0, 0.3), 0 10px 10px rgba(0, 0, 0, 0.2);
    border-top-right-radius: 6px;
    border-bottom-right-radius: 6px;
    h2 {
      font-size: 1.6rem;
      color: lightcoral;
      margin: 0;
      padding: 20px;
    }
    .input-fields {
      @include flexBox();
      flex-direction: column;
      width: 100%;
    }
    .input-container {
      position: relative;
      padding: 30px 20px 20px 20px;
      width: calc(100% - 40px);
      max-width: 400px;

      input {
        position: relative;
        width: 100%;
        font-size: 1.35rem;
        outline: none;
        border: none;
        border-bottom: 2px solid lightcoral;
        background: transparent;
        box-shadow: none;

        &:valid + .input-label {
          top: 10px;
          left: 20px;
          font-size: 0.7rem;
          font-weight: normal;
          color: #999;
        }
        &.invalid-input + .input-label {
          color: rgb(151, 22, 22);
        }
      }
    }
    .input-label {
      position: absolute;
      top: 32px;
      left: 20px;
      font-size: 1.35rem;
      pointer-events: none;
      transition: 0.3s ease-in-out;
    }
    .buttons {
      margin: 0;

      button {
        outline: none;
        border: none;
        color: #fff;
        background-color: lightcoral;
        font-size: 1rem;
        padding: 3px 7px;
        margin: 0;
        text-transform: uppercase;
        border-radius: 3px;
        cursor: pointer;
        transition: 0.5s ease-in;
        &:hover {
          background-color: rgb(218, 111, 111);
        }
      }
    }
  }
}
.animate-in {
  transform-origin: bottom;
  animation: in 0.7s ease-in-out;
}
.animate-out {
  animation: out 0.6s ease-in-out;
}
.animate-invalid {
  animation: invalid 0.4s ease-in-out;
}

@keyframes in {
  0% {
    opacity: 0;
    transform: rotateY(45deg);
  }
  100% {
    opacity: 1;
    transform: rotateY(0deg);
  }
}
@keyframes out {
  0% {
    transform: rotate(0deg) translateY(0px);
  }
  60% {
    transform: rotate(10deg);
  }
  100% {
    transform: translateZ(-1000px);
  }
}
@keyframes invalid {
  0% {
    transform: translateZ(0);
  }
  20% {
    transform: translateZ(40px);
  }
  40% {
    transform: translateZ(20px);
  }
  60% {
    transform: translateZ(40px);
  }
  80% {
    transform: translateZ(20px);
  }
  100% {
    transform: translateZ(0);
  }
}
</style>
