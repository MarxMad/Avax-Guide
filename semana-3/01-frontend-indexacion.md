# Semana 3 · Sesión 1 — Frontend, indexación y prototipado

**Fecha:** 16 de marzo  
**Instructor:** Gerardo Vela  
**Tema:** Prototipo desde V0: contrato con Foundry, despliegue en Fuji, integración frontend (Ethers/Viem) con Cursor o Antigravity.

---

## Objetivos de la sesión

- Arrancar el **prototipo desde V0**: contrato mínimo → desplegar con **Foundry** en Fuji → frontend que lo use.
- Escribir y desplegar contratos con Foundry; usar **Cursor** (o Antigravity) para acelerar la integración y el código del frontend.
- Conectar un frontend mínimo a la C-Chain (Fuji), leer y escribir en tu contrato, y conectar wallet (Core / MetaMask).

---

## 1. Prototipo V0 — Flujo en 4 pasos

1. **Contrato mínimo** en Foundry (Solidity).
2. **Desplegar a Fuji** con `forge create` o script.
3. **Frontend mínimo** (React + Vite + Ethers) que lee y escribe en ese contrato.
4. **Conectar wallet** y probar en Fuji.

Herramientas recomendadas para codear rápido: **Cursor** (IDE con IA) para contratos y frontend; **Antigravity** si lo usas para vibe coding / flujo de desarrollo.

---

## 2. V0 — Paso 1: Contrato mínimo con Foundry

### Inicializar proyecto Foundry

```bash
forge init avax-v0 --no-commit
cd avax-v0
```

### Contrato mínimo (ejemplo)

Crea o edita `src/HolaAvalanche.sol`:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

contract HolaAvalanche {
    string public mensaje = "Hola Avalanche desde CriptoUNAM";

    function actualizarMensaje(string calldata _nuevo) external {
        mensaje = _nuevo;
    }
}
```

Compilar y comprobar:

```bash
forge build
```

---

## 3. V0 — Paso 2: Desplegar en Fuji con Foundry

### Variables de entorno

Crea `.env` en la raíz del proyecto (y añade `.env` al `.gitignore`):

```
PRIVATE_KEY=tu_clave_privada_sin_0x
```

### Despliegue con forge create

```bash
forge create src/HolaAvalanche.sol:HolaAvalanche \
  --rpc-url https://api.avax-test.network/ext/bc/C/rpc \
  --private-key $PRIVATE_KEY
```

Anota la **dirección del contrato** que imprime el comando. Verifica la tx en [Fuji Snowtrace](https://testnet.snowtrace.io/).

### (Opcional) Script de deploy

Puedes usar un script para reutilizar el deploy:

```bash
forge script script/Deploy.s.sol --rpc-url https://api.avax-test.network/ext/bc/C/rpc --broadcast --private-key $PRIVATE_KEY
```

Con eso tienes **contrato en Fuji** y dirección lista para el frontend.

---

## 4. V0 — Paso 3: Frontend mínimo (React + Vite + Ethers)

### Crear proyecto

```bash
npm create vite@latest avax-v0-frontend -- --template react
cd avax-v0-frontend
npm install
npm install ethers
```

### Configuración Fuji

- **RPC:** `https://api.avax-test.network/ext/bc/C/rpc`
- **Chain ID:** `43113`

### Leer y escribir en el contrato

Necesitas la **dirección** del contrato desplegado y el **ABI**. Con Foundry puedes copiar el ABI desde `out/HolaAvalanche.sol/HolaAvalanche.json` (campo `abi`) o exportarlo:

```bash
forge inspect HolaAvalanche abi
```

Ejemplo mínimo en tu app (ajusta `CONTRACT_ADDRESS`):

```javascript
import { ethers } from 'ethers';

const FUJI_RPC = 'https://api.avax-test.network/ext/bc/C/rpc';
const FUJI_CHAIN_ID = 43113;
const CONTRACT_ADDRESS = '0x...'; // la que te dio forge create

const ABI = [
  'function mensaje() view returns (string)',
  'function actualizarMensaje(string)',
];

// Solo lectura
const provider = new ethers.JsonRpcProvider(FUJI_RPC);
const contract = new ethers.Contract(CONTRACT_ADDRESS, ABI, provider);
const mensaje = await contract.mensaje();

// Escritura (con wallet conectada)
const signer = await new ethers.BrowserProvider(window.ethereum).getSigner();
const contractWrite = new ethers.Contract(CONTRACT_ADDRESS, ABI, signer);
const tx = await contractWrite.actualizarMensaje('Nuevo mensaje');
await tx.wait();
```

Usa **Cursor** (o Antigravity) para generar los componentes React que llamen a estas funciones (botón conectar wallet, mostrar `mensaje`, input + botón para `actualizarMensaje`).

---

## 5. V0 — Paso 4: Conectar wallet y cambiar a Fuji

- Llamar `eth_requestAccounts` para conectar.
- Cambiar a Fuji con `wallet_switchEthereumChain` (chainId `43113`); si la red no existe, usar `wallet_addEthereumChain` con el RPC y block explorer de Fuji.

Ejemplo de cambio a Fuji (Ethers v6):

```javascript
await window.ethereum.request({
  method: 'wallet_switchEthereumChain',
  params: [{ chainId: ethers.toQuantity(43113) }],
});
```

Si falla con código 4902, añade la red con `wallet_addEthereumChain` (mismo RPC y [testnet.snowtrace.io](https://testnet.snowtrace.io/) como blockExplorerUrls).

---

## 6. Stack recomendado para el prototipo

| Capa | Recomendado |
|------|-------------|
| **Contratos** | Foundry (escribir, compilar, desplegar) |
| **Frontend** | React + Vite + Ethers.js v6 |
| **IDE / flujo** | Cursor (o Antigravity para vibe coding) |
| **Wallet** | Core / MetaMask (window.ethereum) |
| **Red** | Fuji (C-Chain) |

---

## 7. Indexación básica (opcional para V0)

Para listar eventos sin escanear todos los bloques:

- **Eventos con Ethers:** `contract.queryFilter(filter, fromBlock, 'latest')` si tu contrato emite eventos.
- **Snowtrace:** para consultas puntuales (balance, historial).
- **The Graph:** para más adelante cuando necesites queries complejas.

---

## 8. Entregables de esta sesión (V0)

- [ ] Proyecto **Foundry** con contrato mínimo y **desplegado en Fuji**.
- [ ] Proyecto **React + Vite + Ethers** que **lee** y **escribe** en ese contrato.
- [ ] **Conectar wallet** y cambio a **Fuji** desde la UI.
- [ ] (Opcional) Usar **Cursor** o **Antigravity** para generar o refactorizar la integración frontend.

---

## Checklist técnico

- [ ] Foundry: `forge build` y `forge create` a Fuji con contrato desplegado.
- [ ] Frontend: provider Fuji, contrato con dirección + ABI, lectura (view) y una tx (write).
- [ ] Botón “Conectar wallet” y cambio a red Fuji.
- [ ] Enlace a la tx o contrato en Fuji Snowtrace.

---

## Enlaces útiles

- [Foundry Book](https://book.getfoundry.sh/)
- [Ethers.js v6](https://docs.ethers.org/v6/)
- [Core Wallet](https://core.app/)
- [Fuji Snowtrace](https://testnet.snowtrace.io/)
- [Cursor](https://cursor.com/) · Antigravity (vibe coding / flujo de desarrollo)

[← Teleporter](../semana-2/02-teleporter-awm.md) · [Volver al índice](../../README.md) · [Siguiente: Lean Canvas y equipos →](./02-lean-canvas-equipos.md)
