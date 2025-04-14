# Setting-up-BITZ-on-Eclipse-with-CLI
-----

## 💡 Bitz Miner Setup Guide on Eclipse
### Bitz is the first ePOW (Eclipse Proof-of-Work) token anyone can mine with just CPU power.
![image](https://github.com/user-attachments/assets/61d28bc6-05b0-4671-8083-42ee706836e8)

 *	⚡️ 5 million maximum supply
 
 *	🔒 No pre-mining or insider allocation

 *	Token Contract:
https://eclipsescan.xyz/token/64mggk2nXg6vHC1qCdsZdEFzd5QGN4id54Vbho4PswCF
 
 
----

## 🧰 Prerequisites
### Before getting started, make sure you have the following:
	
 * A Linux-based system (Ubuntu 20.04+ or WSL on Windows)
 * A Backpack wallet (or another Eclipse-compatible wallet) [Download](https://chromewebstore.google.com/detail/backpack/aflkmfhebedbjioipglgcbcmnbpgliof)
 * 0.005+ ETH on the Eclipse network
---


 ## Getting Started 

 ### Prepare Environment 
![image](https://github.com/user-attachments/assets/35093e13-2ab7-44a2-9732-ee50a3ba94b6)

 ```
sudo apt update && sudo apt upgrade -y
sudo apt install curl nano build-essential -y
```


## Build Screen from Source 
screen install လုပ်ပီးသားဆိုမလိုဘူးကျော်

```
sudo apt install autoconf make gcc libutempter-dev libpam0g-dev libncurses5-dev -y
curl -O https://ftp.gnu.org/gnu/screen/screen-4.9.1.tar.gz
tar -xzf screen-4.9.1.tar.gz
cd screen-4.9.1
./configure
make
sudo make install
```

### Check screen version 
```
screen --version 
```
![image](https://github.com/user-attachments/assets/e8201671-09bb-41bd-8187-c8d3a48b49a8)


### Install RUST (ကိုယ့်စက်ထဲမှာသွင်းပီးသားလားစစ် သွင်းပီးသားဆိုကျော်)
```
rustc --version
```
## မသွင်းရသေးရင်သွင်း
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
![image](https://github.com/user-attachments/assets/c1da2f88-b8b2-4f2b-8dd7-9850684edc5c)

Press ```1``` to proceed 

```
source $HOME/.cargo/env
```

---

## Install Solana CLI 
```
curl --proto '=https' --tlsv1.2 -sSfL https://solana-install.solana.workers.dev | bash 
```
![image](https://github.com/user-attachments/assets/ddd9d674-bb44-422e-94d4-581d22517028)


### After Installation, reload terminal 
```
source $HOME/.bashrc
```
![image](https://github.com/user-attachments/assets/d5e230be-c10f-4ec7-98c3-feaac3c734c0)


### Check Version (ဒီ command ကို run လို့ version မပြရင် vps ကို reboot လုပ်)
```
solana --version
```

if using  VPS, and ```Solana not found,```  ```REBOOT``` 
```
reboot
```

---
## Configue RPC for Eclipse 
### This connects CLI to the Eclipse mainnet.

```
solana config set --url https://eclipse.helius-rpc.com/
```
![image](https://github.com/user-attachments/assets/5c80aeb7-b800-4274-97f5-88ace151868c)

---

## Wallet Setup (Solana Keypair)
### Create New Keypair 
```
solana-keygen new
```
Press ```ENTER```  and save the passphrase 


### Exporting PrivateKey from ```ID.json``` 
```
cat ~/.config/solana/id.json
```

* Copy the output (a list of numbers) and import it into Backpack Wallet under “Private Key”.
* Fund the wallet with 0.005+ ETH on Eclipse to activate mining.

## Install Bitz CLI 
### This compiles and installs the Bitz miner directly from source.

```
cargo install bitz
```
![image](https://github.com/user-attachments/assets/38899f2d-0d90-406e-aba8-06c7ab6605ea)



## 🧪 Start Mining Bitz by opening Screen
```
screen -S bitzminer
```

### Start Miner
```
bitz collect
```

### Using Multiple core (ဒါက ကိုယ်က cpu core ဘယ်လောက်သုံးမှာလည်း သတ်မှတ်ပေးရမယ် ကိုယ့်မှာ 8 core ဆို 8 core လုံးအပြည့်မသုံးရဘူးနော် အကုန် shut down ကျကုန်မယ်)
```
bitz collect --cores 4
```

---
### To keep it running in the background:
* Detach screen: ```Ctrl + A + D```
* Reattach screen: ```screen -r bitzminer``
* List screens: ```screen -ls```
* Stop miner: ```Ctrl + C``` inside screen
* Kill screen: ```screen -XS bitzminer quit```


I used 4 cores here (will adjsut appropriately according to my SPEC) 
![image](https://github.com/user-attachments/assets/e13e8177-c43f-4d97-b4a3-f5f9c3bf8df1)


### Claim Mined tokens 
```
bitz claim
```

### Check Wallet status 
```
bitz account

```

## ✅ Final Notes
---
* Always keep a backup of your id.json file and mnemonic
* Bitz mining only works if your wallet is funded with ETH on Eclipse
* You can run this setup on basic VPS (e.g., 1 vCPU, 1GB RAM)

# DONE! 

Join My Channel
[TWITTER](https://x.com/airdropbombnode)
[TELEGRAM](https://t.me/airdropbombnode)
[YOUTUBE](https://youtube.com/@airdropbombnode)
