<template>
  <div>
    USerbar says:
    {{user.email}}
  </div>
</template>

<script>
export default {
  name: 'User',
  props: {
user: {
                type: Object,
                default: () => [],
            },
  }
}
</script>
