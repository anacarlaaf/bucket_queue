# KLV Bucket Queue

Implementação de uma **fila de prioridade baseada em buckets multinível (KLV Bucket Queue)**, otimizada para algoritmos como **Dijkstra** com operações eficientes de `decrease_key`.

## Inicialização

```cpp
bucket_queue<pair<long long, unsigned int>> q(max_distance, num_vertices, num_levels);
```

### Parâmetros

- `max_distance`: maior distância esperada (`C`).
- `num_vertices`: número máximo de vértices armazenados.
- `num_levels`: quantidade de níveis da estrutura (geralmente `3` ou `4`).

---

## Operações

### Inserir elemento

```cpp
q.push({dist, vertex});
```

Insere um vértice com prioridade `dist`.

---

### Acessar o menor elemento

```cpp
auto [dist, vertex] = q.top();
```

Retorna o elemento com menor prioridade sem removê-lo.

---

### Remover o menor elemento

```cpp
q.pop();
```

Remove o elemento retornado por `top()`.

---

### Atualizar prioridade

```cpp
q.decrease_key(vertex, new_distance);
```

Atualiza a distância de um vértice. Caso ele ainda não esteja na fila, ele é inserido automaticamente.

---

### Verificar se a fila está vazia

```cpp
if (q.empty()) { ... }
```

---

### Tamanho da fila

```cpp
size_t sz = q.size();
```

---

### Reutilizar a estrutura

```cpp
q.reset();
```

Limpa todos os elementos mantendo a memória já alocada.

---

## Exemplo

```cpp
bucket_queue<pair<long long, unsigned int>> q(C, n, 3);

q.push({0, source});

while (!q.empty()) {
    auto [du, u] = q.top();
    q.pop();

    for (auto [v, w] : adj[u]) {
        if (du + w < dist[v]) {
            dist[v] = du + w;
            q.decrease_key(v, dist[v]);
        }
    }
}
```

## Complexidade

| Operação | Complexidade |
|----------|--------------|
| `push` | Amortizada próxima de **O(1)** |
| `top` | Amortizada próxima de **O(1)** |
| `pop` | **O(1)** |
| `decrease_key` | Amortizada próxima de **O(1)** |
| `reset` | **O(n + k·d)** |

Onde:

- `n` = número de vértices;
- `k` = número de níveis;
- `d` = número de buckets por nível (`≈ (C+1)^(1/k)`).

## Observação

- A estrutura foi projetada para algoritmos de caminhos mínimos, especialmente **Dijkstra**, em grafos com pesos inteiros não negativos.