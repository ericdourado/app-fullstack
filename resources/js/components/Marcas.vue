<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">

                <!-- Inicio card de busca -->
                <card-component titulo="Marcas">
                    <template v-slot:conteudo>
                        <div class="col form-row">
                            <div class="mb-3">
                                <input-container-component titulo="ID" id="inputId" id-help="idHelp"
                                    texto-ajuda="Opcional. Informe o id da marca">
                                    <input type="number" class="form-control" id="inputId" aria-describedby="idHelp"
                                        placeholder="Id">
                                </input-container-component>
                            </div>
                            <div class="col mb-3">
                                <input-container-component titulo="Nome" id="inputNome" id-help="nomeHelp"
                                    texto-ajuda="Opcional. Informe o nome da marca">
                                    <input type="text" class="form-control" id="inputNome" aria-describedby="NomeHelp"
                                        placeholder="Nome da marca">
                                </input-container-component>
                            </div>
                        </div>
                    </template>

                    <template v-slot:rodape>
                        <button type="submit" class="btn btn-primary float-right" btn-sm>Pesquisar</button>
                    </template>
                </card-component>
                <!-- Fim card de busca -->

                <!-- Inicio card listagem marca -->
                <card-component titulo="Relação Marcas">
                    <template v-slot:conteudo>
                        <table-component></table-component>
                    </template>

                    <template v-slot:rodape>
                        <button type="button" class="btn btn-primary float-right" data-toggle="modal" data-target="#modalMarca" btn-sm>Adicionar</button>
                    </template>
                </card-component>
                <!-- Fim card listagem marca -->

            </div>
        </div>
        <modal-component id="modalMarca" titulo="Adicionar Marca">
            <template v-slot:conteudo>
                <div class="form-group">
                    <input-container-component titulo="Nome da Marca" id="novoNome" id-help="novoNomeHelp" texto-ajuda="Informe o nome da marca">
                        <input type="text" class="form-control" id="novoNome" aria-describedby="novoNomeHelp" placeholder="Nome da marca" v-model="nomeMarca">
                    </input-container-component>
                </div>

                <div class="form-group">
                    <input-container-component titulo="Imagem" id="novoImagem" id-help="novoImagemHelp" texto-ajuda="Selecione uma imagem no formato png">
                        <input type="file" class="form-control-file" id="novoImagem" aria-describedby="novoImagemHelp" placeholder="Selecione uma imagem" @change="carregarImagem($event)"> 
                    </input-container-component>
                </div>
            </template>
            <template v-slot:rodape>
                <button type="button" class="btn btn-secondary" data-dismiss="modal">Fechar</button>
                <button type="button" class="btn btn-primary" @click="salvar()">Salvar</button>
            </template>
        </modal-component>
    </div>
</template>

<script>
    export default{
        data() {
            return {
                urlBase: 'http://localhost:8000/api/v1/marca',
                nomeMarca: '',
                arquivoImagem: []
            }
        },
        methods: {
            carregarImagem(e) {
                this.arquivoImagem = e.target.files
            },
            salvar() {
                let formData = new FormData();
                formData.append('nome', this.nomeMarca)
                formData.append('imagem', this.arquivoImagem[0])
                let config = {
                    headers: {
                        'Content-Type': 'multipart/form-data',
                        'Accept': 'application/json',
                    }
                }
                axios.post(this.urlBase, formData, config)
                    .then(response => {
                        console.log(response)
                    })
                    .catch(errors => {
                        console.log(errors)
                    })
            }
        }
    }
</script>
