<template>
  <div class="column">
    <div class="card">
      <header class="card-header">
        <p class="card-header-title has-text-grey">
          {{ title }}
        </p>
      </header>
      <div class="card-content">
        <div class="content">
 <p>Job description: {{ description }}</p>



          <p>Location: {{ location }}</p>
        </div>
      </div>
      <footer class="card-footer">
        <div class="card-footer-item">
          <span>
            <slot />
          </span>
        </div>
      </footer>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Jobbo',
  props: {
    title: {
      type: String,
      required: true
    },
    location: {
      type: String,
      required: false
    },
      description: {
      type: String,
      required: false
    },
  }
}
</script>
