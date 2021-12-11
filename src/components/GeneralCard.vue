<template>
<!-- :color="color" -->
<v-card elevation="3" style="min-height: 100px">
    <v-row no-gutters>
        <v-col cols="4" :style="{minHeight: '100px'/*,border: '2px solid black'*/,display:'flex',justifyContent:'center',alignItems:'center'}">
            <div 
                :style="{
                    /*border: '2px solid black',*/ height: '70%', width:'70%', 
                    borderRadius:'50%',backgroundColor:color,display:'flex',justifyContent:'center',alignItems:'center'
                }">
                <v-icon :color="iconColor" x-large>{{ icon }}</v-icon>
            </div>
        </v-col>
        <v-col cols="8" :style="{minHeight: '100px',display:'flex',justifyContent:'center',flexDirection:'column'}">
           <p class="font-weight-medium mb-1">{{ data }}</p>
           <v-divider></v-divider>
           <div><p class="font-weight-light">{{ cardTitle }}</p></div>
        </v-col>
    </v-row>
</v-card>
</template>

<script>
export default {
    name: 'GeneralCard',
    props:{
        color: String,
        icon: String,
        iconColor:String,
        cardTitle:String,
        data: Number,
    },
    data:()=>({
        
    })
}
</script>
