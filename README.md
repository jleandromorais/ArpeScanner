# ArpeScanner

Scanner de arquivos em rede para o setor de Tarifas da ARPE. Detecta duplicatas exatas, múltiplas versões de um mesmo arquivo e lista os arquivos mais pesados — tudo via terminal, com exportação opcional para Excel.

---

## O que faz

| Detecção | Como funciona |
|---|---|
| **Duplicatas** | Compara arquivos por hash SHA-256 — encontra cópias exatas mesmo com nomes diferentes |
| **Múltiplas versões** | Agrupa arquivos pelo nome base, ignorando sufixos como `(1)`, `_copia`, `_v2`, `_final`, `_old`, etc. |
| **Arquivos pesados** | Lista os N maiores arquivos da pasta varrida |

---

## Requisitos

- Python 3.8+
- `openpyxl` (necessário apenas para exportação Excel)

```bash
pip install openpyxl
```

---

## Uso

```bash
python scanner_rede.py <PASTA> [--top N] [--export]
```

### Exemplos

```bash
# Varredura básica com relatório no terminal
python scanner_rede.py "Z:\Tarifas"

# Mostrar os 20 arquivos mais pesados
python scanner_rede.py "Z:\Tarifas" --top 20

# Varredura completa + exportar para Excel
python scanner_rede.py "Z:\Tarifas" --export

# Caminho de rede (UNC)
python scanner_rede.py "\\servidor\compartilhamento\Tarifas" --export
```

### Argumentos

| Argumento | Descrição |
|---|---|
| `<PASTA>` | Caminho da pasta ou unidade de rede a varrer (obrigatório) |
| `--top N` | Quantidade de arquivos pesados a exibir (padrão: 15) |
| `--export` | Gera um arquivo `.xlsx` na pasta varrida com os resultados |

---

## Saída

### Terminal
O relatório exibe três seções coloridas:

- **Vermelho** — grupos de duplicatas com tamanho desperdiçado por grupo e total
- **Amarelo** — grupos de versões múltiplas com nome base, pasta e data de modificação
- **Azul** — ranking dos arquivos mais pesados

### Excel (com `--export`)
Gera `scanner_rede_YYYYMMDD_HHMMSS.xlsx` com quatro abas:

| Aba | Conteúdo |
|---|---|
| `Duplicados` | Grupos com hash, caminho completo e espaço desperdiçado |
| `Versões` | Grupos de versões com nome base, pasta e data de modificação |
| `Pesados` | Ranking dos arquivos mais pesados com extensão |
| `Resumo` | Totais gerais da varredura |

---

## Sufixos reconhecidos como "versão"

O scanner ignora os seguintes padrões ao agrupar versões:

`(1)` `(2)` · `- Cópia` · `_v1` `_v2` · `_old` · `_final` · `_novo` · `_revisado` · `_corrigido` · `_atualizado` · `_backup` · `_bkp` · `FINAL` · `REVISADO` · `OK` · `NOVO` · `_YYYYMMDD`

---

## Notas

- Arquivos menores que 1 KB são ignorados na busca de duplicatas.
- Arquivos inacessíveis por permissão são listados ao final do relatório, sem interromper a execução.
- O hash é calculado em blocos de 64 KB para não sobrecarregar a memória em arquivos grandes.
