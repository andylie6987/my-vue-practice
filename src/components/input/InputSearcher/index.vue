<template>
    <div :ref="`inputGroup${name}`" class="inputGroup">
        <span class="inputGroup__name" :class="{'inputGroup__name--required': required}">{{name}}</span>
        <input
            class="inputGroup__input"
            :value="value"
            @input="$emit('input', $event.target.value)"
        />
        <button class="inputGroup__search" @click="isShowDialog=true, $emit('click')">
            <img class="search__icon" src="./magnifier-simple-line-icons.svg" />
        </button>
        <div v-if="isShowDialog">
            <slot></slot>
        </div>
    </div>
</template>
<script>
import { widthMixins } from '../_inputMixins'
export default {
    mixins: [widthMixins],
    data: () => ({
        isShowDialog: false
    }),
    props: {
        name: {
            type: String,
            default: ''
        },
        width: {
            type: [String, Number],
            default: '1'
        },
        value: {
            type: [String, Number],
            default: ''
        },
        required: {
            type: Boolean,
            default: false
        }
    },
    mounted() {
        const targetWidth = this.widths[this.width]
        const inputLabel = this.$refs[`inputGroup${this.name}`]
        inputLabel.style.minWidth = targetWidth
    },
    watch: {
        value: {
            handler(newValue, oldValue) {
                if (newValue !== oldValue) {
                    this.isShowDialog = false
                }
            },
            deep: true
        }
    },
    methods: {

    }
}
</script>
<style lang="scss" scoped src="../_input.scss">
</style>