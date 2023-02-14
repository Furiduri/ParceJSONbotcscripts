<script setup lang="ts">
import IRowRol from "../models/IRowRol";

import Avatar from "primevue/avatar";
import AvatarGroup from "primevue/avatargroup";

defineProps<{ Rol: IRowRol }>();
</script>
<template>
    <div class="font-medium text-900 grid p-0 m-0">
        <div class="col-1 p-0">
            <Avatar size="large" class="m-0" :image="Rol.image"></Avatar>
        </div>
        <div class="col-11 p-0">
            <p class="m-0">        
            <b>{{ Rol.name }} :</b> 
            {{ Rol.ability }}</p>
        </div>
    </div>
</template>

<style scoped></style>
