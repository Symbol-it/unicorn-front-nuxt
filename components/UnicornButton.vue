<template>
  <nuxt-link v-if="to" :to="to" class="button">
    <slot />
  </nuxt-link>
  <a v-else-if="href" :href="href" class="button">
    <slot />
  </a>
  <button v-else class="button">
    <slot />
  </button>
</template>
<script>
export default {
    name: 'UnicornButton',
    props: {
        to: {
            type: String,
            default: null
        },
        href: {
          type: String,
          default: ''
        },
    }
}
</script>
<style scoped>
.button {
    min-height: 50px;
    min-width: 150px;
    font-weight: 400;
    font-size: 14px;
    letter-spacing: 0.15em;
    line-height: 18px;
    background: #CFE2F3;
    border: 2px solid black;
    border-radius: 16px;
    color: black;
    text-decoration: none;
    cursor: pointer;
    transition: 0.3s;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    text-transform: uppercase;
    margin: auto;
}

.button:hover {
    background: #C9DAF8;
    border: 2px solid black;
    box-shadow: inset 1px 1px black;
}
</style>
