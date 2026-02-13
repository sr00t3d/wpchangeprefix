# WP Change Prefix

Readme: [English](README.md)

![License](https://img.shields.io/github/license/sr00t3d/wpchangeprefix)
![Shell Script](https://img.shields.io/badge/shell-script-green)

Um script Bash poderoso, seguro e automatizado para alterar o prefixo das tabelas do banco de dados do WordPress. Esta ferramenta gerencia todo o processo: criação de backup do banco de dados, renomeação das tabelas, atualização de referências internas (usermeta/options) e modificação do `wp-config.php`.

## 🚀 Recursos

- **Descoberta Automática**: Detecta automaticamente as credenciais do banco de dados e o prefixo atual a partir do wp-config.php.
- **Segurança em Primeiro Lugar**: Cria um backup completo do banco de dados (`.sql dump`) antes de aplicar qualquer alteração.
- **Limpeza Profunda**: Não apenas renomeia as tabelas, mas também atualiza linhas críticas nas tabelas `_usermeta` e `_options` para evitar problemas de permissão.
- **Atualização de Configuração**: Atualiza automaticamente a variável `$table_prefix` no seu arquivo `wp-config.php`.
- **Autoatualização**: Verifica remotamente a versão mais recente do script.

## 📋 Pré-requisitos

Para executar este script, seu ambiente deve ter:
- SO Linux/Unix (Ubuntu, Debian, CentOS, etc.)
- `bash` (shell)
- `mysql` e `mysqldump` (ferramentas cliente)
- `grep`, `awk`
- `curl` ou `wget` (para verificação de atualizações)
- Acesso `Root/Sudo` é recomendado se as permissões de arquivo forem restritas, embora não seja estritamente necessário se o usuário for proprietário dos arquivos.

## 📥 Instalação

Você pode baixar o script diretamente para o diretório raiz do seu WordPress:

```bash
wget https://raw.githubusercontent.com/percioandrade/wpchangeprefix/refs/heads/main/wp-change-prefix.sh
chmod +x wpchange_prefix.sh
```

## ⚙️ Uso

**1. Navegue até o diretório raiz do seu WordPress (onde o wp-config.php está localizado).**

**2. Execute o script:**

```bash
./wpchange_prefix.sh
```

**3. Siga os prompts interativos:**

- O script irá verificar as credenciais.
- Ele mostrará o prefixo atual detectado.
- Ele pedirá o NOVO prefixo (apenas alfanumérico).
- Confirme a operação.

## Opções de Linha de Comando

```bash
Flag             Descrição
-s, --skip       Pular Backup: Executa o script sem criar um dump do banco de dados (Não recomendado).
-n, --noversion  Sem Verificação de Versão: Ignora a verificação remota de atualizações do script.
-h, --help       Exibe o menu de ajuda.
```

**Exemplo**

# Executar sem verificar atualizações e pulando o backup

```bash
./wpchange_prefix.sh --skip --noversion
```

🛠️ Como Funciona

- **Validação**: Verifica se o `wp-config.php` existe e analisa as credenciais do banco de dados.
- **Conexão**: Testa a conexão com o servidor MySQL.
- **Detecção**: Examina `information_schema` para encontrar o prefixo ativo (procurando por `_usermeta` ou `_options`).
- **Backup**: Executa `mysqldump` para salvar o estado atual.
- **Renomeação**: Percorre todas as tabelas que correspondem ao prefixo antigo e as renomeia para o novo prefixo.
- **Correção de Dados**: Executa atualizações SQL para corrigir referências de prefixo dentro de `usermeta` (chaves como `wp_capabilities`) e options (chaves `like wp_user_roles`).
- **Finalização**: Atualiza a variável PHP no arquivo de configuração.

## ⚠️ Aviso Legal

> [!WARNING]
> Este software é fornecido "como está". Certifique-se sempre de testar primeiro em um ambiente de desenvolvimento. O autor não se responsabiliza por qualquer uso indevido, consequências legais ou impacto em dados causado por esta ferramenta.

## 📚 Tutorial Detalhado

Para um guia completo, passo a passo, sobre como importar arquivos gerados para o Thunderbird e solucionar problemas comuns de migração, confira meu artigo completo:

👉 [**Criar popups modais no WHMCS**](https://perciocastelo.com.br/blog/change-wordpress-database-prefix.html)

## Licença 📄

Este projeto está licenciado sob a **GNU General Public License v3.0**. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.
