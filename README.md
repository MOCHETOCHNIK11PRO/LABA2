# LABA2
#include <iostream>
#include <chrono>

using namespace std;
using namespace chrono;


int main() {
    // Выбор среды для локализации русского языка
    while (true)
    {
        int Environment;
        cout << "1) Clion\n2) Visual Studio\nSelect the development environment number: ";
        cin >> Environment;
        if (Environment == 1) {
            setlocale(LC_ALL, "ru_RU.UTF-8");
            system("chcp 65001");
            break;
        }
        if (Environment == 2) {
            setlocale(0, "Rus");
            break;
        }
        else
            cout << "\n???\n";
    }

    time_point<steady_clock, duration<__int64, ratio<1, 1000000000>>> start, end;
    nanoseconds result;
    int Point = 10;
    int x, j, Max, Min, Mid, Quantity, a, b, index_1, index_2;
    int Nums[100], Sort_Nums[100];

    while (true)
    {
        // Задание 1
        if (Point == 10 || Point == 1)
        {
            srand(time(0));

            for (int i = 0; i < 100; i++) {
                Nums[i] = rand() % 199 - 99; // диапазон [-99; 99]
                Sort_Nums[i] = Nums[i];
            }
            cout << "Задание 1\nЦелочисленный масcив: [";
            for (int i = 0; i < 100; i++) {
                cout << Nums[i] << " ";
            }
            cout << "]\n\n";
        }

        // Задание 2
        if (Point == 10 || Point == 2)
        {
            start = steady_clock::now(); // Начальный момент времени

            // Cортировка "Insert sort"
            for (int i = 1; i < 100; i++) {
                x = Sort_Nums[i];
                j = i;
                while ((j > 0) && (x < Sort_Nums[j - 1])) {
                    Sort_Nums[j] = Sort_Nums[j - 1];
                    j--;
                }
                Sort_Nums[j] = x;
            }

            end = steady_clock::now(); // Конечный момент времени
            result = duration_cast<nanoseconds>(end - start);
            cout << "Задание 2\nОтсортированный масcив: [";
            for (int i = 0; i < 100; i++) {
                cout << Sort_Nums[i] << " ";
            }
            cout << "]\n";
            cout << "Время сортировки: " << result.count() << " (наносек.)\n\n";
        }

        // Задание 3
        if (Point == 10 || Point == 3)
        {
            Min = Max = Sort_Nums[0];
            start = steady_clock::now();
            for (int i = 1; i < 100; i++) { // Поиск максимального и минимального значений
                if (Max < Sort_Nums[i])
                    Max = Sort_Nums[i];
                if (Min > Sort_Nums[i])
                    Min = Sort_Nums[i];
            }
            cout << "Задание 3\nМаксимальный элемент: " << Max << "\nМинимальный элемет: " << Min;
            end = steady_clock::now();
            result = duration_cast<nanoseconds>(end - start);
            cout << "\nВремя поиска макс. и мин. элементов в отсортированном массиве: " << result.count()
                 << " (наносек.)\n\n";

            Min = Max = Nums[0];

            start = steady_clock::now();
            for (int i = 1; i < 100; i++) {
                if (Max < Nums[i])
                    Max = Nums[i];
                if (Min > Nums[i])
                    Min = Nums[i];
            }
            cout << "Максимальный элемент: " << Max << "\nМинимальный элемет: " << Min;
            end = steady_clock::now();
            result = duration_cast<nanoseconds>(end - start);
            cout << "\nВремя поиска макс. и мин. элементов в не отсортированном массиве: " << result.count()
                 << " (наносек.)\n\n";
        }

        // Задание 4
        if (Point == 10 || Point == 4)
        {
            Quantity = 0;
            Mid = (Max + Min); // Поиск среднего значения
            if (Mid % 2 > 0) {
                Mid += 1;
            }
            Mid /= 2;
            cout << "Задание 4\nСреднее значение макс. и мин. элементов массива:" << Mid
                 << "\nИндексы всех элементов, равные среднему значению: [ ";

            for (int i = 20; i < 100; i++) { // Поиск индексов элементов и их кол-ва
                if (Sort_Nums[i] == Mid) {
                    cout << i << " ";
                    Quantity += 1;
                }
                if (Sort_Nums[i] > Mid) {
                    break;
                }
            }
            cout << "] \nКоличество эелементов: " << Quantity << "\n\n";
        }

        // Задание 5
        if (Point == 10 || Point == 5)
        {
            Quantity = 0;
            cout << "Задание 5\nВведите целое число: ";
            cin >> a;

            for (int i = 0; i < 100; i++) { // Поиск кол-ва элементов, которые меньше а
                if (Sort_Nums[i] < a) {
                    Quantity += 1;
                }
                if (Sort_Nums[i] >= a) {
                    break;
                }
            }
            cout << "\nКоличество элементов, которые меньше введенного числа: " << Quantity << "\n\n";
        }

        // Задание 6
        if (Point == 10 || Point == 6)
        {
            Quantity = 0;
            cout << "Задание 6\nВведите целое число: ";
            cin >> b;

            for (int i = 0; i < 100; i++) { // Поиск кол-ва элементов, которые больше b
                if (Sort_Nums[i] > b) {
                    Quantity += 1;
                }
            }
            cout << "\nКоличество элементов, которые больше введенного числа: " << Quantity << "\n\n";
        }

        // Задание 7
        if (Point == 10 || Point == 7)
        {
            cout << "Введите индексы элементов массива, которые хотите поменять: ";
            cin >> index_1 >> index_2;

            // Замена элементов у не отсортированного массива
            start = steady_clock::now();
            x = Nums[index_1];
            Nums[index_1] = Nums[index_2];
            Nums[index_2] = x;
            end = steady_clock::now();
            result = duration_cast<nanoseconds>(end - start);
            cout << "\nВремя замены у не отсортированного массива: " << result.count() << " (наносек.)\n";
            cout << "Итог: [";
            for (int i = 0; i < 100; i++) {
                cout << Nums[i] << " ";
            }
            cout << "]\n\n";

            // Замена элементов у отсортированного массива
            start = steady_clock::now();
            x = Sort_Nums[index_1];
            Sort_Nums[index_1] = Sort_Nums[index_2];
            Sort_Nums[index_2] = x;
            end = steady_clock::now();
            result = duration_cast<nanoseconds>(end - start);
            cout << "\nВремя замены у отсортированного массива: " << result.count() << " (наносек.)\n";
            cout << "Итог: [";
            for (int i = 0; i < 100; i++) {
                cout << Sort_Nums[i] << " ";
            }
            cout << "]\n\n";
        }

        // Меню
        cout << "\t\tМеню\n1) Создать новый массив.\n2) Отсортировать созданный массив.\n3) Найти максимальный и мнимальный элементы в двух массивах.\n4) Среднее значение максимального и минимального значений и индексы элементов равные ему.\n5) Вывести количество элементов, которые меньше введенного числа.\n6) Вывести количество элементов, которые больше введенного числа.\n7) Поменять местами элементы массивов.\n0) Выход.\n";
        while (true) {
            cout << "\nВведите номер пункта, который хотите запустить: ";
            cin >> Point;
            if (Point >= 0 & Point <= 7)
            {
                cout << "\nЗапускаю пункт под номером: " << Point << "\n\n";
                break;
            }
            else
                cout << "\nНе понимаю...\n";
        }

        // Выход
        if (Point == 0)
        {
            cout << "\nВыхожу";
            break;
        }
    }
}
