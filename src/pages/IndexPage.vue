<template>
  
  <div class="q-pa-md" style="max-width: 400px">

    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >
      <q-input
        filled
        label="ชื่อ-สกุล *"
       v-model="name"
         hint="ชื่อและนามสกุล"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'กรุณาพิมพ์ชื่อ']"
      />

      <q-input
        filled
        label="name-surname *"
       v-model="name"
         hint="name and surename"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'pleas enter ur name']"
      />


      <q-input
        filled
        type="number"
        v-model="age"
        label="你的年齡 *"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || '請輸入您的年齡',
          val => val > 0 && val < 100 || '請輸入真實年齡'
        ]"
      />


      <q-toggle v-model="accept" label="ยอมรับ" />

      <div>
        <q-btn label="ยอมรับ" type="submit" color="primary"/>
        <q-btn label="ยกเลิก" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>

  </div>
</template>

<script>
import { useQuasar } from 'quasar'
import { ref } from 'vue'

export default {
  setup () {
    const $q = useQuasar()

    const name = ref(null)
    const age = ref(null)
    const accept = ref(false)
    return {
      name,
      age,
      accept,
      onSubmit () {
        if (accept.value !== true) {
          $q.notify({
            color: 'red-5',
            textColor: 'white',
            icon: 'warning',
            message: 'คุณจำเป็นต้องยอมรับ'
          })
        }
        else {
          $q.notify({
            color: 'green-4',
            textColor: 'white',
            icon: 'cloud_done',
            message: 'ข้อมูลได้รับการยืนยัน'
          })
        }
      },
      onReset () {
        name.value = null
        age.value = null
        accept.value = false
      }
    }
  }
}
</script>