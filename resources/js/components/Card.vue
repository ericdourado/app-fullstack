<template>
    <div class="card mb-3">
        <div class="card-header">{{titulo}}</div>

        <div class="card-body">
            <div class="col form-row">
                <slot name="conteudo"></slot>
            </div>
        </div>
        <div class="card-footer">
            <slot name="rodape"></slot>
        </div>
    </div>
</template>

<script>

export default {
    props: ['titulo']
}
</script>
