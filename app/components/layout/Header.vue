<script setup lang="ts">
const config = useConfig();
const { page } = useContent();

const showToc = computed(() => {
  return config.value.toc.enable
    && config.value.toc.enableInMobile
    && (page.value?._path === '/' ? config.value.toc.enableInHomepage : true);
});
</script>

<template>
  <header
    class="sticky top-0 z-40 relative w-full"
    :class="{ 'lg:border-b': config.header.border }"
    :style="{'min-height': showToc ? '84px' : '56px'}"
Contenedor SVG adaptativo -->
    <div class="absolute inset-0 w-full h-full -z-[1]">
      <img 
        src="/Recurso1.svg"
        alt=""
        class="w-full h-full object-cover object-center"
        style="filter: none !important; -webkit-filter: none !important;"
      />
    </div>

    <!-- Contenido principal -->
    <div class="relative z-10 w-full h-full">
      <div
        class="flex h-14 items-center justify-between gap-2 px-4 md:px-8 w-full"
        :class="{ 'border-b lg:border-none': config.header.border, 'container max-w-screen-2xl': config.main.padded }"
      >
        <LayoutHeaderLogo class="hidden flex-1 md:flex" />
        <LayoutMobileNav />
        <LayoutHeaderLogo v-if="config.header.showTitleInMobile" class="flex md:hidden" />
        <LayoutHeaderNav class="hidden flex-1 lg:flex" />
        <div class="flex flex-1 justify-end gap-2">
          <LayoutSearchButton v-if="!config.search.inAside && config.search.style === 'input'" />
          <div class="flex">
            <LayoutSearchButton v-if="!config.search.inAside && config.search.style === 'button'" />
            <ThemePopover v-if="config.theme.customizable" />
            <DarkModeToggle v-if="config.header.darkModeToggle" />
            <NuxtLink
              v-for="(link, i) in config.header.links"
              :key="i"
              :to="link?.to"
              :target="link?.target"
            >
              <UiButton variant="ghost" size="icon" class="flex gap-2">
                <SmartIcon v-if="link?.icon" :name="link.icon" :size="18" />
              </UiButton>
            </NuxtLink>
          </div>
        </div>
      </div>
      <div v-if="showToc" class="lg:hidden w-full">
        <LayoutToc is-small />
      </div>
    </div>
  </header>
</template>

<style scoped>
/* Garantiza que el SVG cubra todo el espacio */
header {
  contain: layout paint;
}
header img[src*=".svg"] {
  filter: none !important;
  -webkit-filter: none !important;
  forced-color-adjust: none !important;
  color-rendering: initial !important;
  min-width: 100%;
  min-height: 100%;
}
</style>