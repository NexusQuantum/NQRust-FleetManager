<script>
import { abbreviateClusterName } from '@shell/utils/cluster';

export default {
  props: {
    cluster: {
      type:     Object,
      required: true,
    },
    routeCombo: {
      type:    Boolean,
      default: false
    },
  },
  computed: {
    isEnabled() {
      return !!this.cluster?.ready;
    },
    showLocalIcon() {
      if (this.cluster.isLocal && this.cluster.removePreviewColor) {
        return true;
      }

      return this.cluster.isLocal && !this.cluster.isHarvester && !this.cluster.badge?.iconText;
    },

    customColor() {
      return this.cluster.iconColor || '';
    },
  },

  methods: {
    smallIdentifier(input) {
      if (this.cluster.badge?.iconText) {
        return this.cluster.badge?.iconText;
      }

      if (this.cluster.isLocal && !this.cluster.badge?.iconText) {
        return undefined;
      }

      return abbreviateClusterName(input);
    }
  }
};
</script>

<template>
  <div
    v-if="cluster"
    class="cluster-icon-menu"
  >
    <div
      class="cluster-badge-logo"
      :class="{ 'disabled': !isEnabled }"
    >
      <span
        v-if="!showLocalIcon"
        class="cluster-badge-logo-text"
      >
        {{ smallIdentifier(cluster.label) }}
      </span>
      <span
        class="custom-color-decoration"
        :style="{'background': customColor}"
      />
      <svg
        v-if="showLocalIcon"
        class="cluster-local-logo"
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        viewBox="0 0 100 100"
        xml:space="preserve"
      >
        <title>{{ t('nav.ariaLabel.localClusterIcon') }}</title>
        <!-- NQRust fleet-stack mark: control-plane bar + 3 worker nodes -->
        <rect class="rancher-icon-fill" x="14" y="18" width="72" height="12" rx="2" />
        <rect class="rancher-icon-fill" x="14" y="42" width="22" height="40" rx="2" />
        <rect class="rancher-icon-fill" x="39" y="42" width="22" height="40" rx="2" />
        <rect class="rancher-icon-fill" x="64" y="42" width="22" height="40" rx="2" />
      </svg>
    </div>
    <i
      v-if="!routeCombo && cluster.pinned"
      class="icon icon-pin cluster-pin-icon"
      :alt="t('nav.ariaLabel.pinCluster', { cluster: cluster.nameDisplay })"
    />
    <i
      v-else-if="routeCombo"
      class="icon icon-keyboard_tab key-combo-icon"
      :alt="t('nav.ariaLabel.clusterIconKeyCombo')"
    />
  </div>
</template>

<style lang="scss" scoped>
  .rancher-icon-fill {
    fill: var(--on-tertiary, var(--primary));
  }

  .cluster-icon-menu {
    position: relative;
    align-items: center;
    display: flex;
    height: 32px;
    justify-content: center;
    width: 42px;
  }
  .cluster-pin-icon {
    position: absolute;
    top: -6px;
    right: -7px;
    font-size: 14px;
    transform: scaleX(-1);
    color: var(--body-text);
  }
  .key-combo-icon {
    position: absolute;
    top: -7px;
    right: -8px;
    font-size: 14px;
    color: var(--body-text);
    background-color: #dddee6;
    padding: 2px;
    border-radius: 2px;
  }

  .cluster-local-logo {
    width: 20px;
  }

  .cluster-badge-logo {
    width: 42px;
    height: 32px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--default-active-text);
    font-weight: bold;
    background: var(--nav-icon-badge-bg);
    border: 1px solid var(--border);
    border-radius: 5px;
    font-size: 12px;
    text-transform: uppercase;

    .custom-color-decoration {
      height: 4px;
      width: 100%;
      margin: 0 auto;
      position: absolute;
      bottom: 0px;
      border-radius: 0px 0px 5px 5px;
    }

    &.disabled {
      color: var(--muted);
    }
  }
</style>

<style lang="scss">
  .theme-dark .key-combo-icon  {
    color: var(--body-bg);
  }
</style>
