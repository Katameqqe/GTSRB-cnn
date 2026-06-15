# Klasyfikacja Znaków Drogowych za pomocą Sieci Splotowych na zbiorze GTSRB

Repozytorium zawiera implementację systemu klasyfikacji znaków drogowych opartego na architekturze splotowej sieci neuronowej CNN dla zbioru danych GTSRB. Projekt wykorzystuje oficjalną i stabilną bibliotekę torchvision.datasets.GTSRB w celu bezpośredniej klasyfikacji obrazów znaków drogowych na podstawie dostarczonego zestawu danych.

## Zawartość plików:

### Plik main.ipynb:

- Wizualizacja zdjęć oraz ilościowa analiza ich liczebności
- Podział danych na poziomie całych serii zdjęć zapobiegający oszukiwaniu sieci
- Przygotowanie danych oraz automatyczne przekształcenia obrazów, takie jak obracanie, zmiana kontrastu i wymazywanie fragmentów
- Proces uczenia, który automatycznie zapisuje tylko najlepszy uzyskany stan modelu i stopniowo zmniejsza krok uczenia przy braku postępów
- Optymalizacja parametrów sieci za pomocą narzędzia Optuna

### Plik test.ipynb, czyli testowanie i analiza działania:

- Ocena czterech różnych modeli na osobnym zbiorze testowym
- Generowanie tabeli pomyłek oraz raportu dokładności
- Wizualizacja konkretnych pomyłek sieci, pokazująca trudne zdjęcia
- Generowanie map ciepła metodą Grad-CAM, pokazujących na które dokładnie elementy znaku patrzyła sieć

## Budowa sieci:

Model składa się z trzech bloków przetwarzania obrazu. Każdy z nich analizuje kształty i krawędzie, stopniowo zwiększając liczbę wykrywanych detali. Na końcu znajduje się klasyfikator, który decyduje, jaki to znak, oraz mechanizm Dropout zapobiegający uczeniu się na pamięć.

## Wyniki testów:

Wszystkie modele zostały przetestowane na osobnym, bezpiecznym zbiorze testowym zawierającym 12 630 zdjęć:

- Model podstawowy: 93.06 procent dokładności
- Model z przekształceniami obrazu: 93.18 procent dokładności
- Model zoptymalizowany przez Optunę: 93.02 procent dokładności
- Model wysokiej rozdzielczości: 95.39 procent dokładności


## Requirements:

 pip install -r requirements.txt.

## Struktura projektu:
```
main.ipynb
test.ipynb
requirements.txt
data/gtsrb/GTSRB/Final_Test - Testowanie
data/gtsrb/GTSRB/Training - Trenowanie
```