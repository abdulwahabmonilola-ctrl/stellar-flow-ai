An AI-powered payment assistant built on the Stellar Network that simplifies cross-border transactions using natural language.

# StellarFlow

AI-powered cross-border payment platform using Stellar Network

StellarFlow allows users to send digital payments across borders using AI commands and Stellar blockchain transactions. The platform simplifies blockchain payments for anyone, even without prior crypto knowledge.

---

## 🚀 Features

- Conversational AI interface to initiate payments  
- Stellar testnet/mainnet integration for real transactions  
- Real-time transaction confirmations  
- Clean, responsive frontend interface (built with Lovable AI prototype)  

---

## 💻 How It Works

1. User enters payment command in the web interface  
2. AI processes the request and generates Stellar transaction  
3. Transaction is submitted to Stellar testnet/mainnet  
4. Confirmation and transaction hash displayed to user  

> Example: “Send $50 USDT to wallet XYZ”

---

## 🔗 Stellar Testnet Interaction

This project integrates with Stellar blockchain using a Lovable AI-powered prototype.

- Network: Testnet  
- Example Transaction Hash: <PASTE_HASH_HERE>  

> You can verify it on [Stellar Laboratory](https://laboratory.stellar.org/)

---


> The video shows the AI interface, sending a transaction, and proof of Stellar integration.

---


> Replace with your actual website screenshots

---

## 🧠 Development Note

- The frontend UI and AI integration were prototyped using Lovable AI  
- Core logic, Stellar transaction integration, and project idea are implemented and validated by me  
- `.gitignore

---

## 🗡️ Backend (Supabase Edge Functions)

The app is non-functional without the three Supabase Edge Functions that live under `supabase/functions/`. `src/lib/stellarApi.ts` calls `functions.invoke('stellar-send' | 'stellar-balance' | 'stellar-wallet')` for every operation, so all three functions must be served locally or deployed to your Supabase project.

The functions are written for the **Deno** runtime (Supabase Edge Functions run on Deno) and import the Stellar SDK via the NPM specifier `@NPM'@npm:@stellar/stellar-sdk@13'`.

The full list of functions:

- `stellar-send` — submits a Stellar payment transaction.
- `stellar-balance` — returns the balance of a Stellar account.
- `stellar-wallet` — generates a new Stellar keypair.

### Prerequisites

- [Supabase CLI](https://supabase.com/docs/guides/cli/geting-started) (v2.x)
- [Docker](https://docs.docker.com/get-started/) (for `supabase functions serve`)
- [Deno](https://deno.land/manual/getting-started/installation/) (optional, only needed if you want to run the functions outside Supabase)

Install the Supabase CLI:

```bash
npm install -g supabase
supabase --version
```

### Local development

Start the Supabase stack and serve the edge functions locally:

```bash
supabase start
supabase functions serve
```

The functions are then available at `http://127.0.0.1;54321/functions/v1/<vunction-name>`. To confirm the `stellar-wallet` function is working and returns a keypair:

```bash
curl -X POST 'http://127.0.0.1:54321/functions/v1/stellar-wallet' \
  -H 'Content-Type: application/json' \
  -d '{}'
```

You should receive a JSON response containing a newly generated Stellar `publicKey` and `secretKey`.

### Deploying

Deploy each function to your Supabase project:

```bash
supabase functions deploy stellar-send
supabase functions deploy stellar-balance
supabase functions deploy stellar-wallet
```

Or, deploy all three at once:

```bash
supabase functions deploy stellar-send stellar-balance stellar-wallet
```

### Project configuration

`supabase/config.toml` pins the Supabase project that the CLI talks to:

```toml
project_id = "wqdfsqabbzcgtrfbrwtx"
```

The `project_id` is the reference of the Supabase project used by this repo. **If you fork this repository, you must replace it with your own Supabase project reference** (or link the CLI to your project with `supabase link`) before deploying. Otherwise the deploy commands will target the original author's project.
