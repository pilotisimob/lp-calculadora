<template>
  <section>
    <section class="valores">
      <div class="center" size="wide">
        <div class="pills">
          <div class="pill">
            <span class="material-symbols-outlined">location_on</span>
            <span class="pill__spacer"></span>
            <div class="pill__content">
              <p class="pill__brow">Bairro</p>
              <p class="pill__info">{{ route.query?route.query.bairro:'' }}</p>
            </div>
          </div>
          <div class="pill">
            <span class="material-symbols-outlined">bed</span>
            <span class="pill__spacer"></span>
            <div class="pill__content">
              <p class="pill__brow">Quartos</p>
              <p class="pill__info">{{ route.query?route.query.quartos:'' }}</p>
            </div>
          </div>
          <div class="pill">
            <span class="material-symbols-outlined">shower</span>
            <span class="pill__spacer"></span>
            <div class="pill__content">
              <p class="pill__brow">Suítes</p>
              <p class="pill__info">{{ route.query?route.query.suites:'' }}</p>
            </div>
          </div>
          <div class="pill">
            <span class="material-symbols-outlined">directions_car</span>
            <span class="pill__spacer"></span>
            <div class="pill__content">
              <p class="pill__brow">Vagas</p>
              <p class="pill__info">{{ route.query?route.query.vagas:'' }}</p>
            </div>
          </div>
          <div class="pill">
            <span class="material-symbols-outlined">square_foot</span>
            <span class="pill__spacer"></span>
            <div class="pill__content">
              <p class="pill__brow">Metragem</p>
              <p class="pill__info">{{ route.query?route.query.area:'' }} m²</p>
            </div>
          </div>
        </div>
      </div>
      <div class="center valores__content" size="wide">
        <div class="valor">
          <p class="valor__text">Valor sugerido</p>
          <p class="valor__number">{{ `R$ ${valor}` }}</p>
        </div>
        <div class="sugestoes">
          <p class="sugestoes__text">Outras sugestões</p>
          <div class="sugestoes__valores">
            <div class="valor valor--small">
              <p class="valor__text">Mais rápido</p>
              <p class="valor__number">{{ `R$ ${valorRapido}` }}</p>
            </div>
            <div class="sugestoes__spacer"></div>
            <div class="valor valor--small">
              <p class="valor__text">Valor máximo</p>
              <p class="valor__number">{{ `R$ ${valorMaximo}` }}</p>
            </div>
          </div>
        </div>
      </div>
      <div class="align-center">
        <botao-anuncie size="xl" :mensagem="`O valor estimado de aluguel para o seu imovel em ${route.query.bairro.toUpperCase()} de ${route.query.quartos} QUARTOS com ${route.query.suites} SUITE , ${route.query.vagas} VAGA e ${route.query.area} metros é de: R$ ${valor}`"></botao-anuncie>
      </div>
    </section>
    <section>
      <comoCalculamos />
    </section>
    <investimento-section :mosaico="false">
    </investimento-section>
  </section>
</template>

<script setup>
const route = useRoute()
let valor = 0;
if(route.query && route.query.valor) {
  valor = Number(route.query.valor).toLocaleString('pt-BR');
} 
const valorNumerico = Number(valor.replace(/\./g, '').replace(',', '.'));
const valorRapido = (valorNumerico * 0.9).toLocaleString('pt-BR', {
  style: 'decimal',
  minimumFractionDigits: 0,
  maximumFractionDigits: 0
});
const valorMaximo = (valorNumerico * 1.1).toLocaleString('pt-BR', {
  style: 'decimal',
  minimumFractionDigits: 0,
  maximumFractionDigits: 0
});

</script>

<style scoped lang="scss">
  .pills {
    gap: 20px;
    display: flex;
    flex-flow: row wrap;
    justify-content: center;
    @media (max-width: 1105px) {
      justify-content: flex-start;
      padding-inline: 24px;
    }
  }

  .pill {
    display: flex;
    flex-flow: row nowrap;
    align-items: center;
    padding: 12px 18px;
    gap: 11px;
    background-color: hsla(0, 0%, 95%, 1);
    border-radius: 36px;
    .material-symbols-outlined {
      color: var(--primary-color);
    }
  }

    .pill__spacer {
      background-color: hsla(0, 0%, 85%, 1);
      height: 100%;
      width: 1.5px;
    }

    .pill__content {
      display: flex;
      flex-direction: column;
      gap: 1px;
    }

      .pill__brow {
        font-size: .75em;
        font-weight: 300;
      }

      .pill__info {
        font-size: 1.125em;
        font-weight: 700;
      }

  .valores {
    padding-block: 86px 110px;
    @media (max-width: 1105px) {
      padding-block: 46px;
    }
  }

    .valores__content {
      padding: 64px;
      display: flex;
      flex-flow: row nowrap;
      justify-content: space-between;
      @media (max-width: 1105px) {
        flex-flow: column nowrap;
        padding: 24px;
        gap: 20px;
      }
    }

  .valor {
    display: flex;
    flex-flow: column nowrap;
    gap: 14px;
  }

    .valor__text {
      font-size: 1.875em;
      font-weight: 700;
      color: hsla(0, 0%, 21%, 1);
      @media (max-width: 1105px) {
        font-size: 1.25em;
      }
    }

    .valor__number {
      font-size: 5em;
      font-weight: 700;
      color: hsla(22, 100%, 50%, 1);
      @media (max-width: 1105px) {
        font-size: 3.375em;
      }
    }

  .valor--small {
    gap: 5px;
    .valor__text {
      font-size: 1.125em;
      font-weight: 400;
      @media (max-width: 1105px) {
        font-size: 0.75em;
      }
    }
    .valor__number {
      font-size: 2.5em;
      @media (max-width: 1105px) {
        font-size: 1.75em;
      }
    }
  }

  .sugestoes {
      display: flex;
      flex-flow: column nowrap;
      justify-content: space-between;
      @media (max-width: 1105px) {
        gap: 12px;
      }
  }

    .sugestoes__text {
      font-size: 1.25em;
      font-weight: 700;
    }

    .sugestoes__valores {
      display: flex;
      flex-flow: row nowrap;
      gap: 40px;
      @media (max-width: 1105px) {
        gap: 30px;
      }
    }

    .sugestoes__spacer {
      width: 1px;
      height: 100%;
      background-color: hsla(220, 49%, 49%, 1);
    }
</style>
