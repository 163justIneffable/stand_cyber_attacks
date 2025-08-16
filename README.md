<h1 align="center">Stand ESXi for Cyber Attacks</h1>
<p align="center">
  <em>Дипломная работа (2025) по направлению «Информационная безопасность»</em><br>
  <strong>Практический стенд на базе VMware ESXi для моделирования и отработки кибератак, сетевых атак и  с описанием защитных мер</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Windows-10-0078D6?logo=windows&logoColor=white" alt="Windows 10">
  <img src="https://img.shields.io/badge/VMware-ESXi-555?logo=vmware&logoColor=white" alt="VMware ESXi">
  <img src="https://img.shields.io/badge/Docker-Engine-2496ED?logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/Debian-GNU%2FLinux-A81D33?logo=debian&logoColor=white" alt="Debian">
  <br>
  <img src="https://img.shields.io/badge/Kali-Linux-557C94?logo=kalilinux&logoColor=white" alt="Kali Linux">
  <img src="https://img.shields.io/badge/Ubuntu-Server-E95420?logo=ubuntu&logoColor=white" alt="Ubuntu">
  <img src="https://img.shields.io/badge/PostgreSQL-DB-336791?logo=postgresql&logoColor=white" alt="PostgreSQL">
  <img src="https://img.shields.io/badge/MikroTik-RouterOS-9B9B9B" alt="MikroTik">
</p>

---

## 🧭 О проекте

**Stand ESXi for Cyber Attacks** — это учебно-практический стенд на базе гипервизора **VMware ESXi**, предназначенный для безопасного моделирования реальных атак, с описанием защитных мер.  
Стенд используется для обучения, проверки гипотез, отработки реагирования и анализа инцидентов в контролируемой среде.

**Период разработки:** апрель – июнь 2025 года.  
**Ключевые направления:** Blue Team, Red Team, тестирование уязвимостей, автоматизация развертывания и чуть-чуть сети ^^.

---

## 🔍 Модель угроз (по Банку угроз ФСТЭК)

В ходе работы были реализованы и изучены следующие сценарии атак:

1. **Keylogger (CWE-79)** — внедрение JS через XSS для перехвата нажатий клавиш.
2. **Phishing (CWE-79)** — подмена формы логина через XSS и кража учётных данных.
3. **Stealer (CWE-200)** — эмуляция похищения персональных и корпоративных данных.
4. **Docker Escape (CVE-2022-0492)** — выход за пределы контейнера с доступом к хосту.
5. **DHCP Starvation & Rogue DHCP (CWE-346)** — исчерпание пула адресов и раздача ложных параметров для MITM.
6. **ARP Spoofing (CWE-345)** — подмена ARP-записей для перехвата трафика.
7. **Brute-force (CWE-307)** — перебор паролей для несанкционированного доступа.
8. **QRLJacking (CWE-285)** — захват сессии через подмену QR-кода.

---

## 🎯 Цели проекта

Разработать программный стенд для проведения киберучений по защите инфраструктуры организации от кибератак. Стенд позволит моделировать актуальные угрозы и отрабатывать методы защиты, что повысит готовность персонала к оперативному выявлению и нейтрализации потенциальных угроз.

---

## 🏗 Состав и формирование стенда

**Аппаратная база:** сервер Supermicro  
- CPU: 2× Intel Xeon Silver 4216 (2.10 GHz)  
- RAM: 256 GB DDR4  
- NIC: 2× Intel Ethernet X722  
- SSD: 4 ТБ  
- HDD: 2 ТБ  
- RAID: MegaRAID SAS + Lewisburg SATA  

**Платформа:** VMware ESXi (основной гипервизор)  
На ESXi развёрнут вложенный ESXi как учебный стенд. В нём создано **8 виртуальных машин** и **1 виртуальный маршрутизатор**.

---

### Виртуальные машины

1. **Debian 12** — веб-сервер и СУБД  
   - Docker, PHP, Nginx/Apache, PostgreSQL, pgAdmin  
   - Тестовое приложение с регистрацией, авторизацией, ЛК  

2. **Windows 10** — рабочая станция пользователя  
   - Имитация перехода по фишинговым/XSS-ссылкам, QRLJacking  

