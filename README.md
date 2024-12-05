def counting_sort_for_radix(arr, exp):
    """
    Realiza o Counting Sort baseado em um dígito específico (exp).
    
    :param arr: Lista de elementos a serem ordenados.
    :param exp: Representa o dígito atual a ser ordenado (1, 10, 100, etc.).
    """
    n = len(arr)
    output = [0] * n  # Lista para armazenar o resultado ordenado
    count = [0] * 10  # Contagem para os dígitos (0 a 9)

    # Contagem das ocorrências de cada dígito no dígito exp
    for i in range(n):
        index = (arr[i] // exp) % 10
        count[index] += 1

    # Atualização para determinar as posições corretas
    for i in range(1, 10):
        count[i] += count[i - 1]

    # Construção da lista ordenada
    for i in range(n - 1, -1, -1):
        index = (arr[i] // exp) % 10
        output[count[index] - 1] = arr[i]
        count[index] -= 1

    # Copia o resultado ordenado de volta para arr
    for i in range(n):
        arr[i] = output[i]


def radix_sort(arr):
    """
    Ordena uma lista de números inteiros usando o Radix Sort.
    
    :param arr: Lista de números inteiros a serem ordenados.
    """
    if len(arr) == 0:
        return arr

    # Encontra o maior número para determinar o número de dígitos
    max_val = max(arr)

    # Aplica o Counting Sort para cada dígito (posição: unidades, dezenas, etc.)
    exp = 1
    while max_val // exp > 0:
        counting_sort_for_radix(arr, exp)
        exp *= 10

    return arr


# Testes
if __name__ == "__main__":
    data = [170, 45, 75, 90, 802, 24, 2, 66]
    print("Lista original:", data)
    sorted_data = radix_sort(data)
    print("Lista ordenada:", sorted_data)
# 9.-Radix-Sort
