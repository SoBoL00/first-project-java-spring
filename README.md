# Greeting Web Application

## Opis projektu

Jest to prosta aplikacja internetowa stworzona z wykorzystaniem **Spring Boot** oraz **Thymeleaf**. Aplikacja serwuje stronę internetową, która dynamicznie generuje powitanie dla użytkownika na podstawie przekazanej zmiennej `name` oraz wyświetla obrazek.

### Struktura pliku HTML

Plik HTML (`greeting.html`) korzysta z biblioteki **Thymeleaf** do renderowania dynamicznych treści. Kluczowe elementy to:

1. **Dynamiczne powitanie**:
   ```html
   <p th:text="'Hello, ' + ${name} + '!'" />
   ```
   Tekst powitania jest generowany dynamicznie na podstawie wartości zmiennej `name`, która jest przekazywana z kontrolera w aplikacji Spring Boot.

2. **Statyczny tekst**:
   ```html
   <p>
     Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas vestibulum dignissim malesuada.
   </p>
   ```
   Zawiera statyczny tekst dla celów demonstracyjnych.

3. **Obrazek**:
   ```html
   <img th:src="@{/vistula.png}" width="500" height="500"/>
   ```
   Obrazek o nazwie `vistula.png` jest załadowany ze statycznych zasobów aplikacji i wyświetlany na stronie.

## Jak działa aplikacja (Case Study)

### Krok 1: Start aplikacji

Po uruchomieniu aplikacji Spring Boot, serwer nasłuchuje na domyślnym porcie (np. `http://localhost:8080`).

### Krok 2: Żądanie i renderowanie strony

1. Użytkownik wysyła żądanie HTTP (np. do `/greeting`).
2. Kontroler Spring Boot przetwarza to żądanie, przypisuje wartość zmiennej `name` i zwraca widok `greeting.html`.
3. Silnik Thymeleaf renderuje stronę HTML, zastępując zmienne w znacznikach (`th:text`, `th:src`) dynamicznymi danymi.

### Krok 3: Wyświetlenie wyników

Wynikiem jest strona internetowa, która:
- Wyświetla powitanie, np.: "Hello, Dominik!" (jeśli `name=Dominik`)
- Pokazuje tekst demonstracyjny oraz obrazek `vistula.png`.

## Przykłady użycia

| URL                       < Wynik na stronie           >
|----------------------------------------------------------
| `http://localhost:8080/greeting?name=Vistula` < "Hello, Visttula!"       >
| `http://localhost:8080/greeting?name=Mateusz` < "Hello, Mateusz!"        >

## Struktura projektu

### Klasa kontrolera: `HelloController`

Plik: `HelloController.java`

```java
package pl.edu.vistula.first_project_java_spring.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class HelloController {

    @GetMapping(value = "/")
    public String hello() {
        return "Hello Vistula, in my first Spring controller.";
    }

    @GetMapping("/greeting")
    public String greeting(@RequestParam(name="name", required=false, defaultValue="World") String name, Model model) {
        model.addAttribute("name", name);
        return "greeting";
    }
}
```

Ten kontroler obsługuje dwa endpointy:
1. `/` - Zwraca statyczny tekst powitalny.
2. `/greeting` - Renderuje widok `greeting.html` z dynamicznym powitaniem na podstawie parametru `name`.

### Klasa uruchomieniowa: `FirstProjectJavaSpringApplication`

Plik: `FirstProjectJavaSpringApplication.java`

```java
package pl.edu.vistula.first_project_java_spring;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class FirstProjectJavaSpringApplication {

    public static void main(String[] args) {
        SpringApplication.run(FirstProjectJavaSpringApplication.class, args);
    }
}
```

Ta klasa zawiera metodę `main`, która uruchamia aplikację Spring Boot.

## Wymagania

- **Java**: Wersja 11 lub nowsza
- **Maven**: Do zarządzania zależnościami
- **Spring Boot**: Framework backendowy

## Jak uruchomić projekt?

1. Pobierz projekt lub sklonuj repozytorium.
2. Zbuduj projekt za pomocą komendy:
   ```bash
   mvn clean install
   ```
3. Uruchom aplikację:
   ```bash
   mvn spring-boot:run
   ```
4. Przejdź do przeglądarki i otwórz adres:
   ```
   http://localhost:8080/greeting?name=TwojeImie
   ```


## Podsumowanie

Aplikacja przedstawia podstawowe zastosowanie Spring Boot i Thymeleaf do dynamicznego generowania treści na stronie internetowej. Może być rozbudowana o dodatkowe funkcjonalności, takie jak obsługa formularzy, dynamiczne listy czy integracja z bazą danych.
