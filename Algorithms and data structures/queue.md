Kolejka piorytetowa 
- to abstrakcyjny typ danych, którego elementy mają przypisany piorytet,
- udostępnia elementy w kolejności ich piorytetów,
- używana w algorytmach tj: sortowanie sterty, Prima, najkrótsza ścieżka Dijkstry, 

Odpowiednią strukturą danych do zaimplementowania kolejki piorytetowej jest STERTA opatra na drzewach.

Jeśli P jest węzłem nadrzędnym dla C, to klucz (wartość) P jest w przypadku sterty typu max większy lub równy kluczowi C, a w przypadku sterty typu main - mniejszy lub równy kluczowi C.

```
#include <iostream>
#include <vector>
#include <algorithm>
#include <assert.h>
```
template < class klasa > - szablon klasy, możemy sami decydować p typie

class Type	- Typ danych jakiego mają być elementy, które są przechowywane przez kontener.
class Allocator - Alokator, który jest odpowiedzialny za zarządzanie pamięcią. Domyślnie używany jest standardowy alokator pamięci, tj. std::allocator<Type>

Szablon vector:
- struktura danych reprezentująca tablicę,
- tablica jest zbudowana z elementów o typie przekazanym poprzez parametr szablonu Type, 
- kontener umożliwia modyfikację rozmiaru tablicy w trakcie życia obiektu,
- dane w tablicy są ułożone w pamięci zawsze w sposób ciągły co oznacza, że kopiowanie danych do kontenera i z kontenera za pomocą funkcji takich jak np. memcpy jest zawsze bezpieczne.

Zastosowanie: priorytetem jest posiadanie szybkiego dostępu do dowolnego elementu kontenera.

begin() - Zwraca iterator wskazujący na pierwszy element. (metoda)
end() - Zwraca iterator wskazujący na element będący za ostatnim elementem. (metoda)
push_back() - Dodaje nowy element na końcu kontenera vector. (metoda)
pop_back() - Usuwa jeden element z kontenera vector, znajdujący się na jego końcu. (metoda)
empty - 	Sprawdza czy kontener jest pusty. (metoda)

Operacje pozwalające na obsługę sterty:
 - std::make_heap(): tworzy stertę typu max dla podanego zbioru danych, używając w celu przyporządkowania elementów, operatora < lub funkcji porównującej przez użytkownika,
 - std::push_heap(): umieszcza nowy element na końcu sterty typu max,
 - std::pop_heap(): usuwa pierwszy element sterty (zmieniając wartości dla pierwszej i ostatniej pozycji oraz czyniąc podzbiór [pierwszy, ostatni-1) stertą typu max).


```
template <class T,
   class Compare = std::less<typename std::vector<T>::value_type>>
   class priority_queue{
   typedef typename std::vector<T>::value_type      value_type;
   typedef typename std::vector<T>::size_type       size_type;
   typedef typename std::vector<T>::reference       reference;
   typedef typename std::vector<T>::const_reference const_reference;
public:
   bool empty() const noexcept { return data.empty(); }
   size_type size() const noexcept { return data.size(); }


   void push(value_type const & value){
      data.push_back(value);
      std::push_heap(std::begin(data), std::end(data), comparer);
   }

   void pop(){
      std::pop_heap(std::begin(data), std::end(data), comparer);
      data.pop_back();
   }

   const_reference top() const { return data.front(); }

   void swap(priority_queue& other) noexcept{
      swap(data, other.data);
      swap(comparer, other.comparer);
   }

private:
   std::vector<T> data;
   Compare comparer;
};
```

```
template< class T, class Compare>
void swap(
   priority_queue<T, Compare>& lhs,
   priority_queue<T, Compare>& rhs) noexcept(noexcept(lhs.swap(rhs))){
   lhs.swap(rhs);
}
```
Stos - struktura danych, w której dostęp do danych jest możliwy tylko do jednego elementu, zwanego wierzchołkiem. Jest określany mianem LIFO (Last In First Out).

Operacje na stosie:
- push - umieszczenie nowego elementu na szczycie stosu;
- pop - zdjęcie istniejącego elementu ze szczytu stosu;
- empty - informacja czy stos jest pusty;
- size - zwraca ilość elementów umieszczonych na stosie;
- top - zwraca wartość szczytowego elementu na stosie.

assert() - Sprawdza wartość wyrażenia; jeżeli jest fałszywe wypisuje komunikat diagnostyczny i przerywa działanie aplikacji.
pop() - Metoda pop służy do zdjęcia istniejącego elementu ze szczytu stosu.
empty() - Metoda empty sprawdza, czy stos jest pusty.
top() - Metoda top służy do odczytania lub modyfikacji wartości umieszczonej na szczycie stosu.\
push() - Metoda push służy do umieszczenia nowego elementu na szczycie stosu.
```
int main(){
   priority_queue<int> q;
   for (int i : {1, 5, 3, 1, 13, 21, 8}){
      q.push(i);
   }

   assert(!q.empty());
   assert(q.size() == 7);

   while (!q.empty()){
      std::cout << q.top() << ' ';
      q.pop();
   }
}

```
