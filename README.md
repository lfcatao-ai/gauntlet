# GAUNTLET ⚡

Jogo de micro-desafios sincronizados pra jogar em grupo, na mesa, cada um no seu celular.
15 desafios sorteados por código de sala (mesma semente = mesma sequência em todos os
celulares) + boss final. Ranking automático entre celulares usando este próprio repo
como banco de dados (via GitHub API).

## Como jogar

1. Todo mundo abre **https://lfcatao-ai.github.io/gauntlet/** pelo link do grupo
   (o link do grupo tem `#t=TOKEN` no final — é ele que liga o ranking automático).
2. Mesmo **código de sala** pra todo mundo.
3. Grito de "3, 2, 1, VAI!" na mesa e todos tocam JOGAR juntos.
4. Fim da rodada: o score publica sozinho; a tela **Ranking** atualiza ao vivo (8s).

## Ranking automático — como funciona

- Fim de rodada → o jogo faz `PUT /repos/lfcatao-ai/gauntlet/contents/scores/SALA__RODADA__NOME__PONTOS.json`
  usando o token do fragmento `#t=` do link (fica só no link e no localStorage; nunca no código).
- Tela de ranking → lista `scores/` a cada 8s e monta a tabela (leitura pública, sem auth).
- Sem token no link, o jogo cai no modo manual (código reserva de 5 caracteres com checksum).

## Manutenção

- **Token expirou?** Gerar outro em GitHub → Settings → Developer settings →
  Fine-grained tokens: Repository access = só `gauntlet`; Permissions = Contents: Read and write.
  Reenviar o link no grupo com o `#t=NOVO_TOKEN`.
- **Limpar o placar da noite:** apagar os arquivos de `scores/` (ou só os da sala).
- **Nova versão do jogo:** editar `index.html`; o Pages atualiza sozinho em ~1 min.
  O badge de versão na tela inicial existe pra mesa conferir que todos deram refresh.
