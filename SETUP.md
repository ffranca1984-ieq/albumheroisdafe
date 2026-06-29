# Heróis da Fé — Guia de Configuração

## 1. Criar o projeto Firebase (novo)
1. Acesse https://console.firebase.google.com → "Adicionar projeto" → nome "Herois da Fe" (ou outro).
2. Em **Build > Authentication > Sign-in method**, ative **Google**.
3. Em **Build > Firestore Database**, clique em "Criar banco de dados" (modo produção).
4. Cole o conteúdo de `firestore.rules` nas regras do Firestore (aba "Regras").
5. Em **Configurações do projeto > Geral**, role até "Seus apps" → clique no ícone `</>` (Web) → registre o app → copie o objeto `firebaseConfig`.
6. Abra `index.html`, localize o bloco:
   ```js
   const firebaseConfig = {
     apiKey: "SUBSTITUA_AQUI",
     ...
   };
   ```
   e substitua pelos valores reais copiados no passo 5.
7. Em **Authentication > Settings > Authorized domains**, adicione o domínio do Vercel (ex: `herois-da-fe.vercel.app`) depois do deploy.

## 2. Subir para o GitHub
1. Crie um repositório novo, ex: `ffranca1984-ieq/herois-da-fe` (ou pessoal, já que o app é genérico).
2. Suba os arquivos: `index.html`, `manifest.json`, `sw.js`.
3. (Opcional) Suba também `icon-192.png` e `icon-512.png` — qualquer ícone quadrado com o tema do app; sem eles o PWA funciona, só não terá ícone customizado na tela inicial.

## 3. Deploy no Vercel
1. No painel da Vercel, "Add New Project" → importe o repositório criado.
2. Sem necessidade de build command (é HTML estático) — Framework Preset: "Other".
3. Deploy. A URL final será algo como `herois-da-fe.vercel.app`.
4. Volte ao Firebase (passo 1.7) e adicione esse domínio na lista de domínios autorizados — sem isso o login Google não funciona.

## 2. Como funciona a mecânica (resumo)
- **Envelope grátis**: 1 a cada 24h, 5 figurinhas por envelope.
- **Envelopes bônus**: +1 por "Devocional", +1 por "Leitura", +1 por "Quiz" — zera todo dia à meia-noite (local).
- **Raridades**: Comum 70% · Rara 25% · Lendária 5% (só 5 figurinhas lendárias no álbum: Noé, Moisés, Maria, Jesus, Pedro... ajustável em `STICKERS` no código).
- **Trocas**: usuário marca uma repetida como "disponível" → outro usuário vê na aba "Disponíveis" e pode pedir → transferência automática via Firestore transaction.
- **Tudo estático**: as 100 figurinhas (nome, categoria, raridade, versículo, ícone) estão no array `STICKERS` dentro do `index.html` — para editar nomes/versículos/raridades, basta editar esse array, sem custo de API.

## Próximos passos sugeridos
- Substituir os emojis por ilustrações reais, se desejar (basta trocar o campo `icon` de cada item por uma URL de imagem e ajustar o CSS de `.sticker-art` / `.reveal-art` para `<img>`).
- Gerar `icon-192.png` / `icon-512.png` para a tela inicial do PWA.
- Criar QR code de divulgação, como feito para o Família em Conexão.
