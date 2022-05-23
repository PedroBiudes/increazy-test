<template>
  <CDropdown variant="nav-item">
    <CDropdownToggle placement="bottom-end" class="py-0" :caret="false">
      Olá, Joaquim
      <CAvatar :src="avatar" size="md" />
    </CDropdownToggle>
  </CDropdown>
</template>

<script>
import avatar from '@/assets/images/avatars/2.jpg'
export default {
  name: 'AppHeaderDropdownAccnt',
  setup() {
    return {
      avatar: avatar,
      itemsCount: 42,
    }
  },
}
</script>
