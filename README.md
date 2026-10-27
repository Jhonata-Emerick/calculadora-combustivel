# Calculadora de Combustível

Etanol ou gasolina? Este plugin ajuda a decidir na hora de abastecer um veículo flex.

## O que ele faz

- Compara etanol e gasolina com os preços do seu posto.
- Com o rendimento (km/l) do veículo em cada combustível, calcula o custo por quilômetro e recomenda o mais barato.
- Estima a economia em reais por viagem ou por mês, se você informar a distância.
- Sem os rendimentos, aplica a regra aproximada dos 70% (etanol compensa quando custa menos de 70% do preço da gasolina), com empate estimado no limite.
- Explica a origem da regra dos 70% quando perguntado.

## O que ele não faz

- Não consulta preços externos — os preços vêm sempre de você.
- Não exige cadastro nem conexão com serviços externos.

## Como usar

Pergunte algo como:

- "Etanol a 3,99 e gasolina a 5,89 — qual compensa?"
- "Meu carro faz 12 km/l na gasolina e 8,5 no etanol. Etanol a 4,19, gasolina a 6,09. Quanto economizo por mês rodando 1.500 km?"
- "De onde vem a regra dos 70%?"

## Instalação

Instale pelo diretório de plugins da Claude, ou direto deste repositório:

```
/plugin install calculadora-combustivel --marketplace Jhonata-Emerick/calculadora-combustivel
```

## Licença

MIT — veja o arquivo [LICENSE](LICENSE).

## Autor

Emerick Consultoria — https://fuel-smart-math.base44.app
