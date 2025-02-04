<template>
  <button
    :class="{
      'a-button': true,
      [`a-button--${size}`]: size && size !== 'default',
      [`a-button--${type}`]: !!type,
      'a-button--text-shadow': textShadow,
      'a-button--round': round,
      'a-button--fill': fill,
      'a-button--anim': anim,
      'a-button--disabled': disabled,
      'a-button--icon': !!icon,
      'a-button--icon-leading': !!icon && hasContent && iconPosition === 'leading',
      'a-button--icon-trailing': !!icon && hasContent && iconPosition === 'trailing',
    }"
    :disabled="disabled"
  >
    <Icon v-if="icon && iconPosition === 'leading'" :icon="icon" />
    <slot></slot>
    <Icon v-if="icon && iconPosition === 'trailing'" :icon="icon" />
  </button>
</template>

<script lang="ts">
import { defineComponent, useSlots, PropType } from 'vue';
import { Icon } from '@iconify/vue';
import { ButtonType, IconPosition } from './types';

// This ui component is a button.
export default defineComponent({
  name: 'AButton',
  components: {
    Icon,
  },
  props: {
    // Style type of the button
    type: {
      type: String as PropType<ButtonType>,
      default: 'default',
    },
    // If true, a rounded border will be applied to the button
    round: {
      type: Boolean,
      default: false,
    },
    // If true, the button will perform an move up animation on hover
    anim: {
      type: Boolean,
      default: false,
    },
    // Button size
    size: {
      type: String,
      default: 'default',
    },
    // If true, the button will be disabled
    disabled: {
      type: Boolean,
      default: false,
    },
    // If true, the button will fill the parent container
    fill: {
      type: Boolean,
      default: false,
    },
    // If true, the text in the button will have be applied a text-shadow.
    textShadow: {
      type: Boolean,
      default: false,
    },
    // The icon in the button
    icon: {
      type: String,
      default: '',
    },
    // The position of the icon
    iconPosition: {
      type: String as PropType<IconPosition>,
      default: 'leading',
    },
  },
  setup() {
    const hasContent = !!useSlots().default;
    return {
      hasContent,
    };
  },
});
</script>

<style lang="scss">
.a-button {
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  position: relative;
  height: 42px;
  line-height: 30px;
  padding: 4px 20px;
  background: var(--bg);
  color: var(--primary);
  border-radius: 6px;
  box-shadow: 0px 4px 10px var(--shadow-6);
  font-size: 14px;
  font-weight: 600;
  letter-spacing: 0.05rem;
  cursor: pointer;
  border: 1px solid var(--primary);
  user-select: none;
  box-sizing: border-box;
  white-space: nowrap;
  transition: filter 100ms ease;
}
.a-button:hover {
  filter: brightness(1.1);
}
.a-button:active {
  filter: brightness(1.05);
}
.a-button.a-button--round {
  border-radius: 24px;
}
.a-button.a-button--large {
  font-size: 16px;
  line-height: 36px;
  padding: 6px 24px;
  height: 52px;
  border-radius: 8px;
}
.a-button.a-button--large.a-button--round {
  border-radius: 30px;
}
.a-button.a-button--small {
  font-size: 12px;
  line-height: 30px;
  padding: 3px 14px;
  height: 32px;
  border-radius: 5px;
}
.a-button.a-button--small.a-button--round {
  border-radius: 18px;
}
.a-button.a-button--fill {
  width: 100%;
}
.a-button.a-button--depth {
  text-shadow: 2px 2px 4px var(--shadow-12);
}
.a-button.a-button--text-shadow {
  text-shadow: 2px 2px 4px var(--shadow-12);
}
.a-button.a-button--primary {
  background: var(--primary);
  color: var(--btn);
  border: none;
}
.a-button.a-button--gradient {
  box-shadow: 0 3px 14px var(--shadow-18);
  background: linear-gradient(42deg, var(--primary), var(--secondary));
  color: var(--btn);
  border: none;
}
.a-button.a-button--gradient-reverse {
  background: linear-gradient(42deg, var(--secondary), var(--primary));
  box-shadow: 0 3px 14px var(--shadow-18);
  color: var(--btn);
  border: none;
}
.a-button.a-button--depth {
  background: linear-gradient(180deg, var(--primary-l-6) 36%, var(--primary-d-4));
  box-shadow: 0 3px 14px var(--shadow-18);
  color: var(--btn);
  border: none;
}
.a-button.a-button--primary:hover {
  filter: none;
  background: var(--primary-85);
}
.a-button.a-button--primary:active {
  filter: none;
  background: var(--primary-75);
}
.a-button.a-button--anim {
  transition: all var(--anim-duration, 200ms) ease;
}
.a-button.a-button--anim:hover {
  transform: translateY(-4px);
  box-shadow: 0 4px 10px var(--shadow-24);
}
.a-button.a-button--disabled {
  transition: none;
  border: none;
  background: var(--disabled) !important;
  color: var(--text-disabled) !important;
  box-shadow: 0 3px 12px var(--shadow-5);
  cursor: not-allowed;
}
.a-button--icon {
  display: flex;
  align-items: center;
  padding: 6px 12px;
  svg {
    font-size: 1.25em;
    flex-shrink: 0;
  }
}
.a-button--small.a-button--icon {
  padding: 4px 10px;
  svg {
    font-size: 1.125em;
  }
}
.a-button--large.a-button--icon {
  padding: 8px 15px;
  svg {
    font-size: 1.375em;
  }
}
.a-button--round.a-button--icon {
  padding: 6px 11.375px;
  svg {
    font-size: 1.375em;
  }
}
.a-button--small.a-button--round.a-button--icon {
  padding: 4px 8px;
}
.a-button--large.a-button--round.a-button--icon {
  padding: 8px 15px;
  svg {
    font-size: 1.375em;
  }
}

// leading position icon with text
.a-button--icon-leading {
  padding: 6px 18px 6px 16px;
  svg {
    margin-right: 4px;
  }
}
.a-button--small.a-button--icon-leading {
  padding: 4px 12px 4px 10px;
  svg {
    margin-right: 3px;
  }
}
.a-button--large.a-button--icon-leading {
  padding: 8px 22px 8px 18px;
  svg {
    margin-right: 6px;
  }
}
.a-button--round.a-button--icon-leading {
  padding: 6px 14px 6px 12px;
  svg {
    margin-right: 4px;
  }
}
.a-button--round.a-button--small.a-button--icon-leading {
  padding: 4px 10px 4px 8px;
  svg {
    margin-right: 3px;
  }
}
.a-button--round.a-button--large.a-button--icon-leading {
  padding: 8px 20px 8px 16px;
  svg {
    margin-right: 6px;
  }
}

// trailing position icon with text
.a-button--icon-trailing {
  padding: 6px 16px 6px 18px;
  svg {
    margin-left: 4px;
  }
}
.a-button--small.a-button--icon-trailing {
  padding: 4px 10px 4px 12px;
  svg {
    margin-left: 3px;
  }
}
.a-button--large.a-button--icon-trailing {
  padding: 8px 18px 8px 22px;
  svg {
    margin-left: 6px;
  }
}
.a-button--round.a-button--icon-trailing {
  padding: 6px 12px 6px 16px;
  svg {
    margin-left: 4px;
  }
}
.a-button--round.a-button--small.a-button--icon-trailing {
  padding: 4px 8px 4px 11px;
  svg {
    margin-left: 3px;
  }
}
.a-button--round.a-button--large.a-button--icon-trailing {
  padding: 8px 16px 8px 21px;
  svg {
    margin-left: 6px;
  }
}
</style>
