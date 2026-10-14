# Plano do port para SkyFire 5.4.8

## Integração local

O SkyFire em `FableCraze/SkyFire_548` descobre módulos em `modules/` e chama
`Addmod_breaking_news_overrideScripts()`. O loader herdado já possui esse
nome. `module.cmake` define `MODULE_ENABLED FALSE` antes da coleta de fontes,
configuração e registro de scripts, até a implementação do port.

## Incompatibilidades identificadas

| Implementação herdada | Situação no SkyFire local |
| --- | --- |
| `WardenPayloadMgr` e `GetPayloadMgr()` | Ausentes; falta o transporte de payloads utilizado pelo módulo. |
| `ForceChecks()` e `IsInitialized()` | Não expostos na interface pública de `Warden`. |
| `CanPacketSend(WorldSession*, WorldPacket const&)` | Ausente. `OnPacketSend(WorldSocket*, WorldPacket&)` não é uma substituição direta. |
| `OnAfterConfigLoad` e enums de hooks nos construtores | Adaptar para `OnConfigLoad(bool)` e construtores com nome do script. |
| `sConfigMgr->GetOption<T>()` | Adaptar às APIs `GetXOption` do SkyFire. |
| `Acore::StringFormat` e macros `LOG_*` | Adaptar às interfaces de formatação e logging do SkyFire. |
| Payload Lua e quadros da UI | Validar especificamente no cliente MoP 5.4.8. |

## Sequência proposta

1. Definir um transporte suportado pelo cliente 5.4.8 para atualizar o quadro
   de notícias e os pontos de integração necessários no core.
2. Implementar o transporte preservando as verificações normais do Warden,
   tratando sessão, inicialização, limites e desconexões.
3. Adaptar hooks, configuração, logging e formatação ao SkyFire.
4. Revisar estado global e escape de HTML/título no transporte escolhido.
5. Adicionar HTML de exemplo e instruções de configuração reais.
6. Compilar contra uma revisão identificada do SkyFire e testar no cliente:
   seleção de personagem, reconexão, cache, recarga, arquivo ausente,
   conteúdo vazio e conteúdo longo.
7. Ativar a seleção em `module.cmake` e adicionar CI de compilação SkyFire.

O workflow de build AzerothCore foi removido: ele não validaria o port SkyFire.
A presença dos fontes originais não significa compatibilidade funcional.
