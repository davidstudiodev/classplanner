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

/* Estilos globales */
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

div {
    max-width: 900px;
    width: 100%;
    padding: 20px;
    background-color: #fff;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

/* Estilos de los encabezados */
h3 {
    color: #333;
    font-size: 1.5rem;
    margin-bottom: 10px;
}

/* Estilos de los formularios */
section {
    margin-bottom: 30px;
}

label {
    font-size: 1rem;
    font-weight: bold;
    margin-right: 10px;
}

input[type="text"] {
    padding: 8px;
    font-size: 1rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    width: 250px;
    margin-bottom: 15px;
}

button {
    padding: 8px 15px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s;
}

button:hover {
    background-color: #45a049;
}

/* Estilos de las listas */
ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
}

li {
    padding: 5px 0;
}

/* Estilo de la tabla */
table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
}

th, td {
    padding: 12px;
    text-align: left;
    border-bottom: 1px solid #ddd;
}

th {
    background-color: #f8f8f8;
    font-weight: bold;
}

td ul {
    padding-left: 20px;
}

input[type="checkbox"] {
    margin-right: 10px;
}

th, td {
    text-align: center;
}


</style>