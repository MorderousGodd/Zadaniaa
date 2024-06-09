Zadanie.1 
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        # Ostatnie i elementów są już na swoich miejscach
        for j in range(0, n-i-1):
            # Zamiana elementów jeśli są w złej kolejności
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]

# Przykładowe użycie
arr = [64, 34, 25, 12, 22, 11, 90]
print("Przed sortowaniem:", arr)
bubble_sort(arr)
print("Po sortowaniu:", arr)

Zadanie.2
def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i+1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]

# Przykładowe użycie
arr = [64, 34, 25, 12, 22, 11, 90]
print("Przed sortowaniem:", arr)
selection_sort(arr)
print("Po sortowaniu:", arr)

import time

# Funkcja do pomiaru czasu wykonania
def measure_time(algorithm, arr):
    start_time = time.time()
    algorithm(arr)
    end_time = time.time()
    return end_time - start_time

arr = [64, 34, 25, 12, 22, 11, 90]

# Pomiar czasu sortowania bąbelkowego
bubble_sort_time = measure_time(bubble_sort, arr.copy())
print("Czas sortowania bąbelkowego:", bubble_sort_time)

# Pomiar czasu sortowania przez wybieranie
selection_sort_time = measure_time(selection_sort, arr.copy())
print("Czas sortowania przez wybieranie:", selection_sort_time)

Zadanie.3
def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and key < arr[j]:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key

# Funkcja do generowania częściowo posortowanych danych
def partially_sorted_data(size, percent_sorted):
    num_sorted = int(size * percent_sorted / 100)
    arr = [i for i in range(num_sorted)]
    arr.extend([random.randint(0, 1000) for _ in range(size - num_sorted)])
    return arr

# Przykładowe użycie
arr = [64, 34, 25, 12, 22, 11, 90]
print("Przed sortowaniem:", arr)
insertion_sort(arr)
print("Po sortowaniu:", arr)

import time
import random

# Funkcja do pomiaru czasu wykonania
def measure_time(algorithm, arr):
    start_time = time.time()
    algorithm(arr)
    end_time = time.time()
    return end_time - start_time

# Generowanie danych testowych
random_data = [random.randint(0, 1000) for _ in range(1000)]
partially_sorted = partially_sorted_data(1000, 80)  # 80% danych posortowanych

# Pomiar czasu dla całkowicie losowych danych
random_sort_time = measure_time(insertion_sort, random_data.copy())
print("Czas sortowania całkowicie losowych danych:", random_sort_time)

# Pomiar czasu dla częściowo posortowanych danych
partially_sorted_sort_time = measure_time(insertion_sort, partially_sorted.copy())
print("Czas sortowania częściowo posortowanych danych:", partially_sorted_sort_time)

Zadanie.4
import time

# Implementacja sortowania przez wstawianie
def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and key < arr[j]:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key

# Funkcja do pomiaru czasu wykonania
def measure_time(algorithm, arr):
    start_time = time.time()
    algorithm(arr)
    end_time = time.time()
    return end_time - start_time

# Dane z tabelki
data_from_table = [64, 34, 25, 12, 22, 11, 90]

# Pomiar czasu sortowania bąbelkowego na danych z tabelki
bubble_sort_time = measure_time(bubble_sort, data_from_table.copy())
print("Czas sortowania bąbelkowego na danych z tabelki:", bubble_sort_time)

# Pomiar czasu sortowania przez wstawianie na danych z tabelki
insertion_sort_time = measure_time(insertion_sort, data_from_table.copy())
print("Czas sortowania przez wstawianie na danych z tabelki:", insertion_sort_time)

Sortowanie bąbelkowe ma złożoność czasową O(n^2), co oznacza, że jego wydajność spada dramatycznie wraz ze wzrostem liczby elementów do posortowania. Jest to zazwyczaj mniej wydajne niż sortowanie przez wstawianie, szczególnie dla dużych zbiorów danych.

Sortowanie przez wstawianie również ma złożoność czasową O(n^2), ale w praktyce działa lepiej niż sortowanie bąbelkowe dla wielu przypadków, zwłaszcza gdy dane są częściowo posortowane. Działa ono poprzez iteracyjne "wstawianie" elementów do już posortowanej części tablicy, co może być bardziej efektywne niż "przechodzenie" przez wszystkie elementy, jak to robi sortowanie bąbelkowe.

W skrócie, sortowanie przez wstawianie często działa lepiej niż sortowanie bąbelkowe, szczególnie dla większych zbiorów danych i danych częściowo posortowanych. Jednakże, wybór algorytmu sortowania zależy od charakterystyki danych i wymagań wydajnościowych danego problemu.

