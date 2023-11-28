<script setup lang="ts">
import { reactive, ref, onMounted, watch, watchEffect } from 'vue';
import "../assets/theWelcome.css"
// @ts-ignore
import TestComponent from './TestComponent.vue';


const inputData = reactive({
  ID: '',
  Name: '',
  Age: '',
  index: '',
})

const TableDataSource = ref<any>([])

//reactive chỉ dùng và chuyên dụng cho object (sẽ thích hợp cho việc thao tác với object lồng object)
//ref thì nhận tất và phải .value khi lấy dữ liệu, ref có nhiều thuộc tính hơn so với reactive
//reactive và ref đều được sử dụng để theo dõi sự thay đổi khi sử dụng watch/watchEffect


let currentID = Math.random();

let b = ref(0)

const TableRef = ref(null)

const handleAddPerson = () => {
  TableDataSource.value.push({
    ID: currentID,
    Name: inputData.Name,
    Age: inputData.Age
  })

  localStorage.setItem('DataSource', JSON.stringify(TableDataSource.value))
  currentID = currentID + 1;
  inputData.Name = ''
  inputData.Age = ''
}

const handleUpdatePerson = (data: any, indexNumber:any) => {
  inputData.ID = data.ID
  inputData.Name = data.Name
  inputData.Age = data.Age
  inputData.index = indexNumber
}

const handleOnPushUpdate = () => {
  // a.value = a.value + 2

  const storedData = localStorage.getItem('DataSource')
  if (storedData !== null) {
    const newData = JSON.parse(storedData)
    newData[inputData.index as any] = {
      ID: inputData.ID,
      Name: inputData.Name,
      Age: inputData.Age
    }
    localStorage.setItem('DataSource', JSON.stringify(newData))
    TableDataSource.value = JSON.parse(localStorage.getItem('DataSource')!)
    inputData.ID = ''
    inputData.Name = ''
    inputData.Age = ''
    inputData.index = ''
  }
}

const handleDeletePerson = (data: any) => {
  TableDataSource.value.splice(data, data + 1)
  localStorage.setItem('DataSource', JSON.stringify(TableDataSource.value))
}

onMounted(() => {
  const storedData = localStorage.getItem('DataSource')
  if (storedData !== null) {
    const newData = JSON.parse(storedData)
    TableDataSource.value = newData
  }

  console.log(TableRef, "TABLEREF")
})



watch(b, ()=>{
  console.log("watch", b.value)
  console.log("watch", inputData.Name)
})

watchEffect(()=>{
  console.log("watchEffect2", inputData.Age)
})

// watch se theo doi nhung reactive o tham so dau tien, khi tham so dau tien bi thay doi no
//  se chay nhung ham` duoc viet ben trong no

// watchEfffect se chay 1 lan duy nhat sau khi render, sau do se theo doi nhung reactive ben trong
// than ham cua no





</script>

<template>
  <div>
    <TestComponent title="Person" />
    <div class="inputDiv">
      Name:
      <input v-model="inputData.Name" style="width: 70%;" />
    </div>
    <div class="inputDiv">
      Age:
      <input v-model="inputData.Age" style="width: 70%;" />
    </div>

    <div>
      <button v-if="!inputData.ID" class="buttonAdd" @click="() => { handleAddPerson() }">Add</button>
      <button v-if="inputData.ID" class="buttonUpdate" @click="() => { handleOnPushUpdate() }">Update</button>

    </div>

    <table ref="TableRef">
      <tr>
        <th>STT</th>
        <th>Name</th>
        <th>Age</th>
        <th>Function</th>
      </tr>
      <tr class="trContent" v-for="(item, index) in TableDataSource" :key="index">
        <td>{{ index + 1 }}</td>
        <td>{{ item.Name }}</td>
        <td>{{ item.Age }} </td>
        <td>
          <button class="buttonFunction" @click="() => { handleUpdatePerson(item, index) }">Edit</button>
          <button class="buttonFunction" @click="() => { handleDeletePerson(index) }">Delete</button>
        </td>
      </tr>
    </table>
  </div>
</template>
