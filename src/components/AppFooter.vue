<template>
  <CFooter>
    <div>
      <span class="ms-1"
        >&copy; {{ new Date().getFullYear() }} BuscaCEP increazy</span
      >
    </div>
    <div class="ms-auto">
      <span class="me-1" target="_blank">Powered by</span>
      <a href="https://coreui.io/vue">CoreUI for Vue</a>
    </div>
  </CFooter>
</template>

<script>
export default {
  name: 'AppFooter',
}
</script>
