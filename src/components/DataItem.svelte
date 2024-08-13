<script>
  export let title;
  export let content;
</script>

<div class="data-item">
  <div>
    <h2>{title}</h2>
  </div>
  <div>
    <p>{content}</p>
  </div>
</div>

<style>
    .data-item {
      flex: 1 0 50%;
    }
</style>
