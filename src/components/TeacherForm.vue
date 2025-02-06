<template>

    <div>
        <section>
            <h3>Añadir Profesor:</h3>
            <div><label for="">Nombre: </label><input type="text" v-model="teacher.teacherName"></div>
            <div><label for="">Apellido: </label><input type="text" v-model="teacher.lastname"></div>
            <div><label for="">DNI: </label><input type="text" v-model="teacher.dni"></div>
            <div><label for="">Asignaturas: </label><input type="text" v-model="subject"> <button @click="handleSubject">Agregar</button></div>
            <div>
                <ul>
                    <li v-for="(e, index) in teacher.subjects" :key="index">{{ e }}</li>
                </ul>
            </div>

            <input type="checkbox" v-model="teacher.doc"> Documentación entregada
            <button @click="handlerTeachers">Agregar profesor</button>
        </section>
    
        <section>
            <h3>Listado de profesores:</h3>
            <table>
                <tr>
                    <th>Nombre: </th>
                    <th>Apellido: </th>
                    <th>DNI / NIF: </th>
                    <th>Asignaturas: </th>
                    <th>Documentación entregada: </th>
                </tr>
                <tr v-for="elem in teachers" :key="elem.dni">
                    <th>{{ elem.teacherName }}</th>
                    <th>{{ elem.lastname }}</th>
                    <th>{{ elem.dni }}</th>
                    <th>
                        <ul>
                            <li v-for="(item, index) in elem.subjects" :key="index">{{ item }}</li>
                        </ul>
                    </th>
                    <th v-if="elem.doc">Entregada</th>
                    <th v-else>No entregada</th>

                </tr>
            </table>
        </section>
    </div>
</template>

<script lang="ts" setup>
    import { Ref, ref } from 'vue';
    
    interface ITeacher {
        teacherName: string, 
        lastname: string,
        dni: string, 
        subjects: Array<string>,
        doc: boolean
    }

    let teacher:Ref<ITeacher> = ref({
        teacherName: '',
        lastname: '',
        dni: '',
        subjects: [],
        doc: false
    })

    let teachers:Ref<Array<ITeacher>> = ref([])

    let subject:Ref<string> = ref('')

    const handleSubject = () => {
        teacher.value.subjects.push(subject.value)
        subject.value = ''
    }

    const handlerTeachers = () => {
        teachers.value.push({
            teacherName: teacher.value.teacherName,
            lastname: teacher.value.lastname,
            dni: teacher.value.dni,
            subjects: teacher.value.subjects,
            doc: teacher.value.doc
        })
        teacher.value.teacherName = ''
        teacher.value.lastname = ''
        teacher.value.dni = ''
        teacher.value.subjects= []
        teacher.value.doc = false
    }

</script>

<style scoped>

</style>