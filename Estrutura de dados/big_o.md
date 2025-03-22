## Notas sobre Big O

Big O descreve **como o tempo ou o uso de memória de um algoritmo cresce** à medida que o tamanho do input (n) aumenta. Em outras palavras, é uma forma de entender o **comportamento assintótico** de um algoritmo sem se prender a detalhes de implementação ou de hardware.

---

## Complexidade de Tempo

### O(1)
- **Definição**: O tempo de execução **não varia** em função do tamanho do input.
- **Exemplo clássico**: Acessar o primeiro elemento de um array.
- **Exemplo visual**: Uma linha **constante** no gráfico — não sobe, mesmo que `n` aumente.

```go
// O(1) - Acesso direto
func getFirstElement(arr []int) int {
    return arr[0] // Sempre constante
}
```

---

### O(log n)
- **Definição**: O tempo de execução **cresce de forma logarítmica**. Para dobrar o número de elementos, o custo aumenta apenas em uma fração (logarítmica).
- **Exemplo clássico**: Busca Binária (Binary Search) — cada comparação reduz o problema à metade.
- **Exemplo visual**: Uma curva que **sobe lentamente** no gráfico conforme `n` cresce.

```go
// O(log n) - Binary Search
func binarySearch(arr []int, target int) bool {
    left, right := 0, len(arr)-1
    for left <= right {
        mid := (left + right) / 2
        if arr[mid] == target {
            return true
        } else if arr[mid] < target {
            left = mid + 1
        } else {
            right = mid - 1
        }
    }
    return false
}
```

---

### O(n)
- **Definição**: O tempo de execução **aumenta na mesma proporção** que o tamanho do input.
- **Exemplo clássico**: Percorrer um array do início ao fim.
- **Exemplo visual**: Gráfico **linear**, subindo conforme `n` cresce.

```go
// O(n) - Percorrer todos os elementos
func linearSearch(arr []int, target int) bool {
    for _, val := range arr {
        if val == target {
            return true
        }
    }
    return false
}
```

---

### O(n log n)
- **Definição**: O tempo de execução **multiplica o tamanho n** pelo **log de n**.
- **Exemplo clássico**: **Merge Sort** ou **Quick Sort** (em média).
- **Exemplo visual**: Sobe **mais rápido** que O(n), mas **mais lento** que O(n²).

```go
// O(n log n) - Merge Sort
func mergeSort(arr []int) []int {
    if len(arr) <= 1 {
        return arr
    }
    mid := len(arr) / 2
    left := mergeSort(arr[:mid])
    right := mergeSort(arr[mid:])
    return merge(left, right)
}

func merge(left, right []int) []int {
    var result []int
    i, j := 0, 0
    for i < len(left) && j < len(right) {
        if left[i] < right[j] {
            result = append(result, left[i])
            i++
        } else {
            result = append(result, right[j])
            j++
        }
    }
    result = append(result, left[i:]...)
    result = append(result, right[j:]...)
    return result
}
```

---

### O(n²)
- **Definição**: O tempo de execução **cresce quadraticamente**: para cada elemento, é preciso percorrer todos os outros.
- **Exemplo clássico**: Comparar todos os pares de um array em loops aninhados.
- **Exemplo visual**: O gráfico **se eleva rapidamente** conforme `n` aumenta.

```go
// O(n²) - Comparar todos os pares
func allPairsSum(arr []int) int {
    sum := 0
    for i := 0; i < len(arr); i++ {
        for j := 0; j < len(arr); j++ {
            sum += arr[i] + arr[j]
        }
    }
    return sum
}
```

---

## Complexidade de Espaço
Também avaliamos **quanto de memória** (espaço) um algoritmo precisa conforme o tamanho do input aumenta.
- **Exemplo**: Criar uma cópia completa do array implica O(n) de espaço adicional.
- **Exemplo visual**: No gráfico, conforme `n` cresce, o uso de memória **acompanha** esse aumento.

---

### Resumo
- **Big O** indica o comportamento assintótico de um algoritmo em termos de **tempo** e **memória**.
- **Ajuda a comparar algoritmos** e prever a escalabilidade para grandes entradas.
- **Não substitui testes práticos**, mas orienta para escolher a abordagem mais eficiente.