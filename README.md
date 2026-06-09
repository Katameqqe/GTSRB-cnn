# Rozpoznawanie Znaków Drogowych za pomocą Sieci Neuronowych

Projekt zawiera kompletny i zoptymalizowany proces uczenia maszynowego do klasyfikacji znaków drogowych na podstawie bazy danych GTSRB. Projekt przeszedł drogę od podstawowej konfiguracji do bezpiecznej i odpornej na błędy struktury sieci splotowych.

## Rozwiązane wyzwania:

1. Nierówny podział znaków w bazie danych. Niektóre znaki występują bardzo rzadko. Rozwiązaliśmy to przez wdrożenie mechanizmu próbkowania ważonego o nazwie WeightedRandomSampler. 
2. Wyciek danych w bazie. Zdjęcia tego samego fizycznego znaku nagrane sekwencyjnie mogły trafić jednocześnie do uczenia i testu. Zaprojektowaliśmy własny podział danych na poziomie całych serii zdjęć. Zapobiega to oszukiwaniu sieci i urealnia wyniki.

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
- Model wysokiej rozdzielczości: 95.39 procent dokładności, co stanowi nasz najlepszy wynik

## Zapisane wykresy:

- test_confusion_matrix.png to wykres wszystkich pomyłek i poprawnych trafień
- model_mistakes_analysis.png to zestawienie zdjęć, na których model się pomylił
- gradcam_high_res_analysis.png to nałożone na znaki mapy ciepła pokazujące skupienie uwagi sieci

## Requirements:

1. Zainstaluj biblioteki wpisując pip install -r requirements.txt.

## Struktura projektu:
```
GTSRB-cnn/
main.ipynb
test.ipynb
requirements.txt
data/
Train/ - foldery ze znakami od 0 do 42
Test/ - zdjęcia w formacie png
Train.csv
Test.csv
```