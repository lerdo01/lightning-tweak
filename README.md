# ⚡ Lightning Tweak

Otimizador de desempenho e manutenção para **Windows 10 e Windows 11**, com backend em **Rust** e interface em **Tauri 2 + React + TypeScript**.

> 🚧 **Projeto em desenvolvimento.** O Lightning Tweak ainda não foi lançado e não possui versão beta nem releases publicadas. O código deste repositório está em construção e pode mudar a qualquer momento.

---

## O que é

O Lightning Tweak age **diretamente no sistema**: Registry, serviços, planos de energia, inicialização automática e limpeza de disco. Tudo roda localmente:

- Nada é enviado para a internet.
- Nenhum programa adicional é instalado.
- Todo ajuste tem um botão que **restaura o valor padrão do Windows**.
- Ajustes marcados como **alto risco** exigem confirmação na interface.

## Status

| Item | Situação |
| --- | --- |
| Versão | Nenhuma lançada |
| Beta | Não disponível |
| Instalador / binários | Não disponíveis |
| Desenvolvimento | Ativo |

Quando houver uma primeira versão de testes, ela será publicada na aba **Releases** deste repositório.

## Seções do aplicativo

### Ajustes

| Seção | O que cobre |
| --- | --- |
| **Painel** | Visão geral (CPU, memória, discos, tempo ligado) e otimização rápida |
| **Desempenho** | Efeitos visuais, animações, thumbnails, Game Mode, HAGS, throttling de CPU, indexação, pagefile, TRIM, boot multicore |
| **Energia** | Plano de alto desempenho, suspensão USB, início rápido |
| **Rede** | Pilha TCP/IP, Wi-Fi de alto desempenho, Teredo, NetBT, ICS, assinatura SMB, NCSI |
| **Privacidade** | Telemetria, ID de publicidade, Cortana, histórico de atividade, localização, relatórios de erro, inventário de aplicativos, OneDrive |

### Manutenção

| Seção | O que cobre |
| --- | --- |
| **Otimização geral** | Limpeza de `%TEMP%`, `C:\Windows\Temp`, cache de shaders, crash dumps, WER, logs, caches de navegadores, Windows Update, Lixeira, `MEMORY.DMP` e `pagefile.sys` |
| **Inicialização** | Itens de `Run`, `Run32` e pasta Startup, ordenados por impacto, com leitura dos blobs `StartupApproved` |
| **Serviços** | Catálogo completo via CIM, mudança do modo de inicialização e iniciar/parar/reiniciar |
| **Diagnóstico** | SFC, DISM, CHKDSK e outras ferramentas do Windows |
| **Sobre** | Versão do Windows, CPU, RAM, ativação, privilégios e teste de permissão de escrita no Registry |

## Como funciona

| Parte | Onde fica | Responsabilidade |
| --- | --- | --- |
| Backend | `src-tauri/src` | Lê e escreve no Registry, controla serviços, executa manutenções |
| Frontend | `src` | Dashboard em React com menu lateral por categoria |
| Configuração | `src-tauri/tauri.conf.json` | Janela, CSP, bundle NSIS/MSI |
| Elevação | `src-tauri/windows/app.manifest` | `requireAdministrator` (UAC automático ao abrir) |

### Privilégios de administrador

O manifesto do Windows pede privilégios de administrador na inicialização, então o UAC aparece assim que o programa abre. Se o usuário recusar, o app abre em **modo somente leitura**, e o botão **"Executar como Administrador"** fica disponível no menu lateral.

Em builds de **debug** (`npm run tauri dev`), o `build.rs` troca o nível para `asInvoker`. Sem isso, o `tauri dev` falha com o erro 740: o Windows só exibe o UAC em lançamento interativo, e um processo filho de um shell comum é recusado. A elevação continua disponível pelo botão do menu lateral.

## Tecnologias

- [Rust](https://www.rust-lang.org/)
- [Tauri 2](https://tauri.app/)
- [React](https://react.dev/)
- [TypeScript](https://www.typescriptlang.org/)

## Aviso

Este software modifica configurações do Windows (Registry, serviços, energia, rede e privacidade). Use por sua conta e risco. Os ajustes de alto risco pedem confirmação, e cada alteração pode ser revertida ao padrão do Windows pelo próprio aplicativo.

## Contribuindo

Sugestões e issues são bem-vindas. Como o projeto ainda está em fase inicial, a estrutura pode mudar bastante antes da primeira versão.

## Licença

