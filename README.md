

#  Projeto: Processamento Paralelo de IDs com Threads (C/Windows)

Este projeto demonstra a utilização de **múltiplas threads** em C para processamento robusto de uma lista de identificadores (IDs) em um ambiente Windows. O programa mestre (P0) gerencia a compilação e a execução do programa de trabalho multi-threaded (P1).

##  Funcionalidade

O projeto é dividido em dois programas principais que operam em conjunto:

| Programa | Função Principal | Saída |
| :--- | :--- | :--- |
| **`P0.c`** | **Gerenciador:** Compila dinamicamente o `P1.c` usando `system("gcc...")`, executa o `P1.exe` via `CreateProcessA` e aguarda sua finalização. | Console |
| **`P1.c`** | **Trabalhador Multi-threaded:** Lê IDs de um arquivo, processa-os de forma concorrente em 5 threads, simulando chamadas de API (respostas JSON) e registra o resultado em um log. | Arquivo `logs` |

**O objetivo é demonstrar:** Leitura robusta de arquivos, uso de threads (`CreateThread`), manipulação de seções críticas (`CRITICAL_SECTION`) e comunicação interprocessual (`CreateProcessA`, `WaitForSingleObject`).

##  Pré-requisitos

Para compilar e executar este projeto, você precisa do ambiente de desenvolvimento GCC para Windows.

### 1\. Instalar TDM-GCC

Recomendamos a instalação do TDM-GCC (versão 64-bit), que facilita a configuração do compilador:

  - **Link para Download:** `https://github.com/jmeubank/tdm-gcc/releases/download/v10.3.0-tdm64-2/tdm64-gcc-10.3.0-2.exe`
  - Certifique-se de adicionar o diretório `bin` do GCC ao seu `PATH` do sistema para que o comando `gcc` possa ser reconhecido no terminal.

##  Estrutura do Projeto

Ao extrair o pacote de arquivos (`projetos.rar` ou similar), você deve ter a seguinte estrutura:

```
TPE/
├── P0.c                # Código fonte do gerenciador
├── P1.c                # Código fonte do trabalhador multi-threaded
├── lista_ids.txt       # Arquivo de entrada com os IDs (separados por linha, vírgula ou espaço)
└── build_and_run.bat   # Script para automação da execução (se fornecido)
```

##  Instruções de Execução

O programa `P0.c` automatiza o processo de compilação e execução.

### Opção A: Usando o Script (Recomendado)

1.  Navegue até o diretório do projeto (`TPE/`).
2.  Execute o arquivo:
    ```bash
    build_and_run
    ```
##  Resultado

Após a execução, o programa `P1.exe` criará ou atualizará o arquivo:

  - **`logs`**: Contém o resultado do processamento de cada ID, com a seguinte formatação por linha:
    ```
    [DATA HORA], [ID DA THREAD], [ID PROCESSADO], [RESPOSTA JSON SIMULADA]
    ```

**Exemplo de linha no arquivo `logs`:**

```
2025-10-17 21:15:30, 4832, 1234567890, {"id":1234567890,"status":"ok","valor":542.10}
```
