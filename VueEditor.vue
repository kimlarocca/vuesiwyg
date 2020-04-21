<template>
    <div class="vue-editor">
        <div class="toolbar">
            <button type="button" class="fa fa-bold" @click="bold" title="bold"/>
            <button type="button" class="fa fa-italic" @click="italic" title="italic"/>
            <button type="button" class="fa fa-underline" @click="underline" title="underline"/>
            <button type="button" class="fa fa-link" @click="link" title="insert link"/>
            <button type="button" class="fa fa-unlink" @click="unlink" title="remove link"/>
            <button type="button" class="fa fa-undo" @click="undo" title="undo"/>
            <button type="button" class="fa fa-redo" @click="redo" title="redo"/>
            <button type="button" class="fa fa-paragraph" @click="paragraph" title="insert paragraph"/>
            <button type="button" class="fa fa-align-left" @click="left" title="align left"/>
            <button type="button" class="fa fa-align-center" @click="center" title="align center"/>
            <button type="button" class="fa fa-align-right" @click="right" title="align right"/>
            <button type="button" class="fa fa-hr" @click="hr" title="insert horizontal rule"/>
        </div>
        <div
            class="editor"
            ref="editable"
            contenteditable
            v-on="listeners"
        />
    </div>
</template>

<script>
    export default {
        props: {
            value: {
                type: String,
                default: '',
            }
        },
        computed: {
            listeners () {
                return {...this.$listeners, input: this.onInput};
            }
        },
        mounted () {
            this.$refs.editable.innerHTML = this.$props.value;
        },
        methods: {
            onInput (e) {
                this.$emit('input', e.target.innerHTML);
            },
            underline () {
                document.execCommand('underline', false, '')
            },
            bold () {
                document.execCommand('bold', false, '')
            },
            italic () {
                document.execCommand('italic', false, '')
            },
            undo () {
                document.execCommand('undo', false, '')
            },
            redo () {
                document.execCommand('redo', false, '')
            },
            paragraph () {
                document.execCommand('insertParagraph',false,'')
            },
            left () {
                document.execCommand('justifyLeft',false,'')
            },
            center () {
                document.execCommand('justifyCenter',false,'')
            },
            right () {
                document.execCommand('justifyRight',false,'')
            },
            hr () {
                document.execCommand('insertHorizontalRule',false,'')
            },
            unlink () {
                document.execCommand('unlink',false,'')
            },
            link () {
                let url = prompt("Enter the URL")
                document.execCommand("createLink", false, url)
            }
        },
    };
</script>

<style lang="scss">
    .vue-editor {

        a,
        a:visited,
        a:active {
            color: darkblue;

            &:hover {
                color: darkblue;
            }
        }

        font-weight: normal;

        .toolbar {
            margin-bottom: .25rem;

            button {
                display: inline;
                width: 2rem;
                height: 2rem;
                padding: .5rem 0;
                color: white;
                background: #393939;
                border: none;
            }

            // font awesome free doesn't have an hr icon
            .fa-hr:before {
                content: "—";
            }
        }

        .editor {
            background: white;
            padding: 1rem;
            border: 1px solid #e7f5fe;
        }
    }
</style>
