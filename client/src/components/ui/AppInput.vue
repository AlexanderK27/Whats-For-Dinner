<template>
    <div class="input-field">
        <label v-if="label" :for="name">{{label}}</label>
        <div class="input-area">
            <input
                :type="inputType"
                :id="name"
                :placeholder="placeholder"
                :class="warning ? 'warning' : 'ok'"
                maxlength="15"
                v-model="inputValue"
                @input="$emit('input-change', inputValue)"
                @blur="$emit('input-change', inputValue)"
            />
            <i
                v-if="showPasswordIcon"
                :class="warning ? 'material-icons warning' : 'material-icons ok'"
                @click="onShowPassword"
            >{{show ? 'visibility_off' : 'visibility'}}</i>
        </div>
        <small v-if="warning">{{warning}}</small>
    </div>
</template>

<script>
export default {
    props: {
        name: { type: String, required: true },
        label: { type: String },
        type: { type: String, default: "text" },
        placeholder: { type: String },
        value: { type: String },
        warning: { type: String },
        showPasswordIcon: { type: Boolean, default: false },
    },
    data() {
        return {
            show: false,
            inputType: this.type,
            inputValue: this.value,
        };
    },
    watch: {
        value: function () {
            this.inputValue = this.value;
        },
    },
    methods: {
        onShowPassword() {
            this.inputType === "text"
                ? (this.inputType = "password")
                : (this.inputType = "text");
            this.show = !this.show;
        },
    },
};
</script>

<style lang="less" scoped>
.input-field {
    width: 100%;
    text-align: left;

    label,
    small {
        margin-left: 6px;
    }

    label {
        font-size: 14px;
        font-weight: bold;
    }

    small {
        color: @color_danger_dark;
    }

    .input-area {
        position: relative;

        input {
            box-sizing: border-box;
            width: 100%;
            padding: 10px 46px 10px 16px;
            font-family: Avenir, Helvetica, Arial, sans-serif;
            border-style: solid;
            border-radius: 8px;
            outline-color: @color_darkest;

            &.ok {
                border-color: @color_grey_9;
            }

            &.warning {
                border-color: @color_danger_dark;
                outline: none;
            }
        }

        i {
            position: absolute;
            top: 7px;
            right: 13px;
            cursor: pointer;

            &.ok {
                color: @color_firm_tertiary;
            }

            &.warning {
                color: @color_danger_dark;
            }
        }
    }
}
</style>