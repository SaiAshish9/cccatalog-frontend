<template>
  <div class="column is-2 provider-card">
    <div>
      <span class="provider-name">{{ provider.display_name }}</span>
    </div>
    <div class="provider-logo">
      <a :href="'/collections/'+provider.source_name">
        <img :alt="provider.display_name"
            :src="getProviderLogo(provider.source_name)">
      </a>
    </div>
    <div>
      <span>Collection size: {{ getProviderImageCount(provider.image_count) }} images</span>
    </div>
  </div>
</template>

<script>
import ImageProviderService from '@/api/ImageProviderService';

export default {
  name: 'collection-item',
  props: ['provider'],
  methods: {
    getProviderImageCount(imageCount) {
      return (imageCount).toLocaleString('en');
    },
    getProviderLogo(providerName) {
      const provider = ImageProviderService.getProviderInfo(providerName);
      if (provider) {
        const logo = provider.logo;
        const logoUrl = require(`@/assets/${logo}`); // eslint-disable-line global-require, import/no-dynamic-require

        return logoUrl;
      }

      return '';
    },
  },
};
</script>

<style lang="scss" scoped>
  @import "@creativecommons/vocabulary/scss/colors.scss";
  .provider-card {
    margin: 0.5em;
    border: 1px solid $color-light-gray;
  }

  .provider-name {
    font-weight: 800;
  }

  .provider-logo {
    height: 10em;
    line-height: 10em;
    white-space: nowrap;
    position: relative;

    a {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }

    img {
      width: 100%;
    }
  }
</style>
