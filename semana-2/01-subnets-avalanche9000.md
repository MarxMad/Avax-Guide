# Semana 2 · Sesión 1 — Subnets y Avalanche9000

**Fecha:** 9 de marzo  
**Instructor:** Andrés Rodriguez  
**Tema:** Revolución de las L1s, arquitectura Avalanche9000 y lanzamiento de una red personalizada local.

---

## Objetivos de la sesión

- Entender el modelo de subnets y L1s personalizadas en Avalanche.
- Conocer la arquitectura Avalanche9000.
- Lanzar una red personalizada local (Subnet-EVM o similar).

---

## 1. Subnets en Avalanche

- **Subnet:** conjunto de validadores que consensúan un conjunto de blockchains.
- Cada blockchain puede tener sus propias reglas (EVM, AVM, personalizadas).
- Ventajas: soberanía, escalabilidad, gas y gobernanza configurables.

---

## 2. Arquitectura Avalanche9000

- Evolución de la plataforma para mayor rendimiento y flexibilidad.
- Mejoras en throughput, finalidad y experiencia para desarrolladores.
- Base para las próximas generaciones de subnets y L1s.

Documentación oficial recomendada: [Avalanche9000](https://docs.avax.network/) (buscar "Avalanche 9000" o "Subnets").

---

## 3. Red personalizada local

### Opciones típicas

- **Subnet-EVM:** blockchain EVM que corre como subnet.
- **Avalanche CLI** o **AvalancheGo** en modo local para simular una subnet.

### Pasos conceptuales

1. Definir la blockchain (EVM, reglas de gas, etc.).
2. Configurar validadores y subnets (en local: nodos de desarrollo).
3. Lanzar la red y conectar con Core Wallet o Metamask (RPC local).
4. Desplegar contratos en tu L1 local.

Los ejercicios en clase seguirán la guía del instructor con la versión actual de las herramientas.

---

## Checklist

- [ ] Entender diferencia entre P-Chain, X-Chain, C-Chain y una subnet.
- [ ] Haber revisado documentación de Subnets y Avalanche9000.
- [ ] Red local corriendo (según lo visto en sesión).
- [ ] Anotar dudas para la sesión de Teleporter/AWM.

---

## Enlaces útiles

- [Subnets — Docs Avalanche](https://docs.avax.network/subnets)
- [Avalanche CLI](https://github.com/ava-labs/avalanche-cli)
- [Subnet-EVM](https://github.com/ava-labs/subnet-evm)

[← Semana 1](../semana-1/02-c-chain-solidity-fuji.md) · [Volver al índice](../../README.md) · [Siguiente: Teleporter y AWM →](./02-teleporter-awm.md)
