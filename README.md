# RPA Excel Collection & Consolidation Automation (PyAutoGUI + Pandas)

Automação em Python para simular um fluxo manual em portal web: acessar o sistema, aplicar filtros (filial + período), baixar um relatório em Excel e consolidar valores por data com Pandas, gerando um CSV final para acompanhamento operacional.

> English (short): Python RPA automation using PyAutoGUI to download Excel reports from a web portal and consolidate values by date with Pandas.

---

## Principais recursos

* Automação RPA com PyAutoGUI (cliques e digitação) para navegação em portal web
* Login via variáveis de ambiente (sem credenciais no código)
* Parametrização por linha de comando:

  * período (start/end date)
  * código de filial
  * pasta de downloads
  * caminho do CSV de saída
* Aguardar download com timeout controlado
* Consolidação com Pandas:

  * leitura do Excel baixado
  * agregação por data
  * export do resumo em CSV
* Estrutura simples e direta (sem “enterprise fake”)

---

## Contexto

Em rotinas de backoffice e operações, é comum existir um processo repetitivo como:

* abrir um portal web
* realizar login
* filtrar por filial e período
* baixar relatório em Excel
* consolidar valores por data para conciliação / acompanhamento

Quando feito manualmente, esse fluxo tende a ser lento, sujeito a falhas e difícil de repetir com consistência.

Este projeto automatiza esse processo de forma simples, mantendo o foco em produtividade e padronização.

---

## Aviso importante (uso autorizado)

Este repositório é apresentado como exemplo técnico/portfólio.

* Utilize apenas ambientes e contas autorizadas
* Não publique dados reais, links internos ou credenciais
* Respeite políticas internas e LGPD
* Este projeto não deve ser utilizado em produção sem as devidas autorizações e adaptações

---

## Estrutura do projeto

```
.
├─ .gitignore
├─ LICENSE
├─ README.md
├─ main.py
└─ requirements.txt
```

---

## Requisitos

* Python 3.10+
* Ambiente com interface gráfica (GUI)
* Navegador (ex.: Google Chrome)
* Acesso ao portal web alvo

> Observação: PyAutoGUI depende de resolução/monitor e pode exigir ajustes de coordenadas.

---

## Instalação

```bash
python -m venv .venv

# Windows
.venv\Scripts\activate

# Linux / macOS
source .venv/bin/activate

pip install -r requirements.txt
```

---

## Configuração

### 1) URL do portal

Você pode definir a URL por variável de ambiente:

```bash
set PORTAL_URL=https://seu-portal.com/login
```

Ou editar diretamente no `main.py` (constante `DEFAULT_PORTAL_URL`).

### 2) Credenciais (variáveis de ambiente)

Para evitar credenciais no código, utilize variáveis de ambiente:

```bash
set PORTAL_USER=seu_usuario
set PORTAL_PASS=sua_senha
```

Se não definir, o script solicitará via prompt.

### 3) Coordenadas do PyAutoGUI (necessário ajustar)

O script usa um mapeamento de coordenadas (classe `ClickMap`) para clicar em pontos do portal.

Você deve ajustar as coordenadas conforme seu monitor/resolução e layout do portal.

Dica útil:

```python
import pyautogui as py
py.displayMousePosition()
```

---

## Execução

Exemplo de execução via linha de comando:

```bash
python main.py --start-date "2025-01-01" --end-date "2025-01-31" --branch-code 34
```

Com parâmetros adicionais:

```bash
python main.py \
  --start-date "2025-01-01" \
  --end-date "2025-01-31" \
  --branch-code 34 \
  --downloads-dir "C:\\Users\\SeuUsuario\\Downloads" \
  --output "output\\resumo.csv" \
  --wait-download-seconds 30
```

O processo executa as seguintes etapas:

* abre o portal (URL configurada)
* realiza login (variáveis de ambiente ou prompt)
* navega pelo menu e aplica filtros (filial + período)
* baixa o Excel
* lê o arquivo baixado e consolida valores por data
* salva o CSV final no caminho informado

---

## Saídas geradas

* CSV consolidado por data (ex.: `output/resumo.csv`)
* Arquivo Excel baixado permanece na pasta de downloads

---

## Sanitização de dados

Este repositório não contém dados reais.

* Credenciais não são versionadas
* Arquivos Excel baixados e outputs devem permanecer fora do Git
* Ajustes de URL e layout devem ser feitos localmente

---

## Licença

MIT
