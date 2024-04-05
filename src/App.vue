<template>
  <div id="app">
    
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4">Formulários no Vue</h1>
        <p class="lead">Treinando a manipulação de formulários</p>
      </div>
    </div>

    <div class="container">

      <div class="row">

        <!-- formulario -->
        <div class="col-sm-6">

          <h3>Preencha abaixo</h3>

          <form @submit.prevent="enviar" @reset="resetar">

            <div class="form-group">
              <label>Nome:</label>
              <input 
                type="text"
                class="form-control"
                placeholder="Seu nome"
                v-model.lazy.trim="dev.nome">
            </div>

            <div class="form-group">
              <label>Endereço de email:</label>
              <input 
                type="email"
                class="form-control"
                placeholder="Seu email"
                v-model.lazy="dev.email">
            </div>

            <div class="form-group">
              <label>Idade:</label>
              <input 
                type="number"
                class="form-control"
                placeholder="Sua idade"
                v-model.lazy.number="dev.idade">
            </div>

            <div class="form-group">

              <p>Gênero:</p>

              <div class="form-check form-check-inline">
                <input 
                  type="radio"
                  class="form-check-input"
                  value="Masculino"
                  v-model="dev.genero">
                <label class="form-check-label">Masculino</label>
              </div>

              <div class="form-check form-check-inline">
                <input 
                  type="radio"
                  class="form-check-input"
                  value="Feminino"
                  v-model="dev.genero">
                <label class="form-check-label">Feminino</label>
              </div>

            </div>

            <div class="form-group">
              <label>Ocupação:</label>
              <select class="form-control" v-model="dev.ocupacao">
                <option value="" disabled>Selecione uma opção...</option>
                <option 
                  v-for="(ocupacao, index) in ocupacoes"
                  :key="index"
                  :value="ocupacao">
                  {{ ocupacao }}
                </option>
              </select>
            </div>  

            <div class="form-group">

              <p>Tecnologias:</p>

              <div class="form-check form-check-inline">
                <input 
                  type="checkbox"
                  class="form-check-input"
                  value="JavaScript"
                  v-model="dev.tecnologias">
                <label class="form-check-label">JavaScript</label>
              </div>

              <div class="form-check form-check-inline">
                <input 
                  type="checkbox"
                  class="form-check-input"
                  value="Vue JS"
                  v-model="dev.tecnologias">
                <label class="form-check-label">Vue JS</label>
              </div>

              <div class="form-check form-check-inline">
                <input 
                  type="checkbox"
                  class="form-check-input"
                  value="Vuex"
                  v-model="dev.tecnologias">
                <label class="form-check-label">Vuex</label>
              </div>

              <div class="form-check form-check-inline">
                <input 
                  type="checkbox"
                  class="form-check-input"
                  value="Vue Router"
                  v-model="dev.tecnologias">
                <label class="form-check-label">Vue Router</label>
              </div>

            </div>      

            <div class="form-group">
              <label>Resumo de perfil:</label>
              <textarea 
                class="form-control"
                placeholder="Conte-nos um pouco sobre você..."
                v-model.lazy="dev.biografia"></textarea>
            </div>

            <div class="form-group">
              <AppRange 
                label="Salário pretendido:"
                v-model.number="dev.salario"
                min="1000"
                max="15000"
                step="500"
                :inputClasses="{'form-range': true }"/>
            </div>

            <div class="form-group">

              <div class="form-check form-check-inline">
                <input 
                  type="checkbox"
                  class="form-check-input"
                  v-model="dev.notificacoes"
                  true-value="Sim"
                  false-value="Não">
                <label class="form-check-label">Receber notificações por email</label>
              </div>

            </div>

            <button class="btn btn-secondary" type="reset">Resetar</button>
            <button class="btn btn-success" type="submit">Enviar</button>

          </form>

        </div>

        <!-- saida -->
        <div class="col-sm-6">

          <h3>Saída</h3>

          <div class="card">

            <div class="card-header">Dados</div>

            <ul class="list-group list-group-flush">
              <li class="list-group-item"><strong>Nome:</strong> {{ dev.nome }}</li>
              <li class="list-group-item"><strong>Email:</strong> {{ dev.email }}</li>
              <li class="list-group-item"><strong>Idade:</strong> {{ dev.idade }}</li>
              <li class="list-group-item"><strong>Gênero:</strong> {{ dev.genero }}</li>
              <li class="list-group-item"><strong>Ocupação:</strong> {{ dev.ocupacao }}</li>
              <li class="list-group-item"><strong>Tecnologias:</strong> 
                <ul v-for="(tecnologia, index) in dev.tecnologias"
                  :key="index">
                  <li>{{ tecnologia }}</li>
                </ul>
              </li>
              <li class="list-group-item"><strong>Biografia:</strong> 
                <div style="white-space: pre">{{ dev.biografia }}</div>
              </li>
              <li class="list-group-item"><strong>Salário pretendido: </strong> {{ dev.salario }} </li>
              <li class="list-group-item"><strong>Receber notificações?</strong> {{ dev.notificacoes }} </li>
            </ul>

            <div class="card-header">Model</div>

            <div class="card-body">
              <pre><code>{{ dev }}</code></pre>
            </div>

          </div>

        </div>

      </div>

    </div>

  </div>
</template>

<script>

import AppRange from './components/AppRange.vue'

export default {
  components: {
    AppRange
  },
  data () {
    return {
      dev: {},
      default: {
        nome: '',
        email: '',
        idade: 24,
        biografia: 'Sou desenvolvedor desde 2023...',
        genero: 'Masculino',
        ocupacao: '',
        tecnologias: [],
        notificacoes: 'Não',
        salario: 1000
      },
      ocupacoes: [
        'Desenvolvedor Front-End (Web)',
        'Desenvolvedor Front-End (Mobile)',
        'Desenvolvedor Front-End (Web e Mobile)',
        'Desenvolvedor Back-End',
        'Desenvolvedor Full-Stack',
      ]
    }
  },
  methods: {
    enviar () {
      const formEnviado = Object.assign({}, this.dev)
      console.log('Formulário enviado', formEnviado)
    },
    resetar () {
      this.dev = Object.assign({}, this.default)
    }
  },
  created () {
    this.resetar()
    console.log('Created')
  },
  activated () {
    this.resetar()
    console.log('Activated')
  }
}
</script>

<style scoped>
  .btn {
    margin-right: 5px;
  }
</style>