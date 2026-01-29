# 💎 Sats Arbitrage Scanner

**Herramienta para encontrar oportunidades de arbitrage en inscripciones ordinales.**

## 🎯 Concepto

El scanner busca inscripciones baratas ($1-10) en Magic Eden que contienen sats valiosos "atrapados". El sat dentro de una inscripción puede valer mucho más que el precio de listing.

**Ejemplo:** Una inscripción listada a $5 podría contener un sat raro que vale $500+ → **Profit: $495**

## 🔍 Tipos de Sats Valiosos

### Por Rareza (Ordinals Theory)
- **⚫ MYTHIC** - Sat #0 (genesis) - Est. $1M+
- **🟣 LEGENDARY** - Primer sat de cada ciclo (~24 años) - Est. $100K+
- **🔴 EPIC** - Primer sat de cada halving (~4 años) - Est. $10K-$50K
- **🟠 RARE** - Primer sat de difficulty adjustment - Est. $500-$5K
- **🟡 UNCOMMON** - Primer sat de cada bloque - Est. $50-$500
- **⚪ COMMON** - Todos los demás - $0

### Por Atributos Especiales
- **🍕 Pizza Sats** - Block 57,043 (Laszlo's pizza, May 2010) - Est. $1K-$10K
- **👤 Nakamoto Era** - Bloques 1-54,316 (minados por Satoshi) - Est. $200-$2K
- **🦋 Palindromes** - Números palíndromos (12321, etc.) - Est. $100-$1K
- **🕰️ Vintage** - Primeros 1000 bloques (2009) - Est. $50-$500
- **⚡ SegWit** - Block 477,120 (activación SegWit) - Est. $150+
- **💎 Block 9** - Primera transacción Satoshi → Hal Finney - Est. $300+

## ⚙️ Cómo Funciona

1. **Escanea Magic Eden** - Busca listings en el rango de precio configurado (default $1-10)
2. **Extrae sat numbers** - Identifica el sat específico de cada inscripción
3. **Analiza rareza** - Usa la lógica de `sat-mining.html` para calcular rareza ordinal
4. **Detecta atributos** - Identifica Pizza sats, Nakamoto era, palindromos, etc.
5. **Calcula valor** - Estima el valor del sat basado en rareza y atributos
6. **Muestra profit** - `profit = valor estimado sat - precio listing`
7. **Auto-refresh** - Se actualiza cada 5 minutos para cazar nuevas oportunidades

## 🚀 Uso

### Acceso
- Dashboard: Click en **💎 ARBITRAGE**
- Directo: `dashboard/sats-arbitrage.html`

### Filtros
- **Min/Max Price** - Rango de precio en USD (default $1-$10)
- **BTC Price** - Precio de Bitcoin para conversión a sats (default $100K)
- **Show All** - Mostrar todas las inscripciones, incluso sin profit

### Stats
- **Scanned** - Número de inscripciones analizadas
- **Opportunities** - Cuántas tienen profit potencial
- **Best Profit** - Mayor ganancia posible en el scan actual
- **Last Scan** - Timestamp del último scan + countdown para próximo

### Resultados
Cada oportunidad muestra:
- Número de inscripción
- Badge de rareza (Mythic, Epic, Rare, etc.)
- Sat number
- Atributos especiales (Pizza, Nakamoto, Palindrome, etc.)
- Precio de listing vs valor estimado
- **Profit potencial** ($ y %)
- Link directo a Magic Eden para comprar

## 🔧 Implementación Técnica

### Reutilización de Código
Usa las funciones de `sat-mining.html`:
- `blockFromSat()` - Calcula el bloque de un sat
- `firstSatOfBlock()` - Primer sat de un bloque
- `getSatRarity()` - Determina rareza ordinal
- `getSpecialAttributes()` - Detecta atributos especiales
- `isPalindrome()` - Verifica si es palíndromo

### Magic Eden API
```javascript
GET https://api-mainnet.magiceden.dev/v2/ord/btc/tokens
  ?limit=100
  &offset=0
  &minPrice=100000    // 100K sats ≈ $1 @ $100K BTC
  &maxPrice=1000000   // 1M sats ≈ $10 @ $100K BTC
```

**Nota:** Por CORS, en producción necesitaría un proxy backend. Actualmente usa datos simulados para testing.

### Valores Estimados (Conservadores)
Los valores son estimaciones basadas en:
- Rareza ordinal según Ordinals Theory
- Ventas históricas de sats especiales
- Demanda del mercado por atributos específicos
- Estimaciones conservadoras (no infladas)

## ⚠️ Disclaimer

**Esta herramienta es educativa y experimental:**
- Los valores estimados son conservadores pero NO garantizados
- El mercado de ordinals es volátil y especulativo
- Siempre DYOR (Do Your Own Research) antes de comprar
- No hay garantía de que puedas vender un sat al precio estimado
- Compra bajo tu propio riesgo

## 🛠️ Futuras Mejoras

- [ ] Integrar API real de Magic Eden (con proxy backend)
- [ ] Datos de ventas históricas reales para valuaciones más precisas
- [ ] Filtros adicionales (tipos de rareza, atributos específicos)
- [ ] Notificaciones push cuando aparece una oportunidad muy buena
- [ ] Tracking de oportunidades pasadas (cuántas se vendieron, a qué precio)
- [ ] Integración con wallet para compra directa
- [ ] Charts de precio histórico por tipo de rareza
- [ ] Comparación con otros marketplaces (Unisat, Ordinals Wallet, etc.)

## 📊 Repo

- **Branch:** `dev-sats-arbitrage`
- **Archivos:** `sats-arbitrage.html`, `SATS-ARBITRAGE.md`
- **Pull Request:** Ready for review & merge to main

---

Built by **Jack 🔧** for Harto Strategy
