Napisz rekurencyjną wersję algorytmu binSearch, dokonaj analizy złożoności czasowej i pamięciowej i porównaj z wersją nierekurencyjną.

def binSearch(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid  # target found
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1  # target is missing


arr = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21]
target = 15

index = binSearch(arr, target)
if index != -1:
    print(f"Element {target} znaleziony na pozycji {index}")
else:
    print(f"Element {target} nie znaleziony w liście")

W tym kodzie, arr to posortowana lista, a target to element, którego szukamy. Funkcja zwraca indeks elementu target w liście arr jeśli jest obecny, w przeciwnym razie zwraca -1. Algorytm działa poprzez ciągłe dzielenie listy na dwie połówki, aż znajdzie szukany element lub do momentu, gdy lista zostanie całkowicie przeszukana.

Rekurencyjna wersja algorytmu binSearch:

def binSearchRecursive(arr, target, left, right):
    if left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid  # target found
        elif arr[mid] < target:
            return binSearchRecursive(arr, target, mid + 1, right)
        else:
            return binSearchRecursive(arr, target, left, mid - 1)
    else:
        return -1  # target is missing

def binSearch(arr, target):
    return binSearchRecursive(arr, target, 0, len(arr) - 1)

Teraz, porównujemy obie wersje pod względem złożoności czasowej i pamięciowej:

Analiza Złożoności Czasowej:

Wersja nierekurencyjna:
Każda iteracja dzieli zakres wyszukiwania na pół, co oznacza, że liczba kroków wyszukiwania jest logarytmiczna względem rozmiaru listy arr.
Złożoność czasowa wynosi O(log n), gdzie n to liczba elementów w liście arr.

Wersja rekurencyjna:
Podobnie jak wersja nierekurencyjna, każde wywołanie rekurencyjne dzieli zakres wyszukiwania na pół.
Złożoność czasowa również wynosi O(log n), ale rekurencja może wprowadzić pewne dodatkowe koszty ze względu na wywołania funkcji i stos wywołań.

Analiza Złożoności Pamięciowej:

Wersja nierekurencyjna:
Wymaga tylko stałej ilości dodatkowej pamięci na przechowywanie zmiennych pomocniczych, takich jak left, right i mid.
Złożoność pamięciowa jest O(1).

Wersja rekurencyjna:
Każde wywołanie rekurencyjne umieszcza na stosie kolejną kopię zmiennych lokalnych oraz adres powrotu.
W skrajnym przypadku, kiedy rekurencja sięga maksymalnej głębokości, złożoność pamięciowa może być proporcjonalna do głębokości rekursji, co wynosi O(log n) dla algorytmu binarnego wyszukiwania.
Podsumowując, obie wersje mają taką samą złożoność czasową, ale wersja rekurencyjna może wymagać dodatkowej pamięci na stosie, co może stanowić problem dla bardzo dużych list. Jednakże, dla większości zastosowań, różnica w złożoności pamięciowej nie będzie zauważalna, a wersja rekurencyjna może być bardziej czytelna i łatwiejsza do zrozumienia.

Podsumowując, obie wersje mają taką samą złożoność czasową, ale wersja rekurencyjna może wymagać dodatkowej pamięci na stosie, co może stanowić problem dla bardzo dużych list. Jednakże, dla większości zastosowań, różnica w złożoności pamięciowej nie będzie zauważalna, a wersja rekurencyjna może być bardziej czytelna i łatwiejsza do zrozumienia.
