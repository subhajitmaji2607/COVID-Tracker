<template>
<v-container fluid>
    <v-row dense class="mt-1">
        <v-row dense class="mt-1 ml-4">
            <v-col cols="12" sm="3">
                <GeneralCard color='#D1C4E9' icon='trending_up' iconColor='#6A1B9A' cardTitle="Total Cases" :data="data.total"/> <!--deep-purple lighten-4 -->
            </v-col>
            <v-col cols="12" sm="3">
                <GeneralCard color="#BBDEFB" icon="masks" iconColor="#1565C0" cardTitle="Active Cases" :data="data.active"/> <!--blue lighten-4-->
            </v-col>
            <v-col cols="12" sm="3">
                <GeneralCard color="#C5E1A5" icon="favorite" iconColor="#1B5E20" cardTitle="Recoverd" :data="data.recoverd"/> <!--green lighten-3--->
            </v-col>
            <v-col cols="12" sm="3">
                <GeneralCard color="#EEEEEE" icon="local_florist" iconColor="#616161" cardTitle="Death" :data="data.death"/> <!--grey lighten-3-->
            </v-col>
        </v-row>
        <v-col cols="12" sm="3" class="mt-2">
            <v-select :items="items" label="Location" outlined prepend-inner-icon="location_on" menu-props="auto"></v-select>
        </v-col>
    </v-row>
</v-container>
</template>

<script>
import GeneralCard from './GeneralCard.vue'
export default {
    name: 'Body',
    components: {
        GeneralCard,
    },
    data: () => ({
        items: ['Foo', 'Bar', 'Fizz', 'Buzz'],
        data:{
            total: 5000,
            active:500,
            recoverd:4300,
            death:200
        }
    })
}
</script>
