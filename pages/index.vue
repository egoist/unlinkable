<template>
  <div class="main">
    <GithubBadge slug="egoist/unlinkable" />
    <h1 class="title">{{ title }}</h1>
    <p class="description">{{ description }}</p>
    <textarea class="input" v-model="input" rows="5" placeholder="Type your tweet..."></textarea>
    <div class="output" v-if="output">
      <div class="link">{{ output }}</div>
      <div class="action">
        <button class="button" @click="copy">Copy</button>
      </div>
      <div class="desc">Now copy the text and post it on Twitter! <a href="https://github.com/egoist/unlinkable/blob/bb4c8880647de1a96d2f554f88aab2443615c0b1/pages/index.vue#L45" target="_blank">How does this work?</a></div>
    </div>
  </div>
</template>

<script>
import copy from 'modern-copy'
import toast from 'native-toast'
import GithubBadge from 'vue-github-badge'

export default {
  head() {
    return {
      title: this.title,
      meta: [
        {
          name: 'description',
          content: this.description
        }
      ]
    }
  },

  data() {
    return {
      title: 'Unlinkable',
      description:
        'Prevent Twitter from auto-converting URL and @mention, #hashtag into links.',
      input: ''
    }
  },

  computed: {
    output() {
      return this.input.replace(/([@#\.])/ig, '$1\u200B')
    }
  },

  methods: {
    copy() {
      copy(this.output)
      toast({
        message: 'Copied!'
      })
    }
  },

  components: {
    GithubBadge
  }
}
</script>

<style src="native-toast/dist/native-toast.css"></style>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font: 14px/1 -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen", "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue", sans-serif;
}
</style>

<style scoped>
.title {
  margin: 0;
}

.main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  margin: 0 auto;
  padding: 40px 10px;
}

.input {
  margin-top: 20px;
}

.output {
  border: 1px solid #e2e2e2;
  margin-top: 20px;
}

.output .link {
  font-size: 18px;
  background: #f9f9f9;
  padding: 10px;
}

.action {
  padding: 10px;
  border-top: 1px solid #e2e2e2;
}

.button {
  background: #e60278;
  width: 100px;
  height: 34px;
  line-height: 34px;
  color: white;
  border: none;
  font-size: 16px;
  box-shadow: inset 0 -1px rgba(64,64,64,.4);
  border-radius: 2px;
  transition: background .1s ease;
  cursor: pointer;
}

.button:hover {
  background: #fd0585;
}

.desc {
  padding: 10px;
  padding-top: 0;
  color: #999;
  font-style: italic;
}
</style>
