<template lang="html">
  <div class="">
    <nav class="panel">
      <p class="panel-heading has-text-primary">
        {{ name }}
      </p>
      <div class="panel-block space"></div>
      <div class="panel-block">
        <button type="button" name="button" class="button is-info" style="width:32%; margin-right:2%">3</button>
        <button type="button" name="button" class="button is-info" style="width:32%; margin-right:2%">3</button>
        <button type="button" name="button" class="button is-info" style="width:32%">3</button>
      </div>
    </nav>
    <a href="." class="button is-light is-pulled-left	">Go back</a>
  </div>
</template>

<script>
export default {
  props : {
    name : {
      type: String
    }
  }
}
</script>

<style lang="css" scoped>
  .space{
    height: 25rem;
  }
</style>
