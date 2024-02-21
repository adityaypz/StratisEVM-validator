# Stratis-Node
Tutorial Stratis Node

## Bahan

- VPS
- Mobaterm X (PC) atau Putty < Disarankan untuk menggunakan mobaterm agar lebih mudah dipahami untuk pemula.

## RPC

Network Name 
```
Auroria
```
RPC URL 
```
https://auroria.rpc.stratisevm.com
```
CID 
```
205205
```
Symbol 
```
STRAX
```
Explorer 
```
https://auroria.explorer.stratisevm.com
```

## Tutorial 

# 1. Setting VPS

Masukan command 

``` 
 sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y && sudo apt install unzip make clang pkg-config libssl-dev build-essential git jq llvm libudev-dev -y
```

Kalau ada perintah [Y/n] ketik Y dan Enter dan jika muncul prompt atau pop up klik OK OK aja


Jika sudah selesai atur firewallnya

# 2. Firewall

``` 
ufw allow 8551
ufw allow 22
ufw allow 8080
ufw allow 443
ufw allow 8545
ufw allow 13000
ufw allow 3500
ufw allow 12000
ufw allow 4000
ufw allow 8551
``` 

lanjut

``` 
ufw enable 
```
Jika sudah, lanjut membuat directory agar tidak berantakan

# 3. Setting Directory

``` 
cd
mkdir repos
cd repos
mkdir StratisEVM
cd StratisEVM
mkdir bin
cd bin
``` 

# 4. Download file yang dibutuhkan untuk run validator

``` 
wget https://github.com/stratisproject/go-stratis/releases/download/0.1.1/geth-linux-amd64-5c4504c.tar.gz 
```
```
wget https://github.com/stratisproject/prysm-stratis/releases/download/0.1.1/beacon-chain-linux-amd64-0ebd251.tar.gz
```
```
wget https://github.com/stratisproject/prysm-stratis/releases/download/0.1.1/validator-linux-amd64-0ebd251.tar.gz
```
```
wget https://github.com/stratisproject/staking-deposit-cli/releases/download/0.1.0/staking-deposit-cli-linux-amd64.zip
```
#5. RUN Validator dulu ga sih 

copas 

``` 
sudo tar -xvf geth-linux-amd64-5c4504c.tar.gz
```
lalu bikin screen baru dengan nama "geth" (copy code dibawah)
```
screen -R geth
```
```
./geth --auroria --http --http.api eth,net,engine,admin --datadir=data\testnet\geth --authrpc.addr=127.0.0.1 --authrpc.jwtsecret=jwtsecret --syncmode=full
```
Jika sudah tekan CTRL A+D 

lanjut copas

``` 
sudo tar -xvf beacon-chain-linux-amd64-0ebd251.tar.gz
```
```
sudo tar -xvf validator-linux-amd64-0ebd251.tar.gz
```

Lanjut bikin screen baru bernama "beacon"

```
screen -R beacon
```
copas
```
./beacon-chain --auroria --datadir=data\testnet\beacon --execution-endpoint=http://localhost:8551/ --jwt-secret=jwtsecret --suggested-fee-recipient=<WALLET ADDRESS KALIAN>
```
hapus <>

setelah itu ada confirmation untuk ketik accept lalu enter
tekan CTRL A+D untuk close screen

## bentar nyusu dulu akweoakse

lanjut lagi bang

copas aj
``` 
unzip staking-deposit-cli-linux-amd64.zip

sudo tar -xvf staking-deposit-cli-linux-amd64/staking-deposit-cli-linux-amd64.tar.gz
```
```
./deposit new-mnemonic --num_validators 1 --chain auroria --eth1_withdrawal_address <walletkalian>
```
seperti biasa wallet kalian diganti dengan address dan hapus <>
ketik english lalu enter
english lagi lalu enter

backup mnemonic, masukan ulang 4 huruf pertama dari setiap kata di mnemonic, 
misal: berak dikebon rasanya enak banget
jadi: bera dike rasa enak bang

## Oke lanjut
copas sj langsung
```
  ./validator accounts import --keys-dir=~/repos/StratisEVM/bin/validator_keys --wallet-dir=~/repos/StratisEVM/bin/wallet_dir --auroria
```

Kita akan buat screen bernama "validator"

```
screen -R validator
```
```
./validator --wallet-dir=~/repos/StratisEVM/bin/wallet_dir --auroria --suggested-fee-recipient=<YOUR_WALLET_ADDRESS>
```

your_wallet ganti dengan address mu lalu CTRL A+D

liat folder dimobaxterm kalian, masuk ke repos>StratisEVM>bin, lalu download validator_keys simpan ke komputer kalian.

Ambil Faucet : 
https://auroria.faucet.stratisevm.com/

Buka web : 
https://auroria.launchpad.stratisevm.com/en/

upload file deposit_data ke webnya, file tersebut ada difolder validator_keys yang kalian download tadi.

Galxenya jangan Lupa Kerjain
https://galxe.com/StratisEVM/

untuk tambahan jangan lupa stake di masternode juga, jangan di wd biar elig nanti nya okeeyy 
https://auroria.masternode.stratisevm.com/
