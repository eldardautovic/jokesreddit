<template>
  <div class="footer">
    <p>
      Made with love by
      <a href="https://salesmanunknown.github.io/">Salesman</a>
    </p>
  </div>
</template>

<script>
export default {};
</script>

<style>
.footer {
  min-height: 10vh;
}

.footer p {
  display: flex;
  justify-content: center;
  align-content: center;
  margin-top: 40px;
  font-family: sans-serif;
  color: white;
}

.footer a {
  padding-left: 5px;
  text-decoration: none;
  color: currentColor;
  transition: 0.7s ease;
}

.footer a:hover {
  opacity: 0.7;
  color: ;
}
</style>