<template>
    <div class="flex border-b border-40">
        <div class="w-1/4 py-4">
            <slot>
                <h4 class="font-normal text-80">
                    {{ label }}
                </h4>
            </slot>
        </div>
        <div class="w-3/4 py-4">
            <slot name="value">
                <p v-if="fieldValue && !shouldDisplayAsHtml" class="text-90">
                    {{ fieldValue }}
                </p>
                <div v-else-if="fieldValue && shouldDisplayAsHtml" v-html="field.value" />
                <p v-else>
                    &mdash;
                </p>
            </slot>
        </div>
    </div>
</template>

<script>
    export default {
        name:     "SelectedPanelItem",
        props:    {
            field:     {
                type:     Object,
                required: true,
            },
            fieldName: {
                type:    String,
                default: "",
            },
        },
        computed: {
            label() {
                return this.fieldName || this.field.name
            },

            fieldValue() {
                if (
                    this.field.value === "" ||
                    this.field.value === null ||
                    this.field.value === undefined
                ) {
                    return false
                }

                if (typeof this.field["displayUsingLabels"] !== "undefined" && this.field["displayUsingLabels"] === true) {
                    return String(this.field.options.find(el => el.value === this.field.value).label)
                }

                return String(this.field.value)
            },

            shouldDisplayAsHtml() {
                return this.field.asHtml
            },
        },
    }
</script>
