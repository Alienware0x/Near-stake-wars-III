# Near-stake-wars-III
NEAR Team снова запускают Stake Wars, чтобы помочь децентрализовать сеть NEAR. Stake Wars III дает сообществу новые интересные задачи и награды для участников, которые хотят стать валидаторами. В Stake Wars: Episode III NEAR фокусируется на Chunk-Only Producers — следующем шаге NEAR к полностью сегментированному протоколу.

Внедряя этот новый тип валидатора, NEAR увеличивает общее количество валидаторов. Stake Wars помогает Chunk-Only Producers подготовиться к этому моменту. Это возможность научиться работать с делегированием на основе контракта.

![image](https://user-images.githubusercontent.com/110548287/182633670-bbf48483-4231-4919-a00e-2d6df47a0dff.png)

Вознаграждения по программе Stake Wars мотивируют новых участников, которые хотят присоединиться к основной сети в качестве валидатора в конце сентября 2022 года.

Для начал нужно заполнить форму для регистрации Chunk-Only Producer https://nearprotocol1001.typeform.com/to/Z39N7cU9?typeform

После этого нужно создать кошелек, арендовать сервер и произвести запуск ноды. 
# Требования к серверу для Chunk-only Producer

CPU: 4-Core CPU with AVX support

RAM: 8GB DDR4

Storage: 500GB SSD

# Аренда сервера

Подойдёт VPS S на contabo, добавьте к нему 400GB SSD за €1,5 в месяц (В требованиях заявлено 500GB, на практике 400GB достаточно).

![image](https://user-images.githubusercontent.com/110548287/182634066-cf70378c-9788-47de-b4f7-83c32417d69d.png)


# Создание кошелька

Переходим на сайт https://wallet.shardnet.near.org/

Нажимаем “Создать учетную запись”

![image](https://user-images.githubusercontent.com/110548287/182634247-c74f5e92-3324-485a-a5ce-e8c5206c46d8.png)

 
Вводим свободное имя пользователя и нажимаем “Reserve My Account ID”

![image](https://user-images.githubusercontent.com/110548287/182634272-8a2f0828-fcb4-4bf7-81aa-00b927fd08bd.png)

Выберите метод восстановления. Я использую мнемоническую фразу.

![image](https://user-images.githubusercontent.com/110548287/182634311-9e2fa57c-1a89-45e7-babb-3df5e8c435c6.png)

Затем сохраните мнемоническую фразу и введите её

![image](https://user-images.githubusercontent.com/110548287/182634353-3bce0b85-791e-4826-92e9-ce893856ea70.png)

В результате на вашем аккаунте должны появиться токены NEAR

![image](https://user-images.githubusercontent.com/110548287/182634396-d64b9edc-5d12-46f5-913d-4cb9e0cec4f2.png)

# Запуск узла

1.	Подключитесь к серверу и обновите пакеты

```
sudo apt update && sudo apt upgrade -y
```
2. Установите Node.js и npm
```
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -  sudo apt install build-essential nodejs
PATH="$PATH"
```
Проверьте версии:
```
node -v
```
Должен быть ответ: v18.xx
```
npm -v
```
Должен быть ответ: 8.xx


3. Установите NEAR-CLI
```
sudo npm install -g near-cli
```
4. Настройте окружающую среду
```
export NEAR_ENV=shardnet
echo 'export NEAR_ENV=shardnet' >> ~/.bashrc
```
5. Установите инструменты разработчика
```
sudo apt install -y git binutils-dev libcurl4-openssl-dev zlib1g-dev libdw-dev libiberty-dev cmake gcc g++ python docker.io protobuf-compiler libssl-dev pkg-config clang llvm cargo
```
6. Установите Python pip
```
sudo apt install python3-pip
```
7. Установите конфигурацию
```
USER_BASE_BIN=$(python3 -m site --user-base)/bin
export PATH="$USER_BASE_BIN:$PATH"
```
8. Установите Building env
```
sudo apt install clang build-essential make
```
9. Установите Rust & Cargo
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
Выберите “1”
```
source $HOME/.cargo/env
```
10. Клонируйте nearcore репозиторий
```
git clone https://github.com/near/nearcore
cd nearcore
git fetch
```
Далее проверьте <commit> в файле и замените его на значение из файла
```
git checkout <commit>
```

в моём случае команда выглядит так
```
git checkout  c1b047b8187accbf6bd16539feb7bb60185bdc38
```
11. Скомпилируйте бинарный файл
```
cargo build -p neard --release --features shardnet
```
12. Инициализируйте рабочую директорию

Для правильной работы узлу NEAR требуется рабочий каталог и несколько файлов конфигурации.
```
./target/release/neard --home ~/.near init --chain-id shardnet --download-genesis
```
Эта команда создаст структуру каталогов и сгенерирует config.json, node_key.json genesis.json

13. Замените config.json
```
rm ~/.near/config.json
wget -O ~/.near/config.json https://s3-us-west-1.amazonaws.com/build.nearprotocol.com/nearcore-deploy/shardnet/config.json
```
14. Установите AWS Cli
```
sudo apt-get install awscli -y
```
15. Замените genesis.json
```
rm ~/.near/genesis.json
cd ~/.near
wget https://s3-us-west-1.amazonaws.com/build.nearprotocol.com/nearcore-deploy/shardnet/genesis.json
```
 

 
# Активация узла в качестве валидатора

1.	Введите в терминале команду
```
near login
```
2. Затем скопируйте ссылку и вставьте её в браузер

![image](https://user-images.githubusercontent.com/110548287/182634849-a2f4c7d1-e6bb-40aa-861c-14356f759c00.png)



3. Предоставьте полный доступ Near CLI, нажимайте “Next”

![image](https://user-images.githubusercontent.com/110548287/182635278-f1a0dd81-8689-44f9-a194-77eeedbf2a26.png)

4. Далее “Подключить”

![image](https://user-images.githubusercontent.com/110548287/182635624-64f50c7c-f645-47a8-91c3-41008e0317e8.png)

5. Введите вашу учетную запись и нажмите “Подтвердить”

![image](https://user-images.githubusercontent.com/110548287/182635689-2bd60481-cb85-4192-a880-26d4d2c21f2f.png)

Вы должны увидеть такую страницу — это ОК

![image](https://user-images.githubusercontent.com/110548287/182635737-8c218cde-cd75-40ff-967b-fd5134cb5a19.png)

6. Введите в терминале вашу учетную запись на жмите “Enter”

![image](https://user-images.githubusercontent.com/110548287/182636223-a7e5f7c5-4dec-4d03-982f-4a8f1e7dd22f.png)

7. Проверьте validator_key.json
```
cat ~/.near/validator_key.json
```
Если файл validator_key.json отсутствует, выполните следующие действия, чтобы создать его:
```
near generate-key <pool_id>
<pool_id> — -> xx.factory.shardnet.near 
```
где xx это имя вашего пула. Вам нужно придумать его самостоятельно

В моем случае команда выглядит следующим образом:
```
near generate-key alienware1.factory.shardnet.near
```
8. Скопируйте сгенерированный файл в папку shardnet
```
cp ~/.near-credentials/shardnet/YOUR_WALLET.json ~/.near/validator_key.json
```
YOUR_WALLET замените на ваше имя, в моем случае команда выглядит следующим образом:
```
cp ~/.near-credentials/shardnet/alienware.shardnet.near.json ~/.near/validator_key.json
```
9. Отредактируйте validator_key.json
```
nano ~/.near/validator_key.json
```
•	Отредактируйте «account_id» => xx.factory.shardnet.near, где xx — имя вашего пула.

•	Измените private_key на secret_key

Содержимое файла должно соответствовать следующему шаблону:
```
{
  "account_id": "xx.factory.shardnet.near",
  "public_key": "ed25519:HeaBJ3xLgvZacQWmEctTeUqyfSU4SDEnEwckWxd92W2G",
  "secret_key": "ed25519:****"
}
```

Ctrl+s — сохранить файл

Ctrl+x — закрыть файл

10 . Создайте сервисный файл
```
sudo nano /etc/systemd/system/neard.service
```
Вставляем следующий текст в файл:
```
[Unit]
Description=NEARd Daemon Service
[Service]
Type=simple
User=<USER>
#Group=near
WorkingDirectory=/home/<USER>/.near
ExecStart=/home/<USER>/nearcore/target/release/neard run
Restart=on-failure
RestartSec=30
KillSignal=SIGINT
TimeoutStopSec=45
KillMode=mixed
[Install]
WantedBy=multi-user.target
```

! Отредактирует строки USER, WorkingDirectory, ExecStart под ваши значения

Ctrl+s — сохранить файл

Ctrl+x — закрыть файл

11. Запустите узел валидатора
```
sudo systemctl daemon-reloadsudo systemctl enable neardsudo systemctl start neard
```
12. Отобразите цветные логи
```
sudo apt install cczejournalctl -n 100 -f -u neard | ccze -A
``` 
Необходимо дождаться полной синхронизации


# Запуск стейкинг пула

Разверните контракт стейкинг пула, шаблон команды:
```
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "<pool id>", "owner_id": "<accountId>", "stake_public_key": "<public key>", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ"}' --accountId="<accountId>" --amount=450 --gas=300000000000000
```
Замените на свои данные

•	Pool ID: Имя стейкинг пула. Пример: alienware1

•	Owner ID: Shardnet аккаунт. Пример: alienware.shardnet.near

•	Public Key: public key из файла validator_key.json

•	5: Комиссия, которую будет взимать пул

•	Account Id: Shardnet аккаунт. Обычно совпадает с Owner ID

Должно появиться сообщение об успешном создании пула

Проверить пул можно > https://explorer.shardnet.near.org/nodes/validators

![photo_2022-08-03_12-31-50](https://user-images.githubusercontent.com/110548287/182637504-802cf460-de7c-467f-872d-87a7219b1007.jpg)

# Создайте cron задачу для автоматического пинга
```
cd
mkdir scripts
cd scripts
nano ping.sh
```

В тексте файла прописываем:
```
#!/bin/sh
# Ping call to renew Proposal added to crontab
export NEAR_ENV=shardnet
export LOGS=/home/<USER_ID>/logs
export POOLID=<YOUR_POOL_ID>
export ACCOUNTID=<YOUR_ACCOUNT_ID>
echo "---" >> $LOGS/all.log
date >> $LOGS/all.log
near call $POOLID.factory.shardnet.near ping '{}' --accountId $ACCOUNTID.shardnet.near --gas=300000000000000 >> $LOGS/all.log
near proposals | grep $POOLID >> $LOGS/all.log
near validators current | grep $POOLID >> $LOGS/all.log
near validators next | grep $POOLID >> $LOGS/all.log
```

Отредактируйте LOGS, POOLID, ACCOUNTID в зависимости от ваших данных.

# Создайте новый crontab, запускаемый каждые 5 минут:
```
crontab -e
```
Прописываем строку с измененным путем к файлу скрипта:
```
*/5 * * * * sh /home/<USER_ID>/scripts/ping.sh
```
Сохраняем и закрываем файл

Список crontab, чтобы увидеть, что он работает:
```
crontab -l
```
Просмотрите свои логи:
```
cat home/<USER_ID>/logs/all.log
```
GL
