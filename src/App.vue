<template>
  <div id="app">
    <div class="conteudo">
      <form class="painel" v-if="!enviado">
        <h1>
          <i class="fa-solid fa-circle-user"></i><br />
          Registrar Reclamação
        </h1>
        <Rotulo nome="Nome">
          <input type="text" v-model="usuario.nome" placeholder="Nome" />
          <span class="icon-form"><i class="fa-solid fa-user"></i></span>
        </Rotulo>
        <Rotulo nome="E-mail">
          <input
            type="text"
            v-model.lazy.trim="usuario.email"
            placeholder="E-mail"
          />
        </Rotulo>
        <Rotulo nome="Senha">
          <input type="password" v-model="usuario.senha" />
        </Rotulo>
        <Rotulo nome="Idade">
          <!-- number só vai permitir valores number -->
          <input
            type="number"
            v-model.number="usuario.idade"
            placeholder="Idade"
          />
        </Rotulo>
        <Rotulo nome="Mensagem">
          <textarea name="" cols="30" rows="5" v-model="mensagem"></textarea>
        </Rotulo>
        <Rotulo nome="Características do Problema">
          <span class="mr-4"
            ><input
              type="checkbox"
              v-model="caracteristicas"
              value="reproduzivel"
            />
            Reproduzível</span
          >
          <span
            ><input
              type="checkbox"
              v-model="caracteristicas"
              value="intermitente"
            />
            Intermitente</span
          >
        </Rotulo>
        <Rotulo nome="Qual produto?">
          <span class="mr-4"
            ><input type="radio" value="web" v-model="produto" /> Web</span
          >
          <span class="mr-4"
            ><input type="radio" value="mobile" v-model="produto" />
            Mobile</span
          >
          <span
            ><input type="radio" value="outro" v-model="produto" /> Outro</span
          >
        </Rotulo>
        <Rotulo nome="Prioridade">
          <select v-model="prioridade">
            <option
              v-for="prioridade in prioridades"
              :value="prioridade.codigo"
              :selected="prioridade.codigo === 1"
              :key="prioridade.codigo"
            >
              {{ prioridade.codigo }} - {{ prioridade.nome }}
            </option>
          </select>
        </Rotulo>
        <Rotulo nome="Primeira Reclamação?">
          <Escolha v-model="escolha" />
        </Rotulo>
        <hr />
        <button @click.prevent="enviar">Enviar</button>
      </form>
      <div class="painel" v-else>
        <div class="cabecalho">Resultado</div>
        <Rotulo nome="Nome">
          <span>{{ usuario.nome }}</span>
        </Rotulo>
        <Rotulo nome="E-mail">
          <span>{{ usuario.email }}</span>
        </Rotulo>
        <Rotulo nome="Senha">
          <span>{{ usuario.senha }}</span>
        </Rotulo>
        <Rotulo nome="Idade">
          <span>{{ usuario.idade }}</span>
        </Rotulo>
        <Rotulo nome="Mensagem">
          <span style="white-space: pre">{{ mensagem }}</span>
        </Rotulo>
        <Rotulo nome="Características do problema">
          <span>
            <ul>
              <li v-for="c in caracteristicas" :key="c">{{ c }}</li>
            </ul>
          </span>
        </Rotulo>
        <Rotulo nome="Qual produto?">
          <span>{{ produto }}</span>
        </Rotulo>
        <Rotulo nome="Prioridade">
          <span>{{ prioridade }}</span>
        </Rotulo>
        <Rotulo nome="Primeira Reclamação?">
          <span>{{ escolha }}</span>
        </Rotulo>
      </div>
    </div>
  </div>
</template>

<script>
import Rotulo from "./components/Rotulo.vue";
import Escolha from "./components/Escolha.vue";

export default {
  name: "app",
  components: { Rotulo, Escolha },
  methods: {
    enviar() {
      this.enviado = true;
    },
  },
  data() {
    return {
      mensagem: "",
      caracteristicas: [],
      produto: "web",
      prioridade: 1,
      prioridades: [
        { codigo: 1, nome: "baixa" },
        { codigo: 2, nome: "media" },
        { codigo: 3, nome: "alta" },
      ],
      usuario: {
        nome: "",
        email: "",
        senha: "",
        idade: 25,
      },
      escolha: true,
      enviado: false,
    };
  },
};
</script>

<style>
body {
  background-color: #ececec;
  display: grid;
  grid-template-columns: repeat(12, 8.33%);
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  grid-column-start: 5;
  grid-column-end: 9;
}
.icon-form {
  display: flex;
  align-items: center;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.5;
  color: #212529;
  text-align: center;
  white-space: nowrap;
  background-color: #e9ecef;
  border: 1px solid #ced4da;
  border-radius: 0.25rem;
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
input {
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
}
.conteudo {
}
label {
  color: #fff;
  font-size: 12px;
}
.painel {
  border-radius: 3px;
  padding: 1em 2em;
  background: rgb(63, 94, 251);
  background: radial-gradient(
    circle,
    rgba(63, 94, 251, 1) 0%,
    rgba(252, 70, 107, 1) 100%
  );
}

.painel .cabecalho {
  width: 100%;
  background-color: #ddd;
  padding: 10px 0px;
  border-radius: 5px;
  font-size: 1.4rem;
}

#app form button {
  float: right;
  margin: 10px 0px;
  padding: 10px 20px;
  font-size: 1.4rem;
  border-radius: 5px;
  color: #fff;
  background-color: #2196f3;
}

#app h1 {
  font-weight: 200;
  margin: 20px;
  padding: 0;
  color: #fff;
}
</style>
