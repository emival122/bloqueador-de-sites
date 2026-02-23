# ⚙️ Documentação Técnica

Esta documentação descreve a estrutura interna, a arquitetura e a lógica de funcionamento do sistema Bloqueador de Sites.

## 🏗️ Arquitetura do Sistema
O projeto segue uma arquitetura simples com separação entre Interface Gráfica, Lógica de Negócio e Persistência de Dados:

* **`main.py`**  
  Responsável pela interface gráfica (Tkinter), interação com o usuário, controle de eventos e chamadas das funções de bloqueio.

* **`sites.csv`**  
  Arquivo responsável por armazenar a lista de sites que podem ser bloqueados ou desbloqueados.

## 💾 Persistência de Dados
Os dados são armazenados em um arquivo CSV localizado na raiz do projeto.

* **Formato:** CSV (Comma Separated Values)
* **Coluna:** Endereço do site
* **Encoding:** Padrão UTF-8

## 📋 Fluxo das Funções

### 1. Leitura de Sites (`ver_sites`)
- Abre o arquivo `sites.csv` em modo leitura.
- Lê cada linha e exibe os sites na `Listbox` da interface.
- Caso o arquivo não exista, o sistema ignora o erro.

### 2. Escrita de Sites (`salvar_site`)
- Abre o arquivo `sites.csv` em modo de adição.
- Salva o site informado pelo usuário.
- Atualiza automaticamente a lista exibida.

### 3. Exclusão de Sites (`deletar_site`)
- Lê todos os sites do arquivo CSV.
- Remove o site selecionado.
- Sobrescreve o arquivo com a nova lista filtrada.

## 🌐 Bloqueio de Sites
O bloqueio é realizado por meio da edição do arquivo `hosts` do Windows:

* **Caminho:**  
  `C:\Windows\System32\drivers\etc\hosts`

### Processo de Bloqueio:
1. Verifica se o programa está sendo executado como administrador.
2. Gera variações do domínio (normal, www, mobile).
3. Insere redirecionamentos para `127.0.0.1`.
4. Executa o comando de limpeza de DNS (`ipconfig /flushdns`).

### Processo de Desbloqueio:
- Remove apenas as entradas correspondentes aos sites cadastrados no CSV.
- Mantém o restante do arquivo `hosts` intacto.

## 🛡️ Segurança e Permissões
- O sistema valida se o usuário possui privilégios de administrador.
- Caso não possua, o bloqueio/desbloqueio é impedido.
- O acesso ao arquivo `hosts` é verificado antes da escrita.

## 🎨 Paleta de Cores (Tema Escuro)
* **Fundo Principal:** `#0f172a`
* **Fundo Secundário:** `#020617`
* **Texto:** `#e5e7eb`
* **Azul (Ações):** `#3b82f6`
* **Verde (Sucesso):** `#22c55e`
* **Vermelho (Bloqueio/Erro):** `#ef4444`