Zadanie.5

import time
import random

def quicksort(arr):
    if len(arr) <= 1:
        return arr
    else:
        pivot = arr[0]
        less_than_pivot = [x for x in arr[1:] if x <= pivot]
        greater_than_pivot = [x for x in arr[1:] if x > pivot]
        return quicksort(less_than_pivot) + [pivot] + quicksort(greater_than_pivot)

def measure_time(algorithm, arr):
    start_time = time.time()
    algorithm(arr)
    end_time = time.time()
    return end_time - start_time

# Dane testowe
data = [random.randint(0, 1000) for _ in range(1000)]

# Pomiar czasu sortowania szybkiego na danych testowych
quicksort_time = measure_time(quicksort, data.copy())
print("Czas sortowania szybkiego na danych testowych:", quicksort_time)

def quicksort(arr, pivot_choice='first'):
    if len(arr) <= 1:
        return arr
    else:
        if pivot_choice == 'first':
            pivot = arr[0]
        elif pivot_choice == 'random':
            pivot = random.choice(arr)
        elif pivot_choice == 'median_of_three':
            first = arr[0]
            middle = arr[len(arr) // 2]
            last = arr[-1]
            pivot = sorted([first, middle, last])[1]

        less_than_pivot = [x for x in arr[1:] if x <= pivot]
        greater_than_pivot = [x for x in arr[1:] if x > pivot]
        return quicksort(less_than_pivot, pivot_choice) + [pivot] + quicksort(greater_than_pivot, pivot_choice)

# Dane testowe
data = [random.randint(0, 1000) for _ in range(1000)]

# Pomiar czasu sortowania szybkiego na danych testowych dla różnych metod wyboru pivota
pivot_choices = ['first', 'random', 'median_of_three']
for pivot_choice in pivot_choices:
    quicksort_time = measure_time(quicksort, data.copy())
    print(f"Czas sortowania szybkiego z wyborem pivota '{pivot_choice}':", quicksort_time)

Wybór pierwszego elementu ('first'):

Prosty do zaimplementowania.
W przypadku, gdy dane są już częściowo posortowane, wybór pierwszego elementu może prowadzić do powstania niesymetrycznego drzewa rekursji, co może spowolnić działanie algorytmu.
Losowy wybór elementu ('random'):

Eliminuje ryzyko wystąpienia najgorszego przypadku (np. gdy dane są posortowane lub odwrotnie posortowane).
W niektórych przypadkach może być skuteczny, ale może również prowadzić do zmienności wyników, ponieważ wybór losowego elementu może być trudny do przewidzenia.
Wybór mediany z trzech losowych elementów ('median_of_three'):

Wybór mediany z trzech losowych elementów pomaga w redukcji ryzyka najgorszego przypadku.
Jest bardziej deterministyczny niż losowy wybór pivota, co może być korzystne w niektórych sytuacjach.
W praktyce może być skutecznym kompromisem między prostotą implementacji a wydajnością.

Zadanie.6

import time
import random

def merge_sort(arr):
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left_half = merge_sort(arr[:mid])
    right_half = merge_sort(arr[mid:])

    return merge(left_half, right_half)

def merge(left, right):
    result = []
    left_idx, right_idx = 0, 0

    while left_idx < len(left) and right_idx < len(right):
        if left[left_idx] < right[right_idx]:
            result.append(left[left_idx])
            left_idx += 1
        else:
            result.append(right[right_idx])
            right_idx += 1

    result.extend(left[left_idx:])
    result.extend(right[right_idx:])
    return result

def measure_memory_usage(arr):
    import sys
    return sys.getsizeof(arr)

# Dane testowe
data = [random.randint(0, 1000) for _ in range(1000)]

# Sortowanie przez scalanie
merge_sorted_data = merge_sort(data.copy())
print("Posortowane dane przez scalanie:", merge_sorted_data)

# Pomiar użycia pamięci
merge_sort_memory = measure_memory_usage(merge_sorted_data)
print("Użycie pamięci po sortowaniu przez scalanie:", merge_sort_memory)

def quicksort(arr):
    if len(arr) <= 1:
        return arr
    else:
        pivot = arr[0]
        less_than_pivot = [x for x in arr[1:] if x <= pivot]
        greater_than_pivot = [x for x in arr[1:] if x > pivot]
        return quicksort(less_than_pivot) + [pivot] + quicksort(greater_than_pivot)

# Dane testowe
data = [random.randint(0, 1000) for _ in range(1000)]

# Sortowanie szybkie
quicksort_sorted_data = quicksort(data.copy())
print("Posortowane dane szybko:", quicksort_sorted_data)

# Pomiar użycia pamięci
quicksort_memory = measure_memory_usage(quicksort_sorted_data)
print("Użycie pamięci po sortowaniu szybkim:", quicksort_memory)

Mergesort jest stabilny i zawsze działa w czasie O(n log n), niezależnie od danych wejściowych. Jednakże, wymaga dodatkowej pamięci w postaci tablicy pomocniczej do scalania podlist, co może prowadzić do większego zużycia pamięci w porównaniu z Quicksortem, szczególnie dla dużych zbiorów danych.
Quicksort ma złożoność czasową O(n log n) w przypadku przeciętnym, ale w najgorszym przypadku może osiągnąć O(n^2). Jednakże, nie wymaga dodatkowej pamięci, ponieważ sortuje w miejscu. Jest to korzystne, jeśli pamięć jest ograniczonym zasobem.
Stąd, jeśli pamięć jest ograniczonym zasobem i nie jesteśmy zbytnio zaniepokojeni najgorszym przypadkiem, Quicksort może być bardziej odpowiedni. Jednakże, jeśli pamięć nie jest problemem i chcemy mieć pewność, że algorytm działa zawsze w czasie O(n log n), Mergesort może być lepszym wyborem.

Zadanie.7

import time
import random

def heapify(arr, n, i):
    largest = i
    left = 2 * i + 1
    right = 2 * i + 2

    if left < n and arr[left] > arr[largest]:
        largest = left

    if right < n and arr[right] > arr[largest]:
        largest = right

    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)

def heapsort(arr):
    n = len(arr)

    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i)

    for i in range(n - 1, 0, -1):
        arr[0], arr[i] = arr[i], arr[0]
        heapify(arr, i, 0)

def measure_time(algorithm, arr):
    start_time = time.time()
    algorithm(arr)
    end_time = time.time()
    return end_time - start_time

# Dane testowe
data_sizes = [10, 100, 1000]  # różne rozmiary list
orderings = ["random", "ascending", "descending"]  # różne uporządkowania danych

for size in data_sizes:
    for ordering in orderings:
        if ordering == "random":
            data = [random.randint(0, 1000) for _ in range(size)]
        elif ordering == "ascending":
            data = list(range(size))
        else:
            data = list(range(size, 0, -1))

        heapsort_time = measure_time(heapsort, data.copy())
        print(f"Czas sortowania przez kopcowanie dla danych rozmiaru {size} i uporządkowania '{ordering}': {heapsort_time} sekundy")

Funkcja heapify tworzy kopiec dla danego poddrzewa.
Funkcja heapsort najpierw buduje kopiec z listy, a następnie wymienia elementy kopca z ostatnim elementem nieposortowanym i naprawia kopiec.
Funkcja measure_time służy do pomiaru czasu sortowania.

Różne rozmiary list:

Zwiększenie rozmiaru listy zazwyczaj prowadzi do wzrostu czasu sortowania. Jest to spowodowane tym, że im więcej danych musi zostać posortowanych, tym więcej operacji musi być wykonanych przez algorytm, co z kolei zajmuje więcej czasu.
Możemy spodziewać się, że czas sortowania przez kopcowanie będzie rosnął wraz ze wzrostem rozmiaru listy, ale tempo tego wzrostu może być zróżnicowane w zależności od specyfiki danych wejściowych oraz efektywności implementacji algorytmu.
Różne uporządkowanie danych:

Dla danych losowych można oczekiwać, że czas sortowania będzie średnio na poziomie, czyli algorytm będzie działał w oczekiwanym czasie.
Dla danych już posortowanych w kolejności rosnącej lub malejącej (lub prawie posortowanych), algorytm może działać wolniej, ponieważ musi często dokonywać zamiany elementów na pierwszym etapie tworzenia kopca. W takich przypadkach czas sortowania może być dłuższy niż dla danych losowych.
Dla danych posortowanych w odwrotnej kolejności (tj. malejącej, gdy algorytm sortuje rosnąco i odwrotnie), czas sortowania może być dłuższy, ponieważ algorytm będzie musiał dokonać więcej zamian na każdym etapie budowania kopca.
Podsumowując, czas sortowania przez kopcowanie może różnić się w zależności od rozmiaru danych i ich uporządkowania. Dla danych losowych algorytm zazwyczaj działa w przyzwoitym czasie, ale dla danych częściowo posortowanych lub dużych list czas sortowania może być wydłużony.
