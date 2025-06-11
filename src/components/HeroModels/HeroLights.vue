<template>
  <TresSpotLight
      :position="[1, 1, 1.5]"
      :angle="0.25"
      :intensity="10"
      :penumbra="0.5"
  />

  <TresSpotLight
      :position="[3, 1, 1.5]"
      :angle="0.3"
      :intensity="10"
      :penumbra="0.4"
      color="#4cc9f0"
  />

  <TresSpotLight
      :position="[-1, 1, 2.5]"
      :angle="0.4"
      :intensity="20"
      :penumbra="1"
      color="#9d4edd"
  />

  <TresRectAreaLight
      color="#A259FF"
      :position="[1, 4, 4]"
      :intensity="1"
      :rotation="[-Math.PI / 5, Math.PI / 4, 0]"
      :width="10"
      :height="10"
  />

  <TresPointLight
      :position="[0, 1, 0]"
      :intensity="1"
      color="#7209b7"
  />

  <TresPointLight
      :position="[1, 2, -2]"
      :intensity="1"
      color="#0d00a4"
  />
</template>
