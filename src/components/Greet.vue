<template>
    <v-card
            class="mx-auto"
            width="100%"
            tile
    >
            <v-row
                    align="end"
                    no-gutters
            >
                <v-col
                        align-self="start"
                        class="space-around"
                        cols="2"
                        lg="1"
                        xl="1"
                >
                    <v-avatar
                            class="profile"
                            color="grey"
                            size="132"
                            tile
                    >
                        <v-img :src="'data:image/jpg;base64,' + PhotoBase64"/>
                    </v-avatar>

                </v-col>
                <v-col align-self="start" cols="10" lg="11" xl="11">
                    <v-list-item
                            color="rgba(0, 0, 0, .4)"
                    >
                        <v-list-item-content>
                            <v-list-item-title class="title">{{SubjectObj.name}}</v-list-item-title>
                            <v-list-item-subtitle>{{SubjectObj.role}}</v-list-item-subtitle>
                        </v-list-item-content>
                    </v-list-item>
                    <br/>
                </v-col>
            </v-row>
            <v-row no-gutters>
                    <v-col cols="12">
                        <v-progress-linear
                                height="25"
                                reactive
                                :value="engagementVal*100"
                                color="blue"
                        >
                            <strong style="color: white">{{'课堂参与度:'+engagementVal*100 + '%'}}</strong>
                        </v-progress-linear>
                    </v-col>
            </v-row>
    </v-card>
</template>

<script>
    import Misc from "@/client/Misc";

    export default {
        name: "greet",
        props:{
            PhotoBase64:String,
            SubjectObj:Object
        },
        data:()=>({

        }),
        computed:{
            engagementVal:function () {
                return Misc.engagementVal(this.SubjectObj)
            }
        }
    }
</script>

<style scoped>

</style>