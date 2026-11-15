# Consolidação de Romaneio — Nexxa

Portal web (uma única página `index.html`) que cruza a **Grade**, a **Programação** e o **Romaneio** e gera, para cada romaneio, a planilha com a sequência de entrega por loja.

## Como usar
1. Abra `index.html` no navegador (ou o link publicado).
2. **Passo 1 – Grades - Rotas>Shopping>Loja:** grade geral consolidada (.xlsx).
3. **Passo 2 – Programação** (opcional com Grade): traz peso (PEDIDO) e data/hora de carregamento.
4. **Passo 3 – Romaneio:** relatório de expedição (.xls) com um ou vários romaneios.
5. Clique em **Consolidar** e depois em **Baixar todos os romaneios** (ou baixe um a um).

Cada romaneio sai em um arquivo `Romaneio <número> <HHhMM>.xlsx`, com:
- cabeçalho: romaneio, rota, data/hora de carregamento, volumes e peso;
- itens com **SEQ ENTREGA**, **H. ENTREGA** e **SHOPPING / ENDEREÇO**;
- aba **Resumo por loja**.

## Regras da sequência
- **Número** = ordem de entrega da loja na Grade (TRANSIT TIME + HORÁRIO DE ENTREGA), só com as lojas presentes no romaneio.
- **Letra** = ponto de parada (shopping/endereço). A letra se repete enquanto as paradas seguidas forem no mesmo local; se a sequência quebrar, vira outra letra. Ex.: `1 - A`, `2 - A`, `3 - B`.
- **Mesmo local** = mesma cidade e:
  - mesmo número no endereço (ignora LJ/LOJA; rodovia sem número usa o km), ou
  - nome do shopping com 2+ coincidências contando a palavra SHOPPING (ex.: *Shopping Itaquera* × *Shopping Metro Itaquera*). "X SH" é comparado separado de "Shopping X". Marca (REDE), cidade, UF e texto entre parênteses não contam.
- Rota do romaneio que não existe na Grade com o mesmo código é associada à rota da Grade com mais lojas em comum e mesmo dia de carregamento (o portal avisa).

## Publicação
É um site estático: funciona no GitHub Pages, Vercel (arrastar a pasta em vercel.com/drop) ou qualquer servidor web.
As planilhas são processadas no navegador; nada é enviado a servidor. Requer acesso a `cdnjs.cloudflare.com` (biblioteca SheetJS).
