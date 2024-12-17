<template>
  <ConfigProvider :locale="getAntdLocale">
    <AppProvider>
      <RouterView />
    </AppProvider>
  </ConfigProvider>
</template>

<script lang="ts" setup>
  import { ConfigProvider } from 'ant-design-vue';
  import { AppProvider } from '/@/components/Application';
  import { useTitle } from '/@/hooks/web/useTitle';
  import { useLocale } from '/@/locales/useLocale';
  import { onMounted } from 'vue';

  // support Multi-language
  const { getAntdLocale } = useLocale();

  useTitle();

  onMounted(() => {
    setTimeout(() => {
      window.parent?.postMessage({ action: 'on-code-ok' }, '*');
    }, 5000);
  });
</script>
