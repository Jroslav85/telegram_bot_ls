Структура Maven проекта для Telegram бота.

### Структура проекта

```
telegram-bot/
|-- src/
|   |-- main/
|   |   |-- java/
|   |   |   |-- com/
|   |   |   |   |-- yourusername/
|   |   |   |   |   |-- telegrambot/
|   |   |   |   |   |   |-- Bot.java
|   |   |-- resources/
|   |   |   |-- application.properties
|-- .gitignore
|-- pom.xml
|-- README.md
```

- **src/main/java/com/yourusername/telegrambot/**: Директория с исходным кодом вашего бота.
- **src/main/resources/**: Директория для ресурсов, таких как файлы конфигурации.
- **src/test/java/com/yourusername/telegrambot/**: Директория для тестов.
- **pom.xml**: Файл конфигурации Maven, который описывает зависимости и настройки сборки проекта.

### Пример `pom.xml`

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.yourusername</groupId>
    <artifactId>telegram-bot</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Dependency for Telegram Bots library -->
        <dependency>
            <groupId>org.telegram</groupId>
            <artifactId>telegrambots</artifactId>
            <version>5.5.0</version>
        </dependency>

        <!-- Dependency for Telegram Bots API -->
        <dependency>
            <groupId>org.telegram</groupId>
            <artifactId>telegrambots-meta</artifactId>
            <version>5.5.0</version>
        </dependency>

        <!-- Logging dependencies -->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.7.32</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-simple</artifactId>
            <version>1.7.32</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

Для регистрации бота в Telegram необходимо выполнить несколько шагов с использованием специального бота Telegram, называемого BotFather. Вот пошаговая инструкция:

### Шаг 1: Найдите BotFather

1. Откройте приложение Telegram.
2. В строке поиска введите `@BotFather`.
3. Выберите BotFather из списка результатов поиска.

### Шаг 2: Создайте нового бота

1. Нажмите кнопку "Start" или введите `/start`, чтобы начать взаимодействие с BotFather.
2. Введите команду `/newbot` и следуйте инструкциям:
   - Вас попросят ввести имя вашего бота. Это имя будет отображаться в списке контактов.
   - Затем вас попросят ввести уникальное имя пользователя для вашего бота, которое должно оканчиваться на `bot` (например, `my_awesome_bot`).

### Шаг 3: Получите токен API

После успешного создания бота BotFather предоставит вам токен API. Этот токен выглядит как строка символов и будет использоваться для аутентификации вашего бота при взаимодействии с Telegram API.

Пример токена:
```
123456789:ABCdefGhIJKlmNoPQrstUVwxyZ1234567890
```

### Шаг 4: Настройте бота

BotFather также предоставляет несколько команд для настройки вашего бота. Вот некоторые из них:

- `/setdescription` - Установить описание вашего бота.
- `/setabouttext` - Установить текст "О боте".
- `/setuserpic` - Установить изображение профиля для вашего бота.
- `/setcommands` - Установить команды для вашего бота.

