<template>
  <div class="page__buy-car">
    <h1>buy car list here</h1>

    <h2>links</h2>
    <pre>
      <nuxt-link to="/">home page</nuxt-link><br />
      <nuxt-link to="/buy-car">/buy-car</nuxt-link><br />
      <nuxt-link to="/buy-car?a=b">/buy-car?a=b</nuxt-link><br />
      <nuxt-link to="/buy-car/audi">/buy-car/audi</nuxt-link><br />
      <nuxt-link to="/buy-car/audi?a=b">/buy-car/audi?a=b</nuxt-link><br />


      anchor<br />
      <a href="/buy-car?a=b">/buy-car?a=b</a><br />
      <a href="/buy-car/audi?a=b">/buy-car/audi?a=b</a><br />
    </pre>

    <label>
      <input type="input" v-model="inputValue" />
    </label>

    <h2>$data</h2>
    <pre><code>{{ { ...$data, logs: undefined } }}</code></pre>

    <h2>list</h2>
    <pre><code>{{ list }}</code></pre>

    <h2>logs</h2>
    <pre><code>
      <ul>
        <li v-for="(logItem, i) in logs" :key="i">[{{ logItem.date }}] @ {{ logItem.client ? 'CLIENT' : 'SERVER' }} {{ logItem.str }}</li>
      </ul>
    </code></pre>
  </div>
</template>
<script>
const logs = []

function getDate() {
  const d = new Date()

  return d.toTimeString()
}

function log(str) {
  console.log(`[${process.client ? 'CLIENT' : 'SERVER'}] ${str}`)

  logs.push({
    str,
    date: getDate(),
    client: process.client,
  })
}

export default {
  name: 'newCarList',
  key: 'new-car-list',
  watchParam: false,
  data() {
    log('data()')
    console.warn(this, this.$data)

    // if (typeof this.$data !== 'undefined') {
    //   return this.$data
    // }

    return {
      asyncData: 0,
      fetch: 0,
      created: 0,
      mounted: 0,
      list: {},

      inputValue: '123',

      logs,
    }
  },
  asyncData() {
    log('asyncData')

    return {
      asyncData: getDate(),
    }
  },
  fetch() {
    log('fetch')

    this.fetch = getDate()
  },
  created() {
    log('created')
  },
  mounted() {
    log('mounted')

    this.mounted = getDate()
  },
  destroyed() {
    log('destroyed')
  },
}
</script>
