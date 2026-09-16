# Oficina Web3: Meu Primeiro Smart Contract na Stellar (Rust + Soroban)

Bem-vindo(a) ao ambiente prático da oficina **"Desbravando a Web3"** dos Encontros Universitários 2026 - UFC Quixadá!

Neste repositório, você dará os seus primeiros passos como desenvolvedor(a) Web3. O ambiente (GitHub Codespaces) já está 100% configurado com o compilador **Rust**, o target **WebAssembly** e a **Stellar CLI**. Não é necessário instalar nada no seu computador!

---

## Passo 0: Faça o Fork e abra o Codespaces

Para salvar o seu progresso e garantir a sua presença, você precisa criar a sua própria cópia deste projeto.

1. No canto superior direito desta página, clique no botão **Fork** e confirme a criação no seu perfil do GitHub.
2. No seu novo repositório (o fork), clique no botão verde **Code**, vá na aba **Codespaces** e clique em **Create codespace on main**.
3. Aguarde o ambiente carregar (pode levar de 1 a 2 minutos no primeiro acesso).

---



## Passo 1: Entendendo o Contrato

Abra o arquivo localizado em `contracts/hello_world/src/lib.rs`. 
Este é o nosso Smart Contract. Ele possui uma única função chamada `hello` que recebe um nome (String) e retorna uma lista com `["Hello", "Nome"]`.

* **`#![no_std]`**: Instrui o Rust a não utilizar a biblioteca padrão pesada, mantendo nosso contrato extremamente leve para rodar na blockchain.
* **`Env`**: É o ambiente da blockchain. Tudo no Soroban precisa do `Env` para acessar a memória e os recursos da rede.

---

## Passo 2: Rodando os Testes

Antes de enviar qualquer coisa para a blockchain, precisamos garantir que o código funciona perfeitamente de forma local.
Abra o terminal na parte inferior da tela (ou aperte `` Ctrl + ` ``) e digite:

```bash
cargo test
```

Sucesso: Se você ver test test::test ... ok, parabéns! O contrato passou no teste automatizado.

## Passo 3: Compilando para WebAssembly (Wasm)

Smart Contracts na Stellar não rodam como código Rust normal. Eles precisam ser transformados em um formato universal, seguro e minúsculo chamado WebAssembly (.wasm).

No terminal, execute o comando de build da Stellar CLI:

```bash
stellar contract build
```

Onde está meu contrato? Na barra lateral esquerda do explorador de arquivos, navegue até: target/wasm32v1-none/release/hello_world.wasm. Este arquivo .wasm é o seu Smart Contract pronto para ir ao ar!

## Passo 4: Criando sua Identidade na Testnet

Para publicar um contrato na blockchain, você precisa de uma conta ("carteira") e de saldo para pagar as taxas da rede. Como usaremos a Testnet (rede de testes), o dinheiro é fictício e gerado gratuitamente por um robô (Friendbot).

1. Gere uma nova identidade e peça fundos:
```bash
stellar keys generate teste --network testnet --fund
```

(Isso cria uma conta chamada "teste" e já deposita saldo fictício nela)

2. Verifique a sua chave pública:
```bash
stellar keys address teste
```

(Isso retornará a sua chave pública começando com G.... Você já está pronto para o deploy!)

## Passo 5: Deploy! (Publicando na Blockchain)

Agora vamos enviar o seu arquivo .wasm para a blockchain da Stellar (Testnet). Execute o comando (copie e cole tudo junto):
```bash
stellar contract deploy \
  --wasm target/wasm32v1-none/release/hello_world.wasm \
  --source-account teste \
  --network testnet \
  --alias hello_world
```

Parabéns! O terminal retornará um código longo começando com a letra C.
Este é o seu Contract ID (Endereço do Contrato). Salve este código, você vai precisar dele! Ele é a prova de que o seu contrato está vivo na blockchain.

## Passo 6: Interagindo com o Contrato

Seu contrato está na rede! Vamos chamá-lo para ver a resposta.

Copie o comando abaixo, mas ATENÇÃO: substitua SEU_CONTRACT_ID_AQUI pelo código que começou com C que você gerou no Passo 5:

```bash
stellar contract invoke \
  --id SEU_CONTRACT_ID_AQUI \
  --source-account teste \
  --network testnet \
  -- \
  hello \
  --to Turma
```


Resultado Esperado: O terminal deve retornar ["Hello", "Turma"].
(Nota: Como essa função apenas "lê" dados e não altera o estado da blockchain, a CLI roda uma simulação gratuita instantânea, sem cobrar taxas!)

## Passo 7: Validação de Presença e Certificado:
Para garantir o seu certificado de participação nos Encontros Universitários 2026, você precisa provar que executou a prática.

1. Copie o Contract ID gerado no Passo 5 (aquele que começa com C).
2. Copie o Link do seu repositório no GitHub (o fork que você criou no Passo 0).
3. Acesse o formulário de frequência: https://forms.gle/J62kmQZrQZkA6VjXA
4. Preencha seus dados (Nome, Matrícula, E-mail), cole o seu Contract ID e o link do seu Fork.

Obrigado por participar e desbravar a Web3 conosco!