3. **Kali Linux** — сетевые атаки  
   - ARP spoofing, brute-force  

4. **Kali Linux** — атаки на DHCP  
   - DHCP Starvation, Rogue DHCP + MITM  

5. **Debian 12** — уязвимый веб-сайт (мишень)  
   - Docker, веб-приложение для тестов атак  

6. **Debian 12** — сайт для DHCP-атак (мишень)  
   - Docker, сервисы для перехвата  

7. **Debian 12** — «портал злоумышленника»  
   - Вредоносные скрипты, приём данных  

8. **Ubuntu** — тест QRLJacking и Docker Escape  

9. **MikroTik RouterOS** — маршрутизатор/цель атаки  
   - DHCP-сервер, OSPF, жертва DHCP-атак  

---

### Минимальные требования по ресурсам (на ВМ)

| ВМ | CPU | RAM | HDD | Примечания |
|----|-----|-----|-----|------------|
| Debian (web/db) | 2 vCPU | 4 GB | 50 GB | Docker, PostgreSQL |
| Windows 10 | 4 vCPU | 8 GB | 60 GB | GUI, браузеры |
| Kali Linux (сети) | 2 vCPU | 4 GB | 40 GB | атаки L2/L3 |
| Kali Linux (DHCP) | 2 vCPU | 4 GB | 40 GB | MITM DHCP |
| Debian (мишень) | 2 vCPU | 4 GB | 30 GB | веб-приложение |
| Debian (DHCP мишень) | 2 vCPU | 4 GB | 30 GB | тест DHCP |
| Debian (злоумышленник) | 2 vCPU | 4 GB | 30 GB | сбор данных |
| Ubuntu | 2 vCPU | 4 GB | 30 GB | Docker Escape |
| MikroTik | 1 vCPU | 256 MB | 2 GB | RouterOS |

---

**Итог:** распределение ролей и ресурсов позволяет воспроизводить атаки от L2-сетей до веб-уровня и проверять многоуровневую защиту в условиях, приближённых к реальным.

---

## ⚠️ Дисклеймер

Все сценарии выполнялись в изолированной тестовой среде в учебных целях.  
Применение подобных техник в реальной инфраструктуре без разрешения является нарушением закона.

## 3.1 🖥 Атака с использованием вредоносного кода для перехвата ввода с клавиатуры

**Межсайтовый скриптинг (Cross-Site Scripting, XSS)** — это класс уязвимостей веб-приложений, при котором злоумышленник внедряет произвольный клиентский код в страницу, отображаемую в браузере жертвы. Такой код исполняется в контексте доверенного домена и получает те же права, что и легитимный скрипт сайта: доступ к DOM, cookies сессии, токенам аутентификации, а также полям ввода.

В данном сценарии демонстрируется уязвимость **CWE-79**, позволяющая внедрить вредоносный JavaScript-код, регистрирующий нажатия клавиш пользователя и отправляющий их злоумышленнику.

---

### 🔹 Лабораторный стенд

**Таблица 1 — Конфигурация стенда для атаки keylogger**

| IP-адрес / Порт     | Роль                | Описание |
|---------------------|--------------------|----------|
| `192.168.0.69:2222` | Веб-сервер          | Сайт организации: форма регистрации, авторизации и личный кабинет |
| `192.168.0.69:1111` | pgAdmin4            | Веб-интерфейс администрирования PostgreSQL |
| `192.168.0.69:5432` | PostgreSQL          | База данных сайта |
| `192.168.0.89`      | Клиент *(Windows 10)*| Жертва атаки — открывает ссылку с XSS-payload |
| `192.168.0.114:3333`| Злоумышленник *(Debian)*| Хостинг `keylogger.php` и приём данных (`keylog.txt`) |

---

💡 *Стенд развёрнут в локальной сети с использованием Docker Compose и виртуальных машин.*  
Веб-приложение реализовано на PHP.

---

### 🛠 Этап 1 — Подготовка окружения

> Разворачиваем серверную часть: веб‑приложение на PHP + PostgreSQL в Docker. Этот этап завершится работоспособным сайтом (порт `2222`) и pgAdmin (порт `1111`). В коде намеренно оставлена уязвимость (точки XSS), используемая далее для keylogger‑сценария.

---

## 🔧 Архитектура и роли

* **php (Apache + PHP)** — уязвимое веб‑приложение (порт `2222 → 80`).
* **db (PostgreSQL)** — БД приложения (порт `5432`).
* **pgadmin (pgAdmin4)** — GUI администрирования БД (порт `1111 → 80`).

**Сегмент сети**: DMZ (внутренние связи контейнеров — через Docker‑сеть).
**Где уязвимость:** неконтролируемый вывод параметра `payload` в `login.php` и `dashboard.php` (отсутствует экранирование).

---

## 📦 Docker Compose (серверная часть)

```yaml
version: '3.8'

services:
  db:
    image: postgres:latest
    container_name: postgres_db
    environment:
      POSTGRES_USER: 163justIneffable
      POSTGRES_PASSWORD: P@ssw0rd
      POSTGRES_DB: anubis
    volumes:
      - db_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"

  pgadmin:
    image: dpage/pgadmin4:latest
    container_name: pgadmin
    environment:
      PGADMIN_DEFAULT_EMAIL: *mail*@list.ru
      PGADMIN_DEFAULT_PASSWORD: P@ssw0rd!
    ports:
      - "1111:80"
    depends_on:
      - db

  php:
    build:
      context: .
      dockerfile: Dockerfile
    volumes:
      - ./html:/var/www/html
    ports:
      - "2222:80"
    depends_on:
      - db

volumes:
  db_data:
```

### Dockerfile

```dockerfile
FROM php:apache

RUN apt-get update && \
    apt-get install -y libpq-dev && \
    docker-php-ext-install pgsql pdo_pgsql
```

> *Примечание:* базовый образ `php:apache` уже содержит Apache с конфигурацией виртуального хоста `/var/www/html`.

---

## 🗂 Структура проекта

```
project-root/
├─ docker-compose.yml
├─ Dockerfile
└─ html/
   ├─ index.php
   ├─ register.php
   ├─ login.php
   ├─ dashboard.php
   ├─ logout.php
   └─ db.php
```

Создаём директорию под код:

```bash
mkdir -p html
```

---

## 💾 PHP‑приложение (уязвимые точки отмечены)

### `html/db.php`

```php
<?php
// db.php — подключение к PostgreSQL через PDO
$host = 'db';         // имя сервиса БД из docker-compose
$port = '5432';
$db   = 'anubis';
$user = '163justIneffable';
$pass = 'P@ssw0rd';

$dsn = "pgsql:host=$host;port=$port;dbname=$db;";

try {
    $pdo = new PDO($dsn, $user, $pass, [PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION]);
} catch (PDOException $e) {
    echo "Ошибка подключения к БД: " . $e->getMessage();
    exit();
}
```

### `html/index.php`

```php
<?php
session_start();
?>
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Главная страница</title>
</head>
<body>
    <h1>Добро пожаловать на сайт</h1>
    <p>
      <a href="register.php">Регистрация</a> |
      <a href="login.php">Вход</a>
    </p>
    <?php
      if(isset($_SESSION['username'])) {
          echo "<p>Привет, " . $_SESSION['username'] . "!</p>";
          echo '<p><a href="dashboard.php">Перейти в личный кабинет</a></p>';
      }
    ?>
</body>
</html>
```

### `html/register.php`

```php
<?php
session_start();
require 'db.php';

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $username = $_POST['username'];
    $password = $_POST['password'];
    $bio = $_POST['bio'];

    // ⚠️ Демонстрационно: без хэширования (уязвимо по CWE-79)
    $sql = "INSERT INTO users (username, password, bio) VALUES (:username, :password, :bio)";
    $stmt = $pdo->prepare($sql);
    $stmt->bindValue(':username', $username);
    $stmt->bindValue(':password', $password);
    $stmt->bindValue(':bio', $bio);

    try {
        $stmt->execute();
        $_SESSION['username'] = $username;
        header("Location: dashboard.php");
        exit();
    } catch (PDOException $e) {
        echo "Ошибка при регистрации: " . $e->getMessage();
    }
}
?>
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Регистрация</title>
</head>
<body>
    <h1>Регистрация</h1>
    <form method="POST">
        <label>Имя пользователя:</label><br>
        <input type="text" name="username" required><br><br>

        <label>Пароль:</label><br>
        <input type="password" name="password" required><br><br>
        
        <label>О себе (bio):</label><br>
        <textarea name="bio" rows="4" cols="50" placeholder="Расскажи о себе"></textarea><br><br>
        
        <input type="submit" value="Зарегистрироваться">
    </form>
    <p>Уже зарегистрированы? <a href="login.php">Войти</a></p>
</body>
</html>
```

### `html/login.php`

```php
<?php
session_start();
require 'db.php';

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $username = $_POST['username'];
    $password = $_POST['password'];

    $sql = "SELECT * FROM users WHERE username = :username";
    $stmt = $pdo->prepare($sql);
    $stmt->bindValue(':username', $username);
    $stmt->execute();
    $user = $stmt->fetch(PDO::FETCH_ASSOC);

    // ⚠️ Демонстрационно: сравнение с открытым текстом
    if ($user && $user['password'] === $password) {
        $_SESSION['username'] = $username;
        header("Location: dashboard.php");
        exit();
    } else {
        $error = "Неверное имя пользователя или пароль";
    }
}

// ⚠️ Уязвимость XSS: вывод без экранирования
if (isset($_GET['payload'])) {
    echo $_GET['payload'];
}
?>
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Вход</title>
</head>
<body>
    <h1>Вход</h1>
    <?php if(isset($error)) { echo "<p style='color:red;'>" . $error . "</p>"; } ?>
    <form method="POST">
        <label>Имя пользователя:</label><br>
        <input type="text" name="username" required><br><br>
        
        <label>Пароль:</label><br>
        <input type="password" name="password" required><br><br>
        
        <input type="submit" value="Войти">
    </form>
    <p>Нет аккаунта? <a href="register.php">Зарегистрироваться</a></p>
</body>
</html>
```

### `html/dashboard.php`

```php
<?php
session_start();
require 'db.php';

if (!isset($_SESSION['username'])) {
    header("Location: login.php");
    exit();
}

$username = $_SESSION['username'];

// Обновление bio
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $newBio = $_POST['bio'] ?? '';
    $sql = "UPDATE users SET bio = :bio WHERE username = :username";
    $stmt = $pdo->prepare($sql);
    $stmt->bindValue(':bio', $newBio);
    $stmt->bindValue(':username', $username);
    $stmt->execute();
}

// Получение профиля
$sql = "SELECT * FROM users WHERE username = :username";
$stmt = $pdo->prepare($sql);
$stmt->bindValue(':username', $username);
$stmt->execute();
$user = $stmt->fetch(PDO::FETCH_ASSOC);

if (!$user) {
    header("Location: login.php");
    exit();
}
?>
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Личный кабинет</title>
</head>
<body>
    <h1>Добро пожаловать, <?php echo htmlspecialchars($user['username']); ?>!</h1>

    <?php
    // ⚠️ Уязвимость XSS: вывод без экранирования
    if (isset($_GET['payload'])) {
        echo $_GET['payload'];
    }
    ?>

    <p><strong>О себе (bio):</strong> <?php echo $user['bio']; ?></p>

    <h2>Редактировать «О себе»</h2>
    <form method="POST">
        <textarea name="bio" rows="4" cols="50"><?php echo $user['bio']; ?></textarea><br>
        <input type="submit" value="Сохранить">
    </form>

    <p><a href="logout.php">Выйти</a></p>
</body>
</html>
```

### `html/logout.php`

```php
<?php
session_start();
session_destroy();
header("Location: index.php");
exit();
```

---

## 🗃 Инициализация БД (через pgAdmin или psql)

**Схема и таблица пользователей:**

```sql
CREATE TABLE IF NOT EXISTS users (
  id SERIAL PRIMARY KEY,
  username VARCHAR(64) UNIQUE NOT NULL,
  password VARCHAR(255) NOT NULL,
  bio TEXT DEFAULT ''
);
```
## В рамках демострации пароли в открытом виде в базе данных хранятся, очевидно, что так не должно быть, можно использовать хеширования

**Регистрация с хэшированием пароля**
```
// Получаем пароль из формы
$password = $_POST['password'];

// Генерируем хэш с использованием алгоритма bcrypt
$passwordHash = password_hash($password, PASSWORD_BCRYPT);

// Сохраняем в БД
$sql = "INSERT INTO users (username, password_hash, bio) VALUES (:username, :password_hash, :bio)";
$stmt = $pdo->prepare($sql);
$stmt->bindValue(':username', $username);
$stmt->bindValue(':password_hash', $passwordHash);
$stmt->bindValue(':bio', $bio);
$stmt->execute();

```
**Авторизация с проверкой пароля**
```
$sql = "SELECT * FROM users WHERE username = :username";
$stmt = $pdo->prepare($sql);
$stmt->bindValue(':username', $username);
$stmt->execute();
$user = $stmt->fetch(PDO::FETCH_ASSOC);

if ($user && password_verify($password, $user['password_hash'])) {
    $_SESSION['username'] = $username;
    header("Location: dashboard.php");
    exit();
} else {
    $error = "Неверное имя пользователя или пароль";
}
```
**Таблица пользователей с безопасным хранением пароля**
```
CREATE TABLE IF NOT EXISTS users (
  id SERIAL PRIMARY KEY,
  username VARCHAR(64) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  bio TEXT DEFAULT ''
);
```

> Через **pgAdmin** подключитесь к хосту `db:5432` (изнутри сети Docker) или к `localhost:1111` PgAdmin4 через браузер. Подключитесь БД `anubis`, затем выполните SQL для таблицы `users`.

📎 *Место для скриншота создания таблицы в pgAdmin:*
![СКРИН — Создание таблицы users](вставлю позже)

---

## ▶️ Запуск и проверка

1. Собрать и запустить контейнеры:

   ```bash
   docker compose up -d --build
   ```
2. Проверить контейнере в режиме CLI
```
root@dock:~# docker ps -a
CONTAINER ID   IMAGE                   COMMAND                  CREATED          STATUS          PORTS
                            NAMES
404652693b31   dpage/pgadmin4:latest   "/entrypoint.sh"         42 minutes ago   Up 42 minutes   443/tcp, 0.0.0.0:1111->80/tcp, [::]:1111->80/tcp   pgadmin
312c834e57dc   test-xss-php            "docker-php-entrypoi…"   42 minutes ago   Up 42 minutes   0.0.0.0:2222->80/tcp, [::]:2222->80/tcp            test-xss-php-1
4e5491887cbc   postgres:latest         "docker-entrypoint.s…"   42 minutes ago   Up 42 minutes   0.0.0.0:5432->5432/tcp, [::]:5432->5432/tcp        postgres_db
root@dock:~#
```
3. Проверить доступность сервисов:

   * Приложение: `http://<ip>:2222`
   * pgAdmin: `http://<ip>:1111`
4. Зарегистрировать тестового пользователя и войти в **ЛК**.
5. Убедиться, что параметр `payload` отрисовывается *как есть* (демонстрационная уязвимость XSS), например:

   ```
   http://<ip>:2222/login.php?payload=<script>alert('xss')</script>
   ```

📎 *Места для скриншотов проверки:*

* ![СКРИН — Приложение на 2222](вставь_путь_к_скрину)
* ![СКРИН — Успешный вход и ЛК](вставь_путь_к_скрину)
* ![СКРИН — Демонстрация XSS через payload](вставь_путь_к_скрину)

---

## ⚠️ Замечания по безопасности (для раздела «Рекомендации»)

* Пароли **не** должны храниться в открытом виде — используйте `password_hash()/password_verify()` (CWE‑522).
* Любой пользовательский ввод должен выводиться с **экранированием**, предпочтительно — контекстно‑зависимым.
* Рассмотрите внедрение **CSP** (`script-src 'self'`) и включение **HttpOnly/SameSite** для cookies.
* Для production храните секреты в `.env`/секрет‑менеджере, а не в `docker‑compose.yml`.

## Дописавать буду в ближайшее время...
