# Plano de Conclusão — Sistema de Criptografia e Descriptografia Avançada

> Gerado em 2026-10-09. Baseado no estado real do código + README.

## Estado atual
- Núcleo AES em Assembly x86 (`AES-Encryption.asm` + `.inc`: SBOX, rounds, key schedule,
  Encryption/Decryption, Socket, IO). Monta com NASM (`-f elf64`) + `ld` → **ELF Linux**.
- GUI C# (`gui_cs/`, net7.0-windows) — **compila** (validado). Sobe o binário do backend
  (opção via WSL) e fala por socket TCP (porta 9001).
- O `_start` ramifica para um **modo servidor TCP** marcado **WIP** no README.

## O que falta
1. **Finalizar o modo servidor (WIP)** — completar o loop `accept`→receber→cripto/decripto→
   responder; múltiplas conexões e encerramento limpo; remover rótulo "experimental".
2. **Protocolo GUI↔backend** — definir e documentar o framing das mensagens no socket;
   validar o fluxo ponta a ponta (GUI Windows → WSL → servidor asm).
3. **Robustez cripto** — IV/nonce por mensagem, padding, tratamento de erro (chave errada,
   dados truncados) no asm.
4. **Build multiplataforma** — hoje gera ELF Linux; adicionar variante Windows OU documentar
   claramente que o backend roda só em Linux/WSL e a GUI o invoca via WSL.
5. **Testes de interoperabilidade** — vetores NIST conhecidos para validar o AES do asm;
   teste automatizado GUI↔servidor.
6. **Empacotamento** — script único que builda asm (Linux/WSL) + GUI (.NET) e explica o fluxo.

## Ferramentas / limitações
- NASM disponível (instalado nesta sessão) e .NET disponível; link/run do ELF exige Linux/WSL.
- Esforço: **médio-baixo** (núcleo pronto; falta fechar o servidor + integração).
