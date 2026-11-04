# Dados

Os arquivos brutos **não são versionados** (cada CSV tem centenas de milhares de linhas). Para reproduzir a análise:

1. Acesse o [Portal da Transparência](https://portaldatransparencia.gov.br) e abra a seção de **Download de dados**, em **Viagens a Serviço**.
2. Baixe o arquivo do ano desejado (a análise usa **2025**) e descompacte.
3. Coloque nesta pasta os dois arquivos usados pelo notebook:
   - `2025_Viagem.csv`
   - `2025_Passagem.csv`

Formato dos arquivos: separador `;`, codificação `cp1252` (Windows-1252) e vírgula como separador decimal. O notebook já lê nesse formato.

Para outro ano, troque `ANO` na célula de configuração do notebook e use os arquivos `{ano}_Viagem.csv` e `{ano}_Passagem.csv`.
