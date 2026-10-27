---
name: calculadora-combustivel
description: Compara etanol e gasolina para veículos flex. Use quando o usuário perguntar "etanol ou gasolina?", "compensa abastecer com álcool?", pedir para comparar preços de combustível, calcular custo por km, economia por viagem ou por mês, ou mencionar a regra dos 70%.
---

# Calculadora de Combustível — Etanol ou Gasolina?

Ajude o usuário a decidir entre etanol e gasolina usando os preços do posto dele e, quando disponível, o rendimento (km/l) do veículo com cada combustível. Nunca consulte preços externos na internet: os preços vêm sempre do usuário. Não exija nenhum cadastro.

## Dados de entrada

Pergunte (ou extraia da mensagem) nesta ordem de prioridade:

1. **Preço do etanol e preço da gasolina** no posto (R$/litro) — obrigatórios.
2. **Rendimento do veículo** com cada combustível (km/l na gasolina e km/l no etanol) — opcionais, mas tornam o cálculo exato. Se o usuário souber só um dos dois, não invente o outro: caia na regra dos 70%.
3. **Distância** da viagem (km) ou quilometragem mensal — opcional, para estimar a economia em reais.

Aceite vírgula decimal (padrão brasileiro): "5,89" = 5.89. Valide que preços e rendimentos são positivos; se algo vier zerado, negativo ou claramente trocado (etanol mais caro que gasolina é possível, mas rendimento de 70 km/l não é plausível), confirme com o usuário antes de calcular.

## Método 1 — Cálculo exato (com os dois rendimentos)

Use sempre que o usuário informar o rendimento com os dois combustíveis:

- custo por km (gasolina) = preço da gasolina ÷ rendimento na gasolina
- custo por km (etanol) = preço do etanol ÷ rendimento no etanol
- **Recomende o combustível de menor custo por km.**
- Diferença percentual = (custo maior − custo menor) ÷ custo maior. Se a diferença for menor que ~2%, trate como empate técnico e diga que tanto faz.

Com distância informada:

- economia por viagem = (custo por km maior − custo por km menor) × km da viagem
- economia mensal = idem, com a quilometragem mensal

Faça os cálculos com precisão (use a ferramenta Bash com `python3 -c "..."` se os números não forem triviais) e apresente custo por km com 3 casas decimais e valores em reais com 2 casas.

## Método 2 — Regra dos 70% (sem os rendimentos)

Quando o usuário não souber os rendimentos, use a regra aproximada: o etanol rende cerca de 70% do que a gasolina rende no mesmo veículo flex.

- razão = preço do etanol ÷ preço da gasolina
- razão **menor que 0,70** → etanol compensa
- razão **maior que 0,70** → gasolina compensa
- razão **igual ou muito próxima de 0,70** (entre ~0,69 e ~0,71) → **empate estimado no limite**: diga que pela regra aproximada é empate e que só os rendimentos reais do veículo decidem

Deixe sempre claro que é uma aproximação: carros flex variam (tipicamente o etanol rende 65%–75% da gasolina), e o resultado pode inverter perto do limite. Ofereça refazer o cálculo exato se o usuário descobrir os rendimentos (computador de bordo ou teste de tanque cheio).

Se o usuário tiver só um rendimento ou quiser economia em reais sem rendimentos, estime o rendimento faltante com o fator 0,70 (rendimento etanol ≈ 0,70 × rendimento gasolina), avisando que a estimativa carrega essa aproximação.

## Explicar a regra dos 70%

Se o usuário perguntar de onde vem a regra ou pedir para explicá-la: o etanol tem menor poder calorífico que a gasolina, então o motor percorre menos km por litro — em média cerca de 70% da distância. Por isso o etanol só compensa financeiramente quando custa menos de 70% do preço da gasolina. O número exato varia por veículo, por isso a regra é um atalho e o cálculo com rendimentos reais é sempre melhor.

## Formato da resposta

Responda em português, curto e direto:

1. **Veredito em uma linha** ("Abasteça com etanol" / "Abasteça com gasolina" / "Empate técnico"), com o método usado entre parênteses.
2. Os números que sustentam o veredito: custo por km de cada um (método exato) ou a razão de preços vs 0,70 (regra aproximada).
3. Economia em reais por viagem/mês, quando houver distância.
4. No método aproximado, a ressalva de que rendimentos reais dão resposta exata.

Não use tabelas nem listas longas para uma comparação simples; duas ou três frases com os números resolvem. Use tabela só se o usuário comparar vários postos ou cenários de uma vez.
