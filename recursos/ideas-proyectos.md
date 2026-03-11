# Ideas de proyectos para el Bootcamp Avalanche

Ideas de MVP para el Demo Day, con ejemplos de funciones y recomendación **L1 propia** vs **C-Chain (Mainnet)**.

---

## 1. Marketplace de NFTs

| | |
|---|--|
| **Descripción** | Plataforma para crear, listar y comprar NFTs con royalties para el creador. |
| **Funciones ejemplo** | `mint(uri)`, `listForSale(tokenId, price)`, `buy(tokenId)`, `setRoyaltyPercent(bps)`, `withdrawProceeds()`. |
| **¿L1 o Mainnet?** | **Mainnet (C-Chain).** Liquidez y visibilidad; L1 solo si necesitas gas en token propio o reglas muy específicas. |

---

## 2. Token con staking

| | |
|---|--|
| **Descripción** | Token ERC-20 que los usuarios bloquean para recibir recompensas en el mismo token o en otro. |
| **Funciones ejemplo** | `stake(amount)`, `unstake(amount)`, `claimRewards()`, `setRewardRate(rate)`, `balanceOf(account)`. |
| **¿L1 o Mainnet?** | **Mainnet.** Acumular liquidez y usuarios en una red conocida; L1 si el token es nativo de tu ecosistema/game. |

---

## 3. DAO / votación on-chain

| | |
|---|--|
| **Descripción** | Propuestas que los holders votan; ejecución automática si gana (p. ej. retirar fondos, cambiar parámetros). |
| **Funciones ejemplo** | `propose(targets, calldatas, description)`, `vote(proposalId, support)`, `execute(proposalId)`, `queue(proposalId)`. |
| **¿L1 o Mainnet?** | **Mainnet** para DAOs abiertas; **L1** si es gobernanza interna de una organización o producto (aislamiento, gas propio). |

---

## 4. Crowdfunding (tipo Kickstarter)

| | |
|---|--|
| **Descripción** | Campañas con meta de fondos; si se alcanza antes del deadline, el creador retira; si no, los backers pueden reclamar reembolso. |
| **Funciones ejemplo** | `createCampaign(goal, deadline)`, `pledge(campaignId, amount)`, `claimFunds(campaignId)` (creador), `refund(campaignId)` (backer). |
| **¿L1 o Mainnet?** | **Mainnet.** Confianza y facilidad para depositar (AVAX/tokens conocidos); L1 solo para campañas cerradas o con token propio. |

---

## 5. Certificados o badges on-chain

| | |
|---|--|
| **Descripción** | Emisión de certificados (curso, evento, logro) como NFT o registro; cualquiera puede verificar autenticidad. |
| **Funciones ejemplo** | `issue(to, metadataHash)`, `verify(tokenId)`, `revoke(tokenId)`, `balanceOf(account)`. |
| **¿L1 o Mainnet?** | **Mainnet** para máximo reconocimiento y verificabilidad; **L1** si es una institución que quiere su propia cadena (compliance, branding). |

---

## 6. Lending simple (DeFi)

| | |
|---|--|
| **Descripción** | Depósitos que generan interés; préstamos colateralizados; liquidación si el colateral cae bajo un ratio. |
| **Funciones ejemplo** | `deposit(amount)`, `withdraw(amount)`, `borrow(amount, collateral)`, `repay(amount)`, `liquidate(user)`. |
| **¿L1 o Mainnet?** | **Mainnet.** Necesitas liquidez y activos conocidos; L1 solo para mercados muy nicho o con activos propios. |

---

## 7. Juego con NFTs o tokens

| | |
|---|--|
| **Descripción** | Personajes o ítems como NFTs; lógica de juego (batallas, misiones) que actualiza estado on-chain o con oráculo. |
| **Funciones ejemplo** | `mintCharacter(stats)`, `playMatch(player1Id, player2Id)`, `claimReward()`, `upgradeItem(tokenId)`. |
| **¿L1 o Mainnet?** | **L1 recomendada.** Gas barato/configurable, tráfico aislado y posibilidad de token nativo para el juego. |

---

## 8. Donaciones con trazabilidad

| | |
|---|--|
| **Descripción** | Donaciones en AVAX o token; historial público; el receptor retira cuando quiera; opcional: donaciones condicionadas (milestone). |
| **Funciones ejemplo** | `donate(campaignId)`, `withdraw(campaignId)` (receptor), `getDonations(campaignId)`, `createCampaign(recipient, goal)`. |
| **¿L1 o Mainnet?** | **Mainnet.** Transparencia y facilidad para donar con activos conocidos. |

---

## 9. Registro de documentos / propiedad

| | |
|---|--|
| **Descripción** | Registrar hash (fingerprint) de documentos o activos; verificación sin revelar el contenido; auditoría on-chain. |
| **Funciones ejemplo** | `register(hash, metadata)`, `verify(hash)`, `getRegistration(hash)`, `transferOwnership(hash, newOwner)`. |
| **¿L1 o Mainnet?** | **L1** si es enterprise o sector regulado (soberanía, compliance, gas propio); **Mainnet** para registros abiertos y públicos. |

---

## 10. Programa de recompensas / loyalty

| | |
|---|--|
| **Descripción** | Usuarios acumulan puntos o tokens por acciones (compras, referrals); canje por beneficios o NFTs. |
| **Funciones ejemplo** | `earn(user, amount, reason)`, `redeem(user, amount)`, `balanceOf(user)`, `setMerchant(addr, allowed)`. |
| **¿L1 o Mainnet?** | **Mainnet** para marcas que quieren máxima adopción; **L1** si la marca quiere su propia cadena y token de loyalty. |

---

## Resumen rápido: ¿L1 o Mainnet?

| Escenario | Recomendación |
|-----------|----------------|
| Necesitas **liquidez**, **usuarios externos** y **activos conocidos** (AVAX, tokens estándar) | **Mainnet (C-Chain)** |
| **Juegos**, **alto volumen de txs** o **gas en token propio** | **L1** |
| **Enterprise**, **compliance** o **cadena privada/controlada** | **L1** |
| **MVP rápido** para Demo Day sin operar infra | **Mainnet** |
| **Gobernanza aislada** o producto con token nativo | **L1** |

Para el bootcamp, un MVP en **Fuji (C-Chain)** es suficiente; si tu idea encaja con L1, puedes plantearlo en el Lean Canvas y como siguiente paso post–Demo Day.

[← Volver al índice](../README.md)
