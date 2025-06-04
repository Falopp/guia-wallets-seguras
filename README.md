# 🛡️ Guía Avanzada para la Creación Segura de Wallets Cripto

> **Objetivo:** describir paso a paso un flujo de generación, almacenamiento y restauración de frases semilla, usando entornos “air-gapped” y rutas de derivación estándar.

---

## 📋 Índice

1. [Entornos seguros](#entornos-seguros)
2. [Generación offline de la frase semilla](#generación-offline-de-la-frase-semilla)
3. [Rutas de derivación (BIP)](#rutas-de-derivación-bip)
4. [Implementación en wallets populares](#implementación-en-wallets-populares)
5. [Estrategia de almacenamiento y separación de fondos](#estrategia-de-almacenamiento-y-separación-de-fondos)
6. [Verificación periódica de restauración](#verificación-periódica-de-restauración)
7. [Checklist rápido y mantenimiento](#checklist-rápido-y-mantenimiento)

---

## Entornos seguros

| Sistema | Caso de uso | Ventajas clave |
|---------|-------------|----------------|
| **Tails OS** | Sesiones puntuales sin dejar rastro | RAM-only, sin persistencia, ideal para operaciones offline |
| **GrapheneOS (Google Pixel)** | Uso diario con alta seguridad móvil | Refuerzos de kernel, sandbox reforzado, actualizaciones rápidas |

---

## Generación offline de la frase semilla

1. **Aísla el equipo** – Desconéctalo de la red y desactiva radios (Wi-Fi/Bluetooth).  
2. **Verifica el generador** – Descarga `bip39-standalone.html` desde una fuente confiable y comprueba su firma PGP/SHA-256.  
3. **Genera la semilla (24 palabras)** – Ejecuta el archivo **sin conexión**.  
4. **Respaldo físico** – Graba la semilla en placas metálicas resistentes a 🔥 y 💧. Evita fotos, cloud, USB, etc.  

> **Tip:** Usa un generador de dados (entropy dice) si quieres entropía “manual” 100 % verificable.

---

## Rutas de derivación (BIP)

| BIP | Propósito | Ejemplo de ruta | Cuándo usar |
|-----|-----------|-----------------|-------------|
| **BIP44** | Multicoin estándar | `m/44'/60'/0'/0/0` (ETH) | Ethereum, ERC-20, y mayoría de altcoins |
| **BIP49** | Bitcoin SegWit (P2SH) | `m/49'/0'/0'/0/0` | Compatibilidad con wallets legacy |
| **BIP84** | Bitcoin Native SegWit (bech32) | `m/84'/0'/0'/0/0` | Tarifa más baja y direcciones bc1 |
| **Electrum (BIP32)** | Esquema propio | se genera internamente | Flexible, permite añadir passphrase |

---

## Implementación en wallets populares

| Wallet | Bitcoin | Ethereum | Notas |
|--------|---------|----------|-------|
| **Electrum** | BIP49 / BIP84 + passphrase opcional | Importa BIP39 (12/24) | Perfecto para operaciones en Tails |
| **Ledger / Trust Wallet** | BIP49 / BIP84 | BIP44 | Amplia compatibilidad e interfaz móvil |
| **MetaMask** | — | BIP44 (`m/44'/60'/…`) | Para dApps y DeFi, añade hardware-wallet para firmar |

---

## Estrategia de almacenamiento y separación de fondos

| Placa | Semilla | Derivación | Uso sugerido |
|-------|---------|------------|--------------|
| 1 | 12 palabras | **BIP84** (Bitcoin) | Ahorro BTC a largo plazo en Electrum + passphrase |
| 2 | 24 palabras | **BIP44** (Ethereum) | ETH + ERC-20 (Ledger / MetaMask) |
| 3 | — | — | Libre para futuros activos |
| 4 | — | — | Copia de seguridad cifrada en otro lugar físico |

> Mantén la **passphrase** escrita aparte (u otro método mnemónico) y nunca junto a la semilla.

---

## Verificación periódica de restauración

1. **Electrum (BTC)**  
   `File → New/Restore → I already have a seed` → ingresa semilla + passphrase → verifica balance.

2. **Trust Wallet / MetaMask (ETH)**  
   *Settings → Import wallet* → ingresa 12/24 palabras → revisa que aparezcan cuentas y tokens.

Repite cada 3-6 meses para asegurar que la copia de seguridad sigue íntegra.

---

## Checklist rápido y mantenimiento

- [ ] Generar semilla offline y verificar integridad del generador.  
- [ ] Grabar semilla en placas metálicas; guardar en caja fuerte resistente a fuego + agua.  
- [ ] Guardar passphrase en ubicación distinta (o método mnemónico personal).  
- [ ] Configurar wallets: Electrum (BTC BIP84), MetaMask/Trust (ETH BIP44).  
- [ ] Probar restauración en entorno seguro.  
- [ ] Actualizar software (Tails, GrapheneOS, wallets) trimestralmente.  
- [ ] Revisar backups y acceso cada 6 meses.

> **Recuerda:** la seguridad perfecta no existe, pero los múltiples niveles (offline, hardware, redundancia física) reducen drásticamente los vectores de riesgo.

---

### 🏁 Conclusión

Siguiendo este flujo tendrás un setup robusto: semillas generadas offline, rutas de derivación estándar y respaldos físicos resistentes. Mantén disciplina operativa y revisiones periódicas para proteger tu patrimonio digital a largo plazo. ¡Buena custodia!
