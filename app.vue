
import type { LeButton } from '#build/components';
<template>
  <main class="p-10 min-h-screen">
    <div class=" flex p-2 gap-4">
      <LeButton class="bg-red-500 ">
        STANDARD
      </LeButton>
      <LeButton variant="outlined" class="  text-red-500 border-red-500 ">
        OUTLINE
      </LeButton>
      <LeButton variant="text" class=" text-red-500 rounded-full ">
        OUTLINE
      </LeButton>
    </div>
    <div class=" flex   px-10 space-x-3 ">
      <div class=" w-1/3" v-for="(i,index) in 3" :key="index">

        <LeFeatureIconCard   class=""  title="Title" content="        Lorem ipsum dolor sit, amet constur adipisicing elit. Nulla fugit quam voluptate, accusantium iure reprehenderit, corporis sint facilis ipsum cupiditate nihil aliquid nobis error possimus!" icon="uil:github"/>

      </div>
    </div>

    <div class=" flex p-2  gap-4 flex-wrap">

        <LeRadialGlowCard title="Test" content="Choose a primary and a gray color from your Tailwind CSS color palette. Components will be styled accordingly." color="purple" />

     
      </div>
  </main>
</template>
