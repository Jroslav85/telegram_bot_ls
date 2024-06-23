Библиотека [TelegramBots](https://github.com/rubenlagus/TelegramBots) предоставляет удобный API для создания ботов в Telegram на языке Java. Вот основные классы и интерфейсы, которые вам понадобятся для создания и управления ботами:

### Основные классы

1. **`TelegramBotsApi`**
   - Используется для регистрации и управления ботами.
   ```java
   TelegramBotsApi botsApi = new TelegramBotsApi(DefaultBotSession.class);
   ```

2. **`TelegramLongPollingBot`**
   - Абстрактный класс для создания бота, который будет получать обновления с сервера Telegram с использованием метода long polling.
   ```java
   public class MyBot extends TelegramLongPollingBot {
       @Override
       public void onUpdateReceived(Update update) {
           // Обработка обновлений
       }
   }
   ```

3. **`TelegramWebhookBot`**
   - Абстрактный класс для создания бота, который будет получать обновления через вебхуки.
   ```java
   public class MyBot extends TelegramWebhookBot {
       @Override
       public BotApiMethod<?> onWebhookUpdateReceived(Update update) {
           // Обработка обновлений
       }
   }
   ```

4. **`Update`**
   - Представляет обновление, полученное от Telegram. Содержит информацию о сообщениях, командах и других событиях.
   ```java
   if (update.hasMessage()) {
       Message message = update.getMessage();
   }
   ```

5. **`SendMessage`**
   - Используется для отправки текстовых сообщений пользователям.
   ```java
   SendMessage message = new SendMessage();
   message.setChatId(chatId);
   message.setText("Hello, world!");
   ```

### Основные интерфейсы

1. **`IBot`**
   - Основной интерфейс для всех ботов. Определяет методы для получения имени бота и токена.
   ```java
   public interface IBot {
       String getBotUsername();
       String getBotToken();
   }
   ```

2. **`WebhookBot`**
   - Интерфейс для ботов, использующих вебхуки. Расширяет `IBot` и добавляет метод для получения пути вебхука.
   ```java
   public interface WebhookBot extends IBot {
       String getBotPath();
   }
   ```

### Примеры использования

#### Пример Long Polling бота:

```java
import org.telegram.telegrambots.bots.TelegramLongPollingBot;
import org.telegram.telegrambots.meta.api.objects.Update;
import org.telegram.telegrambots.meta.api.methods.send.SendMessage;
import org.telegram.telegrambots.meta.exceptions.TelegramApiException;

public class MyLongPollingBot extends TelegramLongPollingBot {

    @Override
    public String getBotUsername() {
        return "YourBotUsername";
    }

    @Override
    public String getBotToken() {
        return "YOUR_BOT_TOKEN";
    }

    @Override
    public void onUpdateReceived(Update update) {
        if (update.hasMessage() && update.getMessage().hasText()) {
            String messageText = update.getMessage().getText();
            long chatId = update.getMessage().getChatId();

            SendMessage message = new SendMessage();
            message.setChatId(String.valueOf(chatId));
            message.setText("You sent: " + messageText);

            try {
                execute(message);
            } catch (TelegramApiException e) {
                e.printStackTrace();
            }
        }
    }
}
```

#### Регистрация Long Polling бота:

```java
import org.telegram.telegrambots.meta.TelegramBotsApi;
import org.telegram.telegrambots.meta.exceptions.TelegramApiException;
import org.telegram.telegrambots.updatesreceivers.DefaultBotSession;

public class Main {
    public static void main(String[] args) {
        try {
            TelegramBotsApi botsApi = new TelegramBotsApi(DefaultBotSession.class);
            botsApi.registerBot(new MyLongPollingBot());
        } catch (TelegramApiException e) {
            e.printStackTrace();
        }
    }
}
```

Эти основные классы и интерфейсы помогут вам начать работу с библиотекой TelegramBots и создать собственного Telegram-бота.

Конечно! Давайте создадим простого Telegram бота, который будет наследовать `TelegramLongPollingBot`. Мы переопределим методы `getBotUsername()`, `getBotToken()` и `onUpdateReceived()`, а также создадим класс `Main` для запуска бота и регистрации его в `TelegramBotsApi`.

### Шаг 1: Создание класса бота

Создадим класс `MySimpleBot`, который будет наследовать `TelegramLongPollingBot`.

```java
import org.telegram.telegrambots.bots.TelegramLongPollingBot;
import org.telegram.telegrambots.meta.api.methods.send.SendMessage;
import org.telegram.telegrambots.meta.api.objects.Update;
import org.telegram.telegrambots.meta.exceptions.TelegramApiException;

public class MySimpleBot extends TelegramLongPollingBot {

    // Метод для получения имени бота
    @Override
    public String getBotUsername() {
        return "YourBotUsername"; // Замените на имя вашего бота
    }

    // Метод для получения токена бота
    @Override
    public String getBotToken() {
        return "YOUR_BOT_TOKEN"; // Замените на токен вашего бота
    }

    // Метод для обработки полученных обновлений
    @Override
    public void onUpdateReceived(Update update) {
        // Проверяем, есть ли сообщение и текст в этом сообщении
        if (update.hasMessage() && update.getMessage().hasText()) {
            String messageText = update.getMessage().getText(); // Текст полученного сообщения
            long chatId = update.getMessage().getChatId(); // ID чата, откуда пришло сообщение

            // Создаем объект SendMessage для отправки ответа
            SendMessage message = new SendMessage();
            message.setChatId(String.valueOf(chatId)); // Устанавливаем ID чата
            message.setText("You sent: " + messageText); // Устанавливаем текст ответа

            try {
                // Отправляем сообщение
                execute(message);
            } catch (TelegramApiException e) {
                e.printStackTrace();
            }
        }
    }
}
```

### Шаг 2: Создание класса Main для запуска бота

Теперь создадим класс `Main`, который будет использовать `TelegramBotsApi` для регистрации и запуска нашего бота.

```java
import org.telegram.telegrambots.meta.TelegramBotsApi;
import org.telegram.telegrambots.meta.exceptions.TelegramApiException;
import org.telegram.telegrambots.updatesreceivers.DefaultBotSession;

public class Main {
    public static void main(String[] args) {
        try {
            // Создаем экземпляр TelegramBotsApi
            TelegramBotsApi botsApi = new TelegramBotsApi(DefaultBotSession.class);

            // Регистрируем нашего бота
            botsApi.registerBot(new MySimpleBot());

            System.out.println("Bot started successfully!");
        } catch (TelegramApiException e) {
            e.printStackTrace();
        }
    }
}
```

### Пояснения к коду

1. **Класс `MySimpleBot`**:
   - Наследуется от `TelegramLongPollingBot`.
   - Переопределяет метод `getBotUsername()`, который возвращает имя бота.
   - Переопределяет метод `getBotToken()`, который возвращает токен бота.
   - Переопределяет метод `onUpdateReceived()`, который обрабатывает входящие обновления. В данном примере бот просто отправляет обратно текст полученного сообщения.

2. **Класс `Main`**:
   - Создает экземпляр `TelegramBotsApi`.
   - Регистрирует бота с помощью метода `registerBot()`.
   - Выводит сообщение в консоль о успешном запуске бота.

### Запуск бота

Для запуска бота:
1. Убедитесь, что у вас есть токен бота, который вы получили от BotFather.
2. Замените `YourBotUsername` и `YOUR_BOT_TOKEN` в классе `MySimpleBot` на реальные значения.
3. Компилируйте и запустите класс `Main`.

Ваш бот должен успешно запуститься и начать обрабатывать сообщения, отправляя обратно текст, который он получает.