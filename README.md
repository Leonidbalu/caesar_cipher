def run_caesar_cipher():

    #Основная функция для работы шифра Цезаря через консоль

    print("=== Шифр Цезаря ===")
    print("1 - Зашифровать")
    print("2 - Расшифровать")

    # Получаем выбор действия
    view = input("Выберите действие (1 или 2): ")

    # Получаем текст
    text = input("Введите текст: ")

    # Получаем сдвиг
    try:
        shift = int(input("Введите сдвиг: "))
    except ValueError:
        print("Ошибка: сдвиг должен быть числом!")
        input("Нажмите Enter для выхода...")  # Ожидание
        return

    # Обрабатываем текст
    result = process_caesar_cipher(text, shift, view)

    # Выводим результат
    print("\nРезультат:")
    print(result)

    input("Нажмите Enter для выхода...")  # Ожидание перед закрытием

def process_caesar_cipher(text, shift, view):

    #Обрабатывает текст по алгоритму шифра Цезаря

    result = ""
    # Алфавиты
    eng_lower = "abcdefghijklmnopqrstuvwxyz"
    eng_upper = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    rus_lower = "абвгдеёжзийклмнопрстуфхцчшщъыьэюя"
    rus_upper = "АБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЪЫЬЭЮЯ"

    # Если режим расшифровки, меняем направление сдвига
    if view == '2':
        shift = -shift

    # Оптимизация для больших сдвигов
    shift_eng = shift % 26
    shift_rus = shift % 33

    # Обрабатываем каждый символ
    for char in text:
        if char in eng_lower:
            idx = (eng_lower.index(char) + shift_eng) % 26
            result += eng_lower[idx]
        elif char in eng_upper:
            idx = (eng_upper.index(char) + shift_eng) % 26
            result += eng_upper[idx]
        elif char in rus_lower:
            idx = (rus_lower.index(char) + shift_rus) % 33
            result += rus_lower[idx]
        elif char in rus_upper:
            idx = (rus_upper.index(char) + shift_rus) % 33
            result += rus_upper[idx]
        else:
            result += char  # остальные символы без изменений

    return result

def encrypt(text, shift):   #Функция для шифрования текста

    return process_caesar_cipher(text, shift, '1')

def decrypt(text, shift):    #Функция для расшифровки текста

    return process_caesar_cipher(text, shift, '2')


# Запуск программы при непосредственном выполнении файла
if __name__ == "__main__":
