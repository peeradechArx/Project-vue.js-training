<template>
  <div>
    <!-- สร้าง input field สำหรับกรอกข้อความ-->
    <input v-model="inputText" placeholder="กรอกข้อความที่นี่" />
    <p>
      : {{ inputText }}</p>
     <!-- สร้าง radio button สำหรับเลือก Yes/No โดยเก็บค่าเลือกไว้ในตัวแปร selectedOption-->
    <input type="radio" v-model="selectedOption" value="option1">
      Yes
    <input type="radio" v-model="selectedOption" value="option2">
      No
      <!-- แสดงผลข้อความที่กรอกเมื่อเลือก ปุ่ม Yes-->
    <div v-if="selectedOption === 'option1'">
       <p>
      : {{ inputText }}</p>
    </div>
    <!-- เมื่อเลือก ปุ่ม no ให้เเสดง checkbox 4 ตัวเลือก โดยเก็บค่าเลือกไว้ในตัวแปร selectedOptions และใช้ v-for ในการวนลูปแสดงตัวเลือก-->
    <div v-if="selectedOption === 'option2'">
      <label v-for="option in options" :key="option.value">
        <input type="checkbox" v-model="selectedOptions" :value="option.value">
        {{ option.label }}
      </label>
      <p v-if="selectedOptions.length > 0">: {{ selectedOptionsText }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      //แสดงผลตัวเลือกที่เลือกออกมาเป็นข้อความ
      selectedOption: 'option2',
      inputText: "",
      //ใช้ options เก็บค่า checkbox 4 ค่าไว้
      options: [
        { value: 'option1', label: 'ฟุตบอล' },
        { value: 'option2', label: 'บอลเลย์' },
        { value: 'option3', label: 'ปิงปอง' },
        { value: 'option4', label: 'เทนนิส' }
      ],
      selectedOptions: []
    };
  },
  // ใช้ computed ใช้เมื่อค่าของ selectedOptions เปลี่ยนแปลง และจะนำค่าของ selectedOptions มาหา label จาก options 
  computed: {
    selectedOptionsText() {
      return this.selectedOptions.map(option => {
        const selectedOption = this.options.find(o => o.value === option)
        return selectedOption ? selectedOption.label : ''
      }).join(', ')
    }
  }
};
</script>
