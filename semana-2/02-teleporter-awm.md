# Semana 2 · Sesión 2 — Teleporter y Avalanche Warp Messaging

**Fecha:** 11 de marzo  
**Instructor:** Andrés Rodriguez  
**Tema:** Interoperabilidad con Teleporter y comunicación Cross-Chain nativa (AWM).

---

## Objetivos de la sesión

- Entender la comunicación entre cadenas en Avalanche.
- Conocer **Avalanche Warp Messaging (AWM)** como capa nativa.
- Usar **Teleporter** para enviar mensajes y llamadas entre subnets/EVM.

---

## 1. Interoperabilidad en Avalanche

- Las subnets y la Red Primaria pueden comunicarse entre sí.
- **AWM** permite mensajes firmados entre blockchains sin puentes externos de terceros.
- **Teleporter** es un protocolo construido sobre AWM para dApps (mensajes y contratos).

---

## 2. Avalanche Warp Messaging (AWM)

- Mensajes firmados por validadores que pueden ser verificados en la cadena destino.
- Nativo del consenso Avalanche; no depende de relays externos.
- Base para Teleporter y otros protocolos cross-chain.

Documentación: [Avalanche Warp Messaging](https://docs.avax.network/dapps/smart-contracts/avalanche-warp-messaging).

---

## 3. Teleporter

- **Qué es:** protocolo para enviar mensajes y llamadas entre subnets (EVM).
- **Casos de uso:** puentes de activos, oráculos cross-chain, gobernanza entre cadenas, etc.
- Flujo alto nivel: contrato origen → mensaje AWM → contrato destino en otra subnet.

### Recursos

- Repositorio y docs: [Teleporter](https://github.com/ava-labs/teleporter)
- Ejemplos de contratos que envían/reciben mensajes Teleporter.

---

## Práctica sugerida

- Revisar un ejemplo de contrato que envía un mensaje con Teleporter.
- Entender el flujo: emisor → AWM → receptor y el papel del relayer (si aplica).
- Anotar diferencias entre “puente tradicional” y AWM/Teleporter.

---

## Checklist

- [ ] Explicar con tus palabras qué es AWM y qué es Teleporter.
- [ ] Haber visto al menos un ejemplo de mensaje cross-chain en la sesión.
- [ ] Saber en qué subnets/RPCs está disponible Teleporter (Fuji, mainnet, custom).

---

## Enlaces útiles

- [Avalanche Warp Messaging](https://docs.avax.network/dapps/smart-contracts/avalanche-warp-messaging)
- [Teleporter — GitHub](https://github.com/ava-labs/teleporter)
- [Teleporter — Docs](https://docs.avax.network/dapps/smart-contracts/teleporter)

[← Subnets y Avalanche9000](./01-subnets-avalanche9000.md) · [Volver al índice](../../README.md) · [Siguiente: Lean Canvas →](../semana-3/01-lean-canvas-equipos.md)
