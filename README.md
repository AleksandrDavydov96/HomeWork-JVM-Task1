# Домашнее задание к занятию 4.1 (модуль 3): JVM. Организация памяти, сборщики мусора, VisualVM

# Задача "Понимание JVM"

## Код для исследования
```java

public class JvmComprehension { // Класс JvmComprehension (и др. системные классы) подгружается через ClassLoader в Metaspace.

    public static void main(String[] args) { // Создание фрейма main() в стеке.
        int i = 1;                      // 1 Создается переменная i в фрейме main() в стеке.
        Object o = new Object();        // 2 Выделяется область памяти в куче, создается объект Object.
        // В фрейме main() в стеке создпется переменная o со ссылкой на объект в куче.
        Integer ii = 2;                 // 3 Создается переменная ii в фрейме main() в стеке.
        printAll(o, i, ii);             // 4 Создание фрейма printAll() в стеке.
        // Создается новая переменная о в фрейме printAll() со ссылкой на созданный объект в куче.
        // Создаются переменные i и ii в фрейме printAll().
        System.out.println("finished"); // 7 В куче создается объект String со строкой "finished".
        // Создается новый фрейм println() со ссылкой на объект String в куче.
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5 Создается объект Integer в куче.
        // В фрейме printAll() создается переменная uselessVar со ссылкой на объект в куче.
        System.out.println(o.toString() + i + ii);  // 6 Созается фрейм toString() со ссылкой на Object в куче,
        // в куче создается объект String в который записывается преобразованный Object,
        // в фрейме toString() хранится ссылка на объект String.
        // Создается фрейм println(), в него передается ссылка на объект String в куче от метода toString(),
        // создается переменаня i в фрейме println(), в фрейме println() создается ссылка на объект Integer ii в куче.
        // Затем в куче создается объект String в который записывается сумма (o.toString() + i + ii),
        // ссылка на объект String передается в фрейм println().
    }
    // Сборщик мусора отрабатывает во время выполнения программы.
}

```