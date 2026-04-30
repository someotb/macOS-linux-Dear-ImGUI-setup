# macOS/Linux Dear ImGUI support

Кросс-платформенное приложение на Dear ImGui с бэкендом GLFW + OpenGL3.
Работает на **macOS** и **Linux (Debian/Ubuntu)**.

---

## Стек

| Компонент | Роль |
|---|---|
| [Dear ImGui](https://github.com/ocornut/imgui) | UI фреймворк |
| [GLFW](https://www.glfw.org/) | Окно + ввод (мышь/клавиатура) |
| OpenGL 3.3 | Рендеринг |

---

## Зависимости

### macOS

Нужен [Homebrew](https://brew.sh/). Если не установлен:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Затем ставим GLFW:

```bash
brew install glfw
```

### Linux (Debian / Ubuntu)

```bash
sudo apt update
sudo apt install build-essential cmake libglfw3-dev libgl1-mesa-dev
```

---

## Клонирование

```bash
git clone --recurse-submodules https://github.com/someotb/macOS-linux-Dear-ImGUI-setup
cd gui_test
```

> Флаг `--recurse-submodules` нужен чтобы подтянуть Dear ImGui автоматически.
> Если уже склонировал без него — выполни:
> ```bash
> git submodule update --init --recursive
> ```

---

## Сборка

```bash
mkdir build && cd build
cmake ..
cmake --build . -j$(nproc 2>/dev/null || sysctl -n hw.logicalcpu)
```

---

## Запуск

```bash
# Из папки build:
./gui_test
```

---

## Структура проекта

```
gui_test/
├── CMakeLists.txt
├── README.md
├── src/
│   └── main.cpp          ← точка входа, здесь пишешь UI
└── third_party/
    └── imgui/            ← Dear ImGui (git submodule)
```

---

## Возможные проблемы

### macOS: warnings про deprecated OpenGL

Apple пометила OpenGL как deprecated начиная с macOS 10.14, но он продолжает работать.
Warnings заглушены флагом `GL_SILENCE_DEPRECATION` в CMakeLists.txt — ничего делать не нужно.

### Linux: ошибка `cannot find -lGL`

```bash
sudo apt install libgl1-mesa-dev
```

### CMake не находит GLFW

**macOS:** убедись что Homebrew установлен в стандартный путь (`/opt/homebrew` на Apple Silicon или `/usr/local` на Intel).
