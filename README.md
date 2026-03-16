# Programs for HP42-S

Compatible with all HP42-S-based calculators, including [Plus42](https://thomasokken.com/plus42/) and SwissMicros DM42/DM42n.

## Usage

Translate using [`txt2raw`](https://thomasokken.com/plus42/#additional) or [SwissMicro's web encoder](https://technical.swissmicros.com/dm42/decoder/).

Import raw file [to Plus42](https://thomasokken.com/free42/importexport.html) or [flash to DM42](https://technical.swissmicros.com/dm42/doc/dm42_user_manual.html#file_menu).

## List of functions

All functions may overwrite or clear the registers `F1`, `F2`, ... `Fn` to store intermediate values.

- [Programming Utilities](#programming-utilities)
- [Arithmetic Operations on Integers](#arithmetic-operations-on-integers)
- [Arithmetic Operations on Fractions](#arithmetic-operations-on-fractions)

### Programming Utilities

| Name | Description | Input Registers | Output Registers | Preserves Stack | Last X |
|------|-------------|-----------------|------------------|-----------------|--------|
| `RGSAVE` | Saves the contents of all stack registers | `X`..`T` | `F-X`..`F-T` | ✅ | Unchanged |
| `RGLOAD` | Overwrite the stack registers from saved state | `F-X`..`F-T` | `X`..`T` | ❌ | Unchanged |
| `RCLEAR` | Clears (`CLV`) the saved stack in registers `F-X`..`F-T` | - | - | ✅ | Unchanged |
| `RCPOP` | A `RGLOAD` followed by a `RGCLEAR` | `F-X`..`F-T` | `X`..`T` | ❌ | Unchanged |

### Arithmetic Operations on Integers

| Name | Description | Input Registers | Output Registers | Preserves Stack | Last X |
|------|-------------|-----------------|------------------|-----------------|--------|
| `GCD` | Computes the greatest common divisor $\gcd(Y, X)$ | `X`, `Y` | `X` | ✅ | $0$ | 
| `LCM` | Computes the least common multiple $\frac{Y*X}{\gcd(Y, X)}$ | `X`, `Y` | `X` | ✅ | Overwritten |
| `?PRIME` | Tests `X` for primality and displays result | `X` | - | ✅ | A factor such that $Last X \mid X $ |
| `FACTOR` | Factor out an $n \mid X$ and store $n$ to `Y` and $X/n$ to `X` | `X` | `X`, `Y` | ❌ | Overwritten |

### Arithmetic Operations on Fractions

| Name | Description | Input Registers | Output Registers | Preserves Stack | Last X |
|------|-------------|-----------------|------------------|-----------------|--------|
| `/EXPAND` | Expands the fraction $\frac{Y}{X}$ by the factor provided as input | `X`, `Y` | `X`, `Y` | `T` only | Expansion factor |
| `/REDUCE` | Reduce/simplify the fraction $\frac{Y}{X}$ | `X`, `Y` | `X`, `Y` | ❌ | $\gcd(Y, X)$ |
| `/ADD` | Add two fractions provided as input (defaults to $\frac{T}{Z}$ and $\frac{Y}{X}$) and save the result as $\frac{Y}{X}$ | `X`..`T` | `X`, `Y` | ❌ | Overwritten |
| `←Ab/c` | Convert the mixed fraction $Z\frac{Y}{X}$ to a proper fraction stored as $\frac{Y}{Z}$ | `X`, `Y`, `Z` | `X`, `Y` | `T` only | Overwritten |
| `→Ab/c` | Convert the fraction $\frac{Y}{X}$ to a mixed fraction stored as $Z\frac{Y}{X}$ | `X`, `Y` | `X`, `Y`, `Z` | ✅ | Overwritten |
| `→a/b` | Convert the decimal number in `X` to a fraction stored as $\frac{Y}{X}$ | `X` | `X`, `Y` | ❌ | Overwritten |
