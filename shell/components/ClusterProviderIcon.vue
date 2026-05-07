<script>
export default {
  props: {
    cluster: {
      type:     Object,
      required: true,
    },
    small: {
      type:    Boolean,
      default: false,
    }
  },

  computed: {
    useForIcon() {
      return !!this.cluster?.badge?.iconText;
    },
    showBorders() {
      return this.cluster?.badge?.color === 'transparent';
    },
  }
};
</script>

<template>
  <div
    v-if="cluster"
    class="cluster-icon"
    :class="{'cluster-icon-small': small}"
  >
    <div
      v-if="useForIcon"
      class="cluster-badge-logo"
      :class="{ 'cluster-icon-border': showBorders}"
      :style="{ backgroundColor: cluster.badge.color, color: cluster.badge.textColor }"
    >
      {{ cluster.badge.iconText }}
    </div>
    <!-- eslint-disable -->
    <svg
      v-else-if="cluster.isLocal && !cluster.isHarvester"
      class="cluster-local-logo"
      version="1.1"
      xmlns="http://www.w3.org/2000/svg"
      xmlns:xlink="http://www.w3.org/1999/xlink"
      viewBox="0 0 100 100"
      xml:space="preserve">
      <title>{{ t('nav.ariaLabel.clusterProvIcon', { cluster: 'local' }) }}</title>
      <!-- NQRust fleet-stack mark: control-plane bar + 3 worker nodes -->
      <rect class="rancher-icon-fill" x="14" y="18" width="72" height="12" rx="2" />
      <rect class="rancher-icon-fill" x="14" y="42" width="22" height="40" rx="2" />
      <rect class="rancher-icon-fill" x="39" y="42" width="22" height="40" rx="2" />
      <rect class="rancher-icon-fill" x="64" y="42" width="22" height="40" rx="2" />
    </svg>
    <!-- eslint-enable -->
    <img
      v-else-if="cluster.providerNavLogo"
      class="cluster-os-logo"
      :src="cluster.providerNavLogo"
      :alt="t('nav.ariaLabel.clusterProvIcon', { cluster: cluster.nameDisplay })"
    >
  </div>
</template>

<style lang="scss" scoped>
  .rancher-icon-fill {
    fill: var(--on-tertiary, var(--primary));
  }
  .cluster-icon {
    align-items: center;
    display: flex;
    height: 32px;
    justify-content: center;
    width: 42px;

    &-border {
      border: 1px solid var(--border);
      border-radius: 5px;
      color: var(--body-text) !important; // !important is needed to override the color set by the badge when there's a transparent background.
    }
  }

  .cluster-icon-small {
    height: 25px;
    width: 25px;

    .cluster-os-logo {
      width: 25px;
      height: 25px;
    }

    .cluster-badge-logo {
      width: 25px;
      height: 25px;
    }
  }

  .cluster-os-logo {
    width: 32px;
    height: 32px;
  }
  .cluster-local-logo {
    display: flex;
    width: 25px;
  }
  .cluster-badge-logo {
    min-width: 42px;
    height: 32px;
    padding: 0px 5px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 5px;
    font-weight: bold;
  }
</style>
