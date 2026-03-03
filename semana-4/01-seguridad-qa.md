# Semana 4 · Sesión 1 — Seguridad y QA

**Fecha:** 23 de marzo  
**Instructor:** Gerardo Vela  
**Tema:** Iteración técnica, QA, pruebas de estrés y seguridad básica en contratos inteligentes.

---

## Objetivos de la sesión

- Revisar buenas prácticas de seguridad en Solidity.
- Aplicar QA e iteración técnica a tu MVP.
- Conocer pruebas de estrés y límites del sistema.

---

## 1. Seguridad básica en contratos

### Vulnerabilidades frecuentes

| Riesgo | Descripción | Mitigación |
|--------|-------------|------------|
| **Reentrancy** | Llamada externa antes de actualizar estado | Checks-Effects-Interactions, ReentrancyGuard |
| **Overflow/Underflow** | Solidity 0.8+ revierte por defecto | Usar `uint256` y tipos adecuados |
| **Acceso indebido** | Funciones críticas sin restricción | `onlyOwner`, roles (OpenZeppelin AccessControl) |
| **Front-running** | Tx vista en mempool y copiada | Límites de slippage, commits, MEV consideraciones |
| **Datos de entrada** | Parámetros no validados | Validar rangos, direcciones != address(0) |

### Herramientas

- **Slither:** análisis estático (Python).
- **Foundry:** `forge test`, fuzzing con `forge test --match-test Fuzz`.
- **Manual:** revisión de flujos de fondos y permisos.

---

## 2. QA e iteración

- **Checklist funcional:** cada flujo de usuario (conectar, leer, escribir) funciona en Fuji.
- **Tests automatizados:** al menos tests unitarios para lógica crítica del contrato.
- **Gas:** revisar coste de funciones clave; optimizar si es necesario para UX.

---

## 3. Pruebas de estrés

- Objetivo: ver comportamiento bajo carga (muchas transacciones, usuarios simultáneos).
- **Foundry:** muchos `vm.prank` y múltiples txs en un test.
- **Scripts:** enviar múltiples txs desde script (ethers/viem) contra Fuji o red local.
- Interpretar: tiempos de confirmación, errores, límites de RPC.

---

## Checklist pre–Demo Day

- [ ] Contrato(s) revisados con enfoque en reentrancy, permisos e inputs.
- [ ] Tests pasando (Foundry o Hardhat).
- [ ] Frontend probado de punta a punta en Fuji.
- [ ] Lista de “known issues” o mejoras futuras para la presentación.

---

## Enlaces útiles

- [Smart Contract Security — Consensys](https://consensys.github.io/smart-contract-best-practices/)
- [Slither](https://github.com/crytic/slither)
- [Foundry — Fuzzing](https://book.getfoundry.sh/forge/fuzz-testing)
- [OpenZeppelin Contracts](https://docs.openzeppelin.com/contracts/)

[← Frontend](../semana-3/02-frontend-indexacion.md) · [Volver al índice](../../README.md) · [Siguiente: Demo Day →](./02-demo-day.md)
