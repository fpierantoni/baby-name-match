# 📊 Configuração do Analytics

Este guia explica como configurar e usar o Google Analytics no app.

---

## 🚀 Passo 1: Criar Conta Google Analytics

1. Acesse [analytics.google.com](https://analytics.google.com)
2. Clique em **"Começar a medir"** (ou "Start measuring")
3. Crie uma conta:
   - **Nome da conta:** Meu Nome É
   - Aceite os termos
4. Crie uma propriedade:
   - **Nome da propriedade:** Meu Nome É - App
   - **Fuso horário:** Brasília (GMT-3)
   - **Moeda:** Real brasileiro (BRL)
5. Selecione **"Web"** como plataforma
6. Configure o fluxo de dados:
   - **URL do site:** `https://baby-name-match.netlify.app`
   - **Nome do fluxo:** App Web
7. **COPIE O MEASUREMENT ID** (formato: `G-XXXXXXXXXX`)

---

## 🔧 Passo 2: Adicionar o ID no Código

No arquivo `index.html`, procure por:

```javascript
gtag('config', 'G-XXXXXXXXXX'); // SUBSTITUIR pelo seu Measurement ID
```

E substitua `G-XXXXXXXXXX` pelo seu Measurement ID real em **DOIS lugares**:

1. Na linha do script do gtag
2. Na configuração do gtag

**Exemplo:**
```javascript
<script async src="https://www.googletagmanager.com/gtag/js?id=G-ABC123DEF4"></script>
<script>
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('js', new Date());
    gtag('config', 'G-ABC123DEF4'); // ← SEU ID AQUI
```

---

## 📈 Métricas Rastreadas

### 1. **Acessos ao Site**
- Automático pelo Google Analytics
- Visualize em: **Relatórios → Aquisição → Visão geral**

### 2. **Início do Jogo** (`game_start`)
Disparado quando o usuário clica em "Começar"

**Propriedades:**
- `game_mode`: "casal" ou "solo"
- `gender_choice`: "menino", "menina" ou "surpresa"

**Ver em:** Eventos → game_start

### 3. **Nomes Adicionados Manualmente** (`custom_name_added`)
Disparado quando o usuário adiciona um nome customizado

**Propriedades:**
- `name`: Nome adicionado
- `player`: Número do jogador (1 ou 2)
- `gender`: Gênero selecionado

**Ver em:** Eventos → custom_name_added

### 4. **Jogo Completo** (`game_completed`)
Disparado quando o usuário chega na tela de resultados

**Propriedades:**
- `game_mode`: "casal" ou "solo"
- `gender_choice`: "menino", "menina" ou "surpresa"
- `winner`: Nome vencedor (1º lugar)
- `second_place`: Nome em 2º lugar
- `third_place`: Nome em 3º lugar
- `total_names`: Total de nomes que participaram

**Ver em:** Eventos → game_completed

---

## 📊 Como Ver os Dados

### Dashboard Principal
1. Acesse [analytics.google.com](https://analytics.google.com)
2. Selecione sua propriedade
3. Vá em **Relatórios → Tempo real** para ver dados ao vivo

### Eventos Customizados
1. **Relatórios → Envolvimento → Eventos**
2. Procure por:
   - `game_start`
   - `custom_name_added`
   - `game_completed`

### Análises Úteis

#### Modo de Jogo Mais Popular
1. Eventos → game_start
2. Adicionar dimensão secundária: `game_mode`
3. Ver contagem de "casal" vs "solo"

#### Gênero Mais Escolhido
1. Eventos → game_start
2. Adicionar dimensão secundária: `gender_choice`

#### Nomes Mais Adicionados Manualmente
1. Eventos → custom_name_added
2. Adicionar dimensão secundária: `name`
3. Ver quais nomes aparecem mais (indica que deveriam estar no banco)

#### Top 10 Nomes Vencedores
1. Eventos → game_completed
2. Adicionar dimensão secundária: `winner`
3. Ver ranking dos nomes que mais ganham

---

## 🔍 Criando Relatórios Customizados

### Exemplo: Ranking de Nomes Vencedores

1. Vá em **Explorar** (menu lateral)
2. Clique em **Criar nova exploração**
3. Configure:
   - **Técnica:** Forma livre
   - **Dimensões:** Adicionar "Nome do evento" e "winner"
   - **Métricas:** Adicionar "Contagem de eventos"
   - **Filtro:** Nome do evento = "game_completed"
4. Arraste "winner" para Linhas
5. Arraste "Contagem de eventos" para Valores
6. Ordene por contagem (decrescente)

**Resultado:** Você verá quantas vezes cada nome foi vencedor!

---

## 🔒 Privacidade

**O que NÃO rastreamos:**
- ❌ Nomes dos participantes (usuários)
- ❌ IPs ou localização precisa
- ❌ Dados pessoais sensíveis

**O que rastreamos:**
- ✅ Uso do app (modo, gênero)
- ✅ Nomes de bebê escolhidos (dados públicos, não pessoais)
- ✅ Padrões de uso agregados

---

## 💡 Dicas

1. **Aguarde 24-48h** para dados significativos
2. Use **Tempo Real** para testar imediatamente
3. Crie **alertas** para metas (ex: 100 jogos completados)
4. Exporte dados periodicamente para análises externas

---

## 🆘 Problemas Comuns

### "Não vejo dados no Analytics"
- ✅ Confirme que substituiu o Measurement ID
- ✅ Aguarde 10 minutos após deploy
- ✅ Teste em modo anônimo (evita ad blockers)
- ✅ Verifique console do navegador (F12) por erros

### "Eventos não aparecem"
- ✅ Vá em **Tempo Real → Visão geral** e teste o app
- ✅ Eventos customizados podem demorar até 24h para aparecer em relatórios

---

## 📞 Suporte

- [Central de Ajuda do Google Analytics](https://support.google.com/analytics)
- [Documentação de Eventos GA4](https://developers.google.com/analytics/devguides/collection/ga4/events)

---

**Configurado com sucesso?** Agora você tem insights poderosos sobre o uso do app! 🎉

