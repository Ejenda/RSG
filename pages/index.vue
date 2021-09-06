<template>
  <div>
    Enter comma seperated names:
    <textarea v-model="text" class="form-textarea mt-1 block w-full"></textarea>
    <ul>
      Names:
      <li v-for="item in names" :key="item">{{ item }}</li>
    </ul>
    <p>
      I want
      <input
        class="w-fit border-gray-900 border-b form-input"
        v-model="groups"
        type="number"
      />
      groups
    </p>
    <button class="form-button" @click="makeGroups">Make groups</button>
    <div v-show="builtGroups.length > 0">
      <div v-for="(group, i) of builtGroups" :key="i">
        Group {{ i + 1 }}
        <ul class="list-number">
          <li v-for="(item, idx) of group" :key="idx">{{ item }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      text: '',
      names: [],
      groups: 1,
      builtGroups: [],
    }
  },
  watch: {
    text(val) {
      this.names = val
        .split(',')
        .map((v) => v.trim())
        .filter((v) => v)
    },
  },
  methods: {
    makeGroups() {
      const groups = this.groups
      const names = [...this.names].sort(() => (Math.random() > .5) ? 1 : -1)
      const groupSize = Math.floor(names.length / groups)
      function randChunkSplit(arr, min, max) {
        var arr = arr.slice();
        let arrs = [],
          size = 1
        while (arr.length > 0) {
          size = Math.min(max, Math.floor(Math.random() * max + min))
          arrs.push(arr.splice(0, size))
        }
        return arrs
      }
    this.builtGroups = (randChunkSplit(names, groupSize, Math.ceil(names.length / groups)))
    },
  },
}
</script>
