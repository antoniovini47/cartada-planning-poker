<div align="center">

# Cartada

**Planning poker direto ao ponto.** Abra uma mesa, mande o link e estimem juntos.

Sem cadastro · Sem servidor · Sem banco de dados · Grátis

**[cartada-planning-poker.vercel.app](https://cartada-planning-poker.vercel.app)**

![Mesa do Cartada com as cartas reveladas](docs/screenshot.png)

</div>

## Como usar

1. Digite seu nome e clique em **Criar sala**.
2. Clique em **Copiar convite** e mande o link para o time.
3. Cada pessoa escolhe uma carta. Ninguém vê o voto dos outros até alguém clicar em **Revelar cartas**.
4. Aparecem a média, a distribuição dos votos e o selo de **Consenso!** quando todos votam igual.
5. Clique em **Nova rodada** e repita.

Baralho: `0 1 2 3 5 8 13 21 34 55 89 ? ☕`

## Como funciona

O Cartada é **um único arquivo HTML**. Não tem backend nem banco de dados.

- **Peer-to-peer:** os navegadores conversam direto entre si via WebRTC ([PeerJS](https://peerjs.com)). O servidor público do PeerJS só faz a apresentação entre eles; os votos não passam por ele.
- **Anfitrião automático:** o primeiro navegador a abrir a sala guarda o estado da mesa. Se ele sair, outro participante assume em poucos segundos e os votos da rodada são reenviados.
- **Memória local:** seu nome, sua identidade anônima e a última sala ficam no `localStorage` do navegador por 1 ano. Ao abrir outro link, você entra direto; na home, aparece um atalho para voltar à última sala, se ela ainda tiver gente.
- **Nada fica guardado:** quando todos saem, a sala deixa de existir.

## Rodando localmente

Qualquer servidor estático serve:

```bash
git clone https://github.com/antoniovini47/cartada-planning-poker.git
cd cartada-planning-poker
python3 -m http.server 8000
```

Abra `http://localhost:8000`. Para publicar, basta subir o `index.html` em qualquer hospedagem estática (Vercel, Netlify, GitHub Pages...).

## Limitações

- A conexão é direta entre navegadores e não há servidor de retransmissão (TURN). Em redes corporativas muito restritas, ela pode falhar.
- Quando o anfitrião sai durante a rodada, os votos são preservados, mas cartas já reveladas voltam a ficar escondidas.
- Não há controle de permissão: qualquer pessoa da sala pode revelar ou começar uma nova rodada. É pensado para times que confiam uns nos outros.

## Contribuindo

Issues e pull requests são bem-vindos. O código é vanilla JS, sem build e sem dependências além do PeerJS via CDN.

## Licença

[MIT](LICENSE). Use, copie, modifique e distribua à vontade.
