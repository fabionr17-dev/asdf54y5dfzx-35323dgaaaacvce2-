# Meu Centro de Controle — app instalável (PWA) com digital

Esta pasta transforma o seu app do Google Apps Script em um **aplicativo instalável** no celular (ícone na tela inicial, janela própria, atalhos de toque longo) e habilita **entrar com a digital**.

O app continua rodando 100% no Google. Esta pasta é só a "casca".

## O que fica no GitHub (e o que NÃO fica)

Ficam só estes 7 arquivos, todos soltos (sem pastas): `index.html` (cerca de 17 KB), `sw.js`, `manifest.json` e 4 ícones `.png`.

**Não ficam no GitHub:** o código do app (`Code.gs` e `App.html`), os seus dados (a planilha), a sua senha e nem sequer a URL do app. A URL `/exec` é colada no celular na primeira abertura e fica guardada só nele. Não há nenhum segredo nesses arquivos. A página também pede aos buscadores para não listá-la (`noindex`).

### Repositório privado: o que muda de verdade

- No plano grátis, o GitHub Pages só publica a partir de repositório **público**.
- Repositório **privado** com Pages exige plano pago (GitHub Pro).
- Mesmo com repositório privado, o **site publicado continua acessível a quem souber o endereço**. Para o site ser realmente restrito, o GitHub exige uma conta de organização.

Ou seja: privado esconde os arquivos-fonte, não o endereço. Como a casca não tem segredo, as duas opções são seguras. O que mais protege é usar um **nome neutro** no repositório (por exemplo `mc-4k8x`, e não `meu-centro-fabio`) e não divulgar o endereço.

## Passo a passo (uma vez só, uns 10 minutos, no computador)

1. **Apps Script:** cole o `Code.gs` e o `App.html` mais recentes e publique **Nova versão** (Implantar → Gerenciar implantações → ✏ → Nova versão).
   Confira: **Executar como: Eu** e **Quem tem acesso: Qualquer pessoa** (obrigatório para abrir dentro do app instalado).
2. **GitHub:** em https://github.com, **New repository**. Dê um nome neutro, escolha **Private** (precisa de GitHub Pro) ou **Public**, e **não** marque "Add a README". Create.
3. **Add file → Upload files:** selecione e arraste os **7 arquivos** (`index.html`, `sw.js`, `manifest.json`, `icon-192.png`, `icon-512.png`, `icon-512-maskable.png` e `apple-touch-icon.png`), **todos soltos, sem pasta**. Commit. (O `LEIA-ME.md` não precisa ir para o GitHub.)
4. **Settings → Pages:** em *Source* escolha *Deploy from a branch*, depois `main` e `/ (root)`, e Save. Em 1 a 2 minutos o endereço aparece no topo da página:
   `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/`
5. **No celular (Chrome):** abra esse endereço. Na primeira vez aparece "Falta configurar a URL": cole a URL do app (Apps Script → Implantar → Gerenciar implantações → copiar a que termina em `/exec`) e toque em **Salvar e abrir**.
6. **Instale:** menu ⋮ do Chrome → **Instalar app** (ou Adicionar à tela inicial). Se você tinha um atalho antigo do link `/exec`, apague-o.
7. **Ative a digital** (próxima seção).

## Entrar com a digital (Android)

1. Abra o app **pelo ícone instalado** e entre com a senha.
2. Vá em **Configurações → Segurança → Entrar com a digital → Ativar digital neste aparelho**
   (o app também oferece isso uma vez, logo depois do login).
3. Confirme a senha, toque em **Continuar** e confirme com a digital (ou o bloqueio de tela do celular).
   O Android pode mostrar um aviso para "criar uma chave de acesso". É isso mesmo, pode aceitar.

Daqui em diante, ao abrir o app aparece a tela de digital; confirmou, entrou.

- **Bloqueio automático:** se o app ficar mais de 3 minutos em segundo plano, a tela de digital volta.
- **"Usar senha":** na tela de digital, entra pela senha normal (a digital continua cadastrada).
- **Revogar:** em Configurações → Segurança dá para revogar um aparelho ou todos. **Trocar a senha desconecta todos.**
- **Validade:** cada aparelho vale 90 dias a partir do último uso; usando, renova sozinho. Limite de 12 aparelhos.
- **Como funciona:** o servidor guarda só o *hash* de uma chave aleatória; a chave fica no celular e só é entregue ao app depois que a digital é confirmada. A senha continua valendo em qualquer lugar.
- **A digital fica ligada ao endereço do site.** Se um dia você mudar o endereço (outro usuário, outro repositório ou outra hospedagem), reinstale o ícone e ative a digital de novo.
- A digital só funciona pelo **ícone instalado**. No link direto do Apps Script, use o gerenciador de senhas do Chrome (o app explica em Configurações → Segurança).

## Se não aparecer "Instalar"

O Chrome só oferece instalar quando o manifesto aponta ícones de 192 e 512 pixels que realmente existam no site. Confira:

1. Abra `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/icon-192.png` e `.../icon-512.png`. Se aparecer "404", os ícones não foram enviados: envie os 4 arquivos `.png` soltos, na mesma pasta do `index.html`.
2. Atualize a página sem usar o cache (no computador: Ctrl+F5; no celular: feche e abra o Chrome) e espere uns segundos.
3. No computador, aperte F12 → aba **Application → Manifest**: ela lista o que está faltando.
4. Enquanto isso, o menu ⋮ do Chrome → **Adicionar à tela inicial** cria um atalho que abre o mesmo app. A digital funciona nele também.
5. Se você já instalou o app uma vez, o botão não aparece de novo. Procure o ícone na tela inicial.

## Atalhos por URL

Você pode criar seus próprios atalhos/widgets apontando para:

| URL | Abre |
|---|---|
| `.../index.html?action=novaconta` | Adição rápida já no tipo Conta |
| `.../index.html?action=receita` | Adição rápida no tipo Receita |
| `.../index.html?action=tarefa` | Adição rápida no tipo Tarefa |
| `.../index.html?action=add` | Adição rápida (detecta o tipo) |
| `.../index.html?action=hoje` | Página Hoje |
| `.../index.html?action=agenda` | Agenda |
| `.../index.html?action=contas` | Contas |

Os mesmos parâmetros funcionam direto na URL `/exec` do Apps Script, se preferir.

## Atualizações

- **Mudanças em `App.html` / `Code.gs`:** publique **Nova versão** no Apps Script; o app instalado pega sozinho.
- **Mudanças nesta pasta:** troque no GitHub só os arquivos que mudaram (**Add file → Upload files**, mesmo nome, Commit).
  Se o app instalado continuar na versão antiga, feche-o e abra de novo (ou limpe os dados do site no Chrome).
