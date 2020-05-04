<template>
  <div>
    <section class="nes-container">
      <section class="message-list">
        <section class="message -left">
          <i class="nes-bcrikko"></i>
          <!-- Balloon -->
          <div class="nes-balloon from-left">
            <p>Well hello traveler. How did you get in here?</p>
          </div>
          <div
            v-for="message in displayedMessages"
            :key="message"
            class="nes-balloon from-left added-messages"
          >
            <p>{{message}}</p>
          </div>
        </section>
      </section>
    </section>
    <div id="user-input" class="nes-container is-rounded">
      <a
        v-if="alSpeaking"
        class="nes-btn"
        @click="addMessage"
        v-on:keyup.space="addMessage"
      >Continue</a>
      <div v-else>
        <Location @foundForecast="displayForecast($event)" />
      </div>
    </div>
  </div>
</template>

<script>
import Location from '@/components/Location.vue'
export default {
  name: "Home",
  components: {
    Location
  },
  data () {
    return {
      messageIndex: 0,
      userResponseIndex: 0,
      userMadeSelection: false,
      messages: [
        'I am the weather wizard and can predict the future!',
        'Just allow location services to get started'
      ],
      displayedMessages: []
    }
  },
  computed: {
    alSpeaking () {
      if (this.displayedMessages.length === 2) {
        return false
      } else {
        return true
      }
    }
  },
  methods: {
    addMessage () {
      let newMessage = this.messages[this.messageIndex]
      if (newMessage) {
        this.displayedMessages.push(newMessage)
        this.messageIndex++
      }
    },
    userMakesSelection (key) {
      this.displayedUserResponses.push(this.userResponses.weather[key])
      this.userResponseIndex++
    },
    displayForecast (forecast) {
      console.log("hello")
      console.log(forecast)
    }
  }
};
</script>
<style>
.added-messages {
  margin-left: 130px;
}
.nes-balloon p {
  overflow: hidden; /* Ensures the content is not revealed until the animation */
  border-right: 0.15em solid black; /* The typwriter cursor */
  white-space: nowrap; /* Keeps the content on a single line */
  margin: 0 auto; /* Gives that scrolling effect as the typing happens */
  /* letter-spacing: 0.15em; Adjust as needed */
  animation: typing 3.5s steps(30, end), blink-caret 0.5s step-end infinite;
  word-wrap: break-word;
}
.nes-bcrikko {
  height: 50px;
  margin-right: 2em;
}
#user-input {
  margin-top: 30px;
}
.selection {
  padding: 0;
  border: none;
  background: none;
}
/* The typing effect */
@keyframes typing {
  from {
    width: 0;
  }
  to {
    width: 100%;
  }
}

/* The typewriter cursor effect */
@keyframes blink-caret {
  from,
  to {
    border-color: transparent;
  }
  50% {
    border-color: black;
  }
}
</style>
