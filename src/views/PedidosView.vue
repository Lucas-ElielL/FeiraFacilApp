<script setup>
  // O aluno deverá implementar a lógica do componente.
  import { pedidos } from '@/data/pedidos'
  function qtndItens(pedido) {
    let itensTotaisPedido = 0;
    for (let i = 0; i < pedido.length; i++) {
    itensTotaisPedido += pedido[i].quantidade;
    }
    return(itensTotaisPedido)
  };
  function precoPedido(pedido) {
    let precoTotal = 0;
    for (let i = 0; i < pedido.length; i++) {
    precoTotal += pedido[i].quantidade * pedido[i].precoUnitario;
    }
    return(precoTotal)
  };
  function precoTotal(pedido) {
    let precoTotalPedido = 0;
    for (const preco of pedido) {
      precoTotalPedido += precoPedido(preco.itens);
    }
    return(precoTotalPedido)
  }
  function itensTotais(pedido) {
    let qtndItensTotais = 0;
    for (const item of pedido) {
      qtndItensTotais += qtndItens(item.itens);
    }
    return(qtndItensTotais);
  }

</script>

<template>
  <main class="container page">
    <header class="page-header">
      <h1>Resumo dos pedidos</h1>
      <p>
        Consulte os pedidos finalizados e o total vendido.
      </p>
    </header>

    <section
      class="summary-grid"
      aria-label="Resumo geral das vendas"
    >
      <article class="summary-card">
        <span>Pedidos realizados</span>

        <!-- O aluno deverá calcular este valor. -->
        <strong>{{ pedidos.length }}</strong>
      </article>

      <article class="summary-card">
        <span>Itens vendidos</span>

        <!-- O aluno deverá calcular este valor. -->
        <strong>{{ itensTotais(pedidos) }}</strong>
      </article>

      <article class="summary-card">
        <span>Total vendido</span>

        <!-- O aluno deverá calcular este valor. -->
        <strong>R${{ precoTotal(pedidos) }}</strong>
      </article>
    </section>

    <section class="card" aria-labelledby="filtro-pedidos">
      <h2 id="filtro-pedidos">Filtrar pedidos</h2>

      <div class="filter-container">
        <div class="form-group">
          <label for="filtro">
            Nome do cliente ou código do pedido
          </label>

          <input
            id="filtro"
            name="filtro"
            type="search"
            placeholder="Digite o cliente ou código"
          />
        </div>

        <button class="button button-primary" type="button">
          Filtrar
        </button>
      </div>
    </section>

    <section class="card" aria-labelledby="pedidos-realizados">
      <h2 id="pedidos-realizados">Pedidos realizados</h2>

      <!--
        O aluno deverá utilizar uma diretiva condicional para
        apresentar uma mensagem na tela quando nenhum pedido for encontrado.
      -->

      <!-- Exiba aqui uma mensagem quando nenhum pedido for encontrado -->
      <div class="table-responsive">
        <table>
          <thead>
            <tr>
              <th scope="col">Código</th>
              <th scope="col">Cliente</th>
              <th scope="col">Produtos</th>
              <th scope="col">Itens</th>
              <th scope="col">Total</th>
            </tr>
          </thead>

          <tbody>

            <ul>
              <li v-for="pedido in pedidos" :key="pedido.codigo">
                <tr>
                  <td>{{ pedido.codigo }}</td>
                  <td>{{ pedido.cliente }}</td>
                  <td>{{ pedido.itens.length }}</td>
                  <td>{{ qtndItens(pedido.itens) }}</td>
                  <td>R$ {{ precoPedido(pedido.itens).toFixed(2) }}</td>
                </tr>
              </li>
            </ul>
           <!--
              Exemplo da estrutura que deverá ser repetida pelo aluno:


            -->
          </tbody>
        </table>
      </div>
    </section>
  </main>
</template>
