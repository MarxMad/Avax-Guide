# Semana 3 · Sesión 2 — Frontend e indexación

**Fecha:** 18 de marzo  
**Instructor:** Invitado Team1  
**Tema:** Workshop de desarrollo, integración de Frontend (Ethers.js / Viem) y setup de indexación.

---

## Objetivos de la sesión

- Conectar tu dApp al C-Chain (Fuji/Mainnet) desde el navegador.
- Usar **Ethers.js** o **Viem** para leer contratos y enviar transacciones.
- Configurar indexación básica (eventos, historial) para mejor UX.

---

## 1. Frontend con Ethers.js o Viem

### Por qué Ethers o Viem

- **Ethers.js:** ampliamente usado, documentación extensa, soporte wallets (MetaMask, Core).
- **Viem:** más moderno, TypeScript-first, tree-shakeable; ideal para nuevos proyectos.

### Conexión a Avalanche (Fuji)

```javascript
// Ethers v6
import { ethers } from 'ethers';

const provider = new ethers.JsonRpcProvider(
  'https://api.avax-test.network/ext/bc/C/rpc'
);
const signer = await provider.getSigner(); // con wallet conectada

// Viem
import { createPublicClient, createWalletClient, http } from 'viem';
import { avalancheFuji } from 'viem/chains';

const client = createPublicClient({
  chain: avalancheFuji,
  transport: http(),
});
```

### Leer un contrato

- ABI del contrato + dirección desplegada.
- Llamadas `view`/`pure` con `contract.metodo()` (ethers) o `readContract` (viem).
- Enviar transacciones con `signer` (ethers) o `writeContract` (viem).

---

## 2. Conectar wallet (Core / MetaMask)

- **Inyected provider:** `window.ethereum` (Core y MetaMask lo exponen).
- Solicitar cuentas: `eth_requestAccounts`.
- Cambiar a Fuji: Chain ID `43113`; agregar red si el usuario no la tiene.

Documentación: [Core — Add to Wallet](https://docs.core.app/core-extension/add-to-core/) (agregar Avalanche Fuji).

---

## 3. Indexación básica

- **Para qué:** listar eventos, historial, balances sin escanear cada bloque.
- **Opciones:**
  - **The Graph:** subgraphs para Avalanche (C-Chain y subnets).
  - **Snowtrace API:** si solo necesitas datos de una dirección o contrato en C-Chain.
  - **Eventos en frontend:** filtrar `contract.queryFilter(evento, fromBlock, toBlock)` (ethers) para MVPs simples.

Para el MVP suele bastar con leer eventos recientes o usar Snowtrace; The Graph se considera para producción.

---

## Checklist

- [ ] Proyecto frontend (React/Vite o similar) con Ethers o Viem.
- [ ] Conexión a Fuji y lectura de un contrato desplegado.
- [ ] “Conectar wallet” y cambio a red Fuji.
- [ ] (Opcional) Listar eventos o datos indexados del contrato.

---

## Enlaces útiles

- [Ethers.js v6](https://docs.ethers.org/v6/)
- [Viem](https://viem.sh/) · [Viem — Avalanche chains](https://viem.sh/docs/chains.html)
- [The Graph — Avalanche](https://thegraph.com/docs/en/supported-networks/avalanche/)
- [Snowtrace](https://snowtrace.io/) · [Fuji Snowtrace](https://testnet.snowtrace.io/)

[← Lean Canvas](./01-lean-canvas-equipos.md) · [Volver al índice](../../README.md) · [Siguiente: Seguridad y QA →](../semana-4/01-seguridad-qa.md)
