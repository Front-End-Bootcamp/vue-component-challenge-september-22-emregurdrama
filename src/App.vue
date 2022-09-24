<script setup>
	import {onMounted, ref } from "vue";
    import DATA from "../src/data.json";

const list = ref([])

function getGroupNames(data){
    const groupNames = data.map(person => person.group)
    const uniqueNames = [...new Set(groupNames)]
    return uniqueNames

}
function filterByGroups(data) {
   const groups = data.reduce((currentData, person) => { currentData [person.group] = []
    return currentData
 }, {})

 Object.keys(groups).forEach(group =>{
    const students = data.filter(person => person.group == group)
    console.log('students', students)
    groups[group] = students
    //list.value = students;
 } )
 return groups

}
onMounted(async () => {
    list.value = await filterByGroups(DATA);
})



const names = getGroupNames(DATA)
console.log('names', names);

const groups = filterByGroups(DATA)
console.log('groups', groups)







</script>

<template>
	<div>
        <ul>
            <li v-for="items in list">
                {{items}}
                <br>

            </li>
        </ul>
	</div>
</template>


<style scoped>

</style>
