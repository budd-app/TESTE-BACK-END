# 🔥 Desafio – Budd 😈  
Esse teste é feito para você desistir.

Bem-vindo ao desafio para participar da Budd CULTURE e antes de mais nada, nós sabemos fazer essa task, aqui vamos avaliar sua capacidade e principalmente resiliência de se juntar a nós nesse desafio incrível 🚀  
Queremos alguém **hacker-curioso, resiliente e criativo** para nos ajudar a construir o futuro.  
Sua missão é implementar um **MVP prático** que mostre como funcionaria uma **compra offline** no Budd.

---

## 🎯 Objetivo

Implementar **dois apps simples** que demonstrem o fluxo:

1. **Usuário** → gera **QR de pagamento assinado** com saldo debitado localmente, como uma conta digital.  
2. **PDV (Atendente)** → lê o QR, **valida assinatura**, confere estoque e gera um **recibo assinado**.  
3. Tudo deve funcionar **100% offline**.

---

## 🛠 Requisitos

### App Usuário
- Mostra um **saldo inicial fictício** (ex.: R$100).
- Permite escolher um produto (ex.: **Cerveja R$10**).
- Ao confirmar:
  - **Debita localmente** o saldo.
  - Gera um **QR Code assinado** com os dados da compra.

### App PDV
- Permite **ler o QR** do usuário.
- **Valida a assinatura** do QR com a chave pública do usuário.
- Confere se o valor/itens são válidos.
- **Baixa estoque local** (ex.: de 10 cervejas → 9).
- Gera um **recibo assinado** confirmando a venda.

---

## 🔑 Criptografia

- Usar **Ed25519** para assinatura digital (pode usar `libsodium`, `tweetnacl` ou equivalente).
- O QR de pagamento deve conter (em formato CBOR/JSON compactado):
  - `commitId` (UUID único da transação)
  - `userFp` (fingerprint da chave pública do usuário)
  - `barId` (identificação do bar)
  - `items` (lista de produtos e quantidades)
  - `total` (valor total da compra)
  - `ts` (timestamp)
  - `exp` (tempo de expiração do QR, ex.: 2 min)
  - `nonce` (valor aleatório)
  - `sigUser` (assinatura digital do usuário)

- O **recibo do PDV** deve conter:
  - `receiptId` (UUID único do recibo)
  - `commitId` (referência ao QR do usuário)
  - `barId`
  - `itemsPriced` (produtos, quantidades e preços)
  - `total`
  - `tsPdv`
  - `sigPdv` (assinatura digital do PDV)

---

## 📦 Offline First

- Nenhum servidor necessário: tudo deve funcionar **localmente**.  
- **Saldo do usuário** e **estoque do PDV** devem ser salvos em **SQLite ou MMKV** (ou equivalente).  
- O app deve funcionar mesmo fechando e reabrindo.  

---

## ⚡ Extra (diferencial)

Implementar um **broadcast BLE**:
- Quando o usuário gera o QR, o app emite um anúncio Bluetooth curto com o `commitId`.
- O PDV capta esse broadcast e mostra **“Pedido detectado próximo”**.
- O atendente ainda precisa escanear o QR para confirmar a venda.  

*(Se você tentar esse extra, mesmo que falhe, já mostra perfil hacker 🔥)*

---

## 🧩 O que será avaliado

- **Entendimento do problema** (não só código, mas arquitetura e conceito).  
- **Criatividade hacker** (formas de serializar, reduzir tamanho do QR, proteger chave, etc).  
- **Resiliência**: tratar erros offline (saldo insuficiente, estoque zerado, QR expirado).  
- **Clareza**: documentação do que foi feito e o que não foi.  
- **Curiosidade**: tentativa do extra com BLE é um diferencial.  

---

## 📋 Entregável

- Repositório GitHub com:
  - Código dos dois apps.  
  - Instruções de como rodar.  
  - Um vídeo curto mostrando:
    1. Usuário compra.  
    2. QR é gerado.  
    3. PDV lê o QR.  
    4. Estoque baixa.  
    5. Recibo aparece assinado.  

---

Boa sorte 🍀 Queremos ver sua criatividade e sua pegada hacker 🤘

