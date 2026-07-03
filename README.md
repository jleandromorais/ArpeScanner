# 🔍 ArpeScanner
 
Ferramenta de linha de comando para escaneamento e auditoria de unidades de rede, desenvolvida para o setor de Tarifas da **ARPE** (Agência Reguladora de Pernambuco).
 
## O que faz?
 
O ArpeScanner varre diretórios de rede e gera um relatório completo identificando:
 
- **Arquivos duplicados/versionados** — agrupa arquivos com nomes semelhantes (cópias, versões `_v1`, `_v2`, `_final`, etc.) e calcula o espaço desperdiçado.
- **Top 15 arquivos mais pesados** — lista os maiores consumidores de espaço no diretório escaneado.
- **Relatório em Excel** — exporta todos os resultados em um `.xlsx` organizado para análise.
## Exemplo de saída
 
```
══════════════════════════════════════════════════════════
  Espaço desperdiçado:      157.8 MB
  Grupos com versões:       23
  Excel gerado:             Z:\...\scanner_rede_20260702_094052.xlsx
══════════════════════════════════════════════════════════
```
 
## Requisitos
 
- Python 3.10+
- Dependências:
```bash
pip install openpyxl
```
 
## Como usar
 
```bash
python scanner_rede.py
```
 
O script solicita o caminho do diretório de rede a ser escaneado e gera o relatório Excel no mesmo diretório.
 
## Stack
 
- **Python** — lógica de escaneamento e agrupamento por similaridade de nomes
- **openpyxl** — geração do relatório Excel
## Contexto
 
Desenvolvido para otimizar a gestão de arquivos regulatórios no setor de Transportes/Tarifas da ARPE, onde o acúmulo de versões e cópias em unidades de rede compartilhadas gera desperdício significativo de espaço.
 
## Autor
 
**Leandro Morais** — Estagiário de Desenvolvimento, ARPE  
[GitHub](https://github.com/jleandromorais)
