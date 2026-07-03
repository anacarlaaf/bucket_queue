# K-Level Bucket Queue

Implementação de uma **K-Level Bucket Queue** para filas de prioridade monotônicas, otimizada para algoritmos como **Dijkstra** com pesos inteiros não negativos.

## Importação

Salve a implementação em um arquivo, por exemplo:

```text
bucket_queue.hpp
```

Inclua no código C++:

```cpp
#include "bucket_queue.hpp"
```

ou, caso esteja em outro diretório:

```cpp
#include "path/to/bucket_queue.hpp"
```

## Instanciação

```cpp
using PQ = bucket_queue<std::pair<long long, unsigned int>>;

long long max_distance = 1000000;
int n = 100000;
int levels = 3;

PQ pq(max_distance, n, levels);
```

### Parâmetros

* `max_distance`: maior distância esperada (define o tamanho dos buckets).
* `n`: número de vértices/elementos.
* `levels`: número de níveis da estrutura (padrão recomendado: `3`).

---

## Interface

### Inserir elemento

```cpp
pq.push({dist, vertex});
```

### Menor elemento

```cpp
auto [dist, vertex] = pq.top();
```

### Remover o menor elemento

```cpp
pq.pop();
```

### Atualizar prioridade (`decrease_key`)

```cpp
pq.decrease_key(vertex, new_distance);
```

Se o vértice ainda não estiver na fila, ele é inserido automaticamente.

### Verificar se está vazia

```cpp
pq.empty();
```

### Número de elementos

```cpp
pq.size();
```

### Reinicializar

```cpp
pq.reset();
```

Mantém a memória alocada e limpa toda a estrutura.

---

## Exemplo

```cpp
#include <bits/stdc++.h>
#include "bucket_queue.hpp"

using namespace std;

int main() {
    using PQ = bucket_queue<pair<long long, unsigned int>>;

    PQ pq(1000, 10, 3);

    pq.push({10, 1});
    pq.push({5, 2});
    pq.push({20, 3});

    while (!pq.empty()) {
        auto [dist, v] = pq.top();
        cout << v << " " << dist << '\n';
        pq.pop();
    }

    return 0;
}
```
