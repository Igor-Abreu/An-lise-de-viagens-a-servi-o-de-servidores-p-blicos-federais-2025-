# Análise de viagens a serviço de servidores públicos federais (2025)

Análise exploratória, em Python, de mais de 800 mil viagens a serviço registradas no [Portal da Transparência](https://portaldatransparencia.gov.br) (CGU). O projeto limpa os dados, cria variáveis de gasto e duração e responde a quatro perguntas sobre quem viaja, quanto cada órgão e cargo gasta e como isso varia ao longo do ano.

## Perguntas

1. Qual a proporção de viagens por cargo?
2. Qual a despesa média por viagem em cada órgão solicitante?
3. Quais cargos têm despesa média por viagem acima da média geral?
4. Como o número de viagens e os gastos variam ao longo do ano, e a duração da viagem explica o custo?

## Alguns resultados

Números da extração de 2025 usada na análise (o Portal atualiza os arquivos, então valores atuais podem diferir):

- **814.395 viagens** e 419.403 registros de passagens.
- **37,61%** das viagens não têm cargo informado e **14,00%** estão sob sigilo: mais da metade do total, o que limita a análise por cargo.
- A diária média é de **R$ 1.988,82** e a passagem média, **R$ 1.109,15**. A mediana de passagens é **R$ 0**, ou seja, a maioria das viagens não tem passagem e poucas viagens caras puxam a média.
- Em despesa total, os maiores órgãos são o Ministério da Justiça e Segurança Pública (unidades com vínculo direto), com **R$ 444,0 milhões**, a Polícia Federal, com **R$ 258,0 milhões**, e o Comando da Aeronáutica, com **R$ 169,1 milhões**.

O notebook gera os demais achados automaticamente (seção 5) e salva os gráficos em `images/`.

![Proporção de viagens por cargo](images/01_proporcao_cargos.png)
![Despesa média por órgão](images/02_despesa_media_orgao.png)
![Evolução mensal](images/04_evolucao_mensal.png)

## Decisões metodológicas

- **Privacidade:** as colunas `nome` e `cpf_viajante` não são carregadas. A análise é agregada e não identifica pessoas.
- **Despesa total** = diárias + passagens + outros gastos. É um valor bruto: devoluções não são descontadas (o notebook mostra quanto elas representam).
- **Dias de viagem** contam o dia de partida e o de retorno.
- **Rankings de média** só incluem órgãos e cargos com 30 viagens ou mais (`MIN_VIAGENS`), para evitar médias instáveis. As tabelas trazem também a mediana, por causa da assimetria dos valores.
- O gráfico de dispersão usa uma amostra de 20 mil viagens e escala logarítmica, já que 800 mil pontos não são legíveis.

## Limitações

- Cargos "Não informado" e "Informações protegidas por sigilo" concentram a maior parte das viagens.
- Não há distinção entre viagens nacionais e internacionais.
- A análise é descritiva: correlação entre duração e custo não implica causalidade.

## Como rodar

```bash
git clone <url-do-repositorio>
cd analise-viagens-servidores-2025
python -m venv .venv && source .venv/bin/activate   # no Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

1. Baixe os CSVs conforme [`data/README.md`](data/README.md).
2. Abra o notebook com `jupyter notebook notebooks/analise_viagens_2025.ipynb`.
3. Execute todas as células. Para outro ano ou outro mínimo de viagens, altere `ANO` e `MIN_VIAGENS` na primeira célula.

**No Google Colab:** envie os CSVs para o Drive e descomente, na célula de configuração, as linhas que montam o Drive e definem `DATA_DIR`.

## Estrutura

```
├── README.md
├── requirements.txt
├── notebooks/
│   └── analise_viagens_2025.ipynb
├── data/
│   └── README.md          # como obter os CSVs (não versionados)
└── images/                # gráficos gerados pelo notebook
```

## Tecnologias

Python, pandas, matplotlib e Jupyter.
