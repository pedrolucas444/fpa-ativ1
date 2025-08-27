# Projeto Algoritmo de Karatsuba

## Descrição do Projeto
O Projeto Algoritmo de Karatsuba implementa o algoritmo de Karatsuba em Python para multiplicação eficiente de dois números inteiros grandes. O algoritmo tem como foco reduzir a complexidade em comparação com a multiplicação tradicional, tornando-o mais eficiente para números grandes.

### Algoritmo de Karatsuba
1.	Dividir os números
- Determine o comprimento do maior número n e calcule m = n / 2.
- Divida os números em duas metades:
- X = x1 * 10^m + x2
- Y = y1 * 10^m + y2
- onde:
- x1, y1 → partes mais significativas (metades superiores)
- x2, y2 → partes menos significativas (metades inferiores)
2.	Calcular três multiplicações recursivas
- a = Karatsuba(x1, y1) → multiplicação das partes superiores
- c = Karatsuba(x2, y2) → multiplicação das partes inferiores
- b = Karatsuba(x1 + x2, y1 + y2) → multiplicação das somas das metades
3.	Combinar os resultados
- O produto final é obtido pela fórmula:

```bash
X * Y = (a * 10^(2m)) + ((b - a - c) * 10^m) + c
```

### Código Implementado(Explicação Linha por Linha)
O código está implementado no arquivo `main.py` e segue a estrutura:

```python
def karatsuba(x, y):
    # Caso base da recursão:
    # Se um dos números for menor que 10 (um dígito), 
    # a multiplicação é feita diretamente (sem dividir mais).
    if x < 10 or y < 10:
        return x * y

    # Passo 1: Dividir os números

    # Encontrar o comprimento do maior número
    n = max(len(str(x)), len(str(y)))
    # Dividir pela metade (parte alta e parte baixa)
    m = n // 2

    # Quebrar X em high_x (metade mais significativa) e low_x (menos significativa)
    high_x, low_x = divmod(x, 10**m)
    # Quebrar Y em high_y e low_y
    high_y, low_y = divmod(y, 10**m)

    # Passo 2: Fazer as três multiplicações recursivas

    # z0 = multiplicação das partes baixas
    z0 = karatsuba(low_x, low_y)
    # z1 = multiplicação da soma das partes (x1+x2, y1+y2)
    z1 = karatsuba((low_x + high_x), (low_y + high_y))
    # z2 = multiplicação das partes altas
    z2 = karatsuba(high_x, high_y)

    # Passo 3: Combinar os resultados
    # Fórmula final:
    return (z2 * 10**(2*m)) + ((z1 - z2 - z0) * 10**m) + z0

```

## Como Executar o Projeto

### Requisitos
- Python 3.x 

### Passos para execução
1. Clone este repositório:
   
   git clone <URL_DO_REPOSITORIO>
   
2. Acesse a pasta do projeto:
   
   cd <NOME_DA_PASTA>
   
3. Execute o código:
   
   python main.py
   

## Relarório Técnico

### Complexidade Ciclomática
A complexidade ciclomática é uma métrica que avalia o número de caminhos independentes existentes no código, ajudando a identificar o nível de ramificação e possíveis cenários de teste necessários.

No caso do algoritmo de Karatsuba implementado, o fluxo de controle pode ser representado por nós (instruções) e arestas (ligações entre instruções):
- (Nó 1) def karatsuba(x, y):
- (Nó 2) if x < 10 or y < 10:
- (Nó 3) return x * y
- (Nó 4) n = max(len(str(x)), len(str(y)))
- (Nó 5) m = n // 2
- (Nó 6) high_x, low_x = divmod(x, 10**m)
- (Nó 7) high_y, low_y = divmod(y, 10**m)
- (Nó 8) z0 = karatsuba(low_x, low_y)
- (Nó 9) z1 = karatsuba((low_x + high_x), (low_y + high_y))
- (Nó 10) z2 = karatsuba(high_x, high_y)
- (Nó 11) return (z2 * 10**(2*m)) + ((z1 - z2 - z0) * 10**m) + z0

Fórmula:
```bash
M = E - N + 2P
```
- E = número de arestas do grafo (13)
- N = número de nós (11)
- P = número de componentes conexos (1, já que o programa é único)
```bash
M = 13 - 11 + 2(1) = 4
```
Portanto, a complexidade ciclomática é 4, mostrando que o código possui poucos caminhos independentes, com estrutura clara e baixa probabilidade de erros relacionados a fluxo.

### Complexidade Assintótica
A complexidade do algoritmo é:
- Melhor caso: O(1)
- Caso médio: O(n^1.58)
- Pior caso: O(n^1.58)

A recorrência que descreve o algoritmo é:
```bash
T(n) = 3T(n/2) + O(n)
```

Pelo Teorema Mestre, obtemos:
```bash
T(n) = O(n^{\log_2 3}) 
```
que é aproximadamente:
```bash
O(n^{1.58})
```

## Conclusão
O algoritmo de Karatsuba surge como uma alternativa mais rápida em relação à multiplicação tradicional, principalmente quando lidamos com números muito grandes. Sua complexidade reduzida permite otimizar cálculos intensivos, tornando-o bastante útil em áreas que demandam alto desempenho, como criptografia, computação científica e processamento de grandes inteiros. Apesar de apresentar um custo inicial maior devido ao uso de recursão, seu verdadeiro ganho aparece à medida que os números envolvidos crescem, superando os métodos convencionais.

Com o Projeto Algoritmo de Karatsuba, foi possível demonstrar na prática o motivo de sua eficiência: ao comparar os resultados com a multiplicação tradicional, ficou evidente que o algoritmo de Karatsuba realiza menos operações e entrega tempos de execução mais curtos para entradas maiores, comprovando sua relevância em cenários reais onde desempenho é essencial.