```
$ git clone git@github.com:narutyo/backpack-sample.git
$ cd backpack-sample
$ git submodule update --init --recursive
$ git submodule foreach git checkout master
$ docker-compose up -d --build

# コンテナが立ち上がってから...
※submodules/backpack直下にauth.jsonファイルを配置してください。
$ docker-compose exec backpack composer install
$ docker-compose exec backpack php artisan migrate --seed
$ sudo find submodules/backpack/storage -type d -exec chmod 777 {} +
$ sudo find submodules/backpack/storage -type f -exec chmod 666 {} +

# ２回目以降は --build 無しでOKです
$ cd backpack
$ docker-compose up -d
```
