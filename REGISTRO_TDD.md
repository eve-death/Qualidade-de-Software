# Registro do ciclo de TDD

## Comportamento escolhido

Cobrar a taxa de entrega de R$ 5 para distancia de ate 3 km (2 km e pedido de R$ 50). Em seguida, o mesmo ciclo foi repetido para as demais regras (ciclos 2, 3 e 4 abaixo).

## Red

**Teste criado:** `test_cobra_taxa_fixa_ate_3_km`

**Motivo da falha:** a funcao `calcular_taxa_entrega` ainda nao existia em `src/pedido.py`, entao o import falhou (`ImportError: cannot import name 'calcular_taxa_entrega'`).

## Green

**Implementacao realizada:** funcao criada retornando fixo `5`, que e o minimo para o teste passar.

## Refactor

**Melhoria realizada:** ao final dos quatro ciclos, os numeros fixos (5, 3, 2 e 100) foram substituidos por constantes nomeadas (`TAXA_BASE`, `KM_INCLUIDOS_NA_TAXA_BASE`, `TAXA_POR_KM_EXCEDENTE`, `PEDIDO_MINIMO_ENTREGA_GRATIS`), os km excedentes passaram a ser calculados com `max(0, ...)` e foi adicionada docstring. O comportamento nao mudou.

**Resultado final:** toda a suite passa (8 testes).

---

## Demais ciclos

| Ciclo | Teste | Red (falha) | Green (implementacao minima) |
|-------|-------|-------------|------------------------------|
| 2 | `test_acrescenta_valor_por_km_excedente_acima_de_3_km` (4 km, R$ 50 -> R$ 7) | `assert 5 == 7` | `if distancia_km > 3: return 5 + (distancia_km - 3) * 2` |
| 3 | `test_entrega_gratuita_para_pedido_a_partir_de_100` (5 km, R$ 100 -> R$ 0) | `assert 9 == 0` | `if total_pedido >= 100: return 0` antes do calculo |
| 4 (opcional) | `test_rejeita_distancia_negativa` | `DID NOT RAISE ValueError` | `if distancia_km < 0: raise ValueError(...)` |
