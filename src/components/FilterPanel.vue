<template>
  <div class="navigation_panel">
    <input type="text" />
    <div>
      <select name="status">
        <option value="alive">Alive</option>
        <option value="died">Died</option>
      </select>
    </div>

    <button>Применить</button>
  </div>
</template>

<script>
export default {};
</script>

<style>
.navigation_panel {
  display: flex;
  justify-content: space-between;
  margin-top: 1rem;
  padding: 1rem;
}
</style>
