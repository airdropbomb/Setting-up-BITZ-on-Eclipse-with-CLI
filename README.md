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

## GLIBC version ပြသာနာ များသောအားဖစ်တက်ပါတယ် not found ဆိုတဲ့ပြသာနာပါ
/root/.avm/bin/anchor-0.31.0: /lib/x86_64-linux-gnu/libm.so.6: version `GLIBC_2.38' not found (required by /root/.avm/bin/anchor-0.31.0)
Anchor CLI (version 0.31.0) ထည့်သွင်းပြီးတဲ့အခါ အလုပ်မလုပ်တဲ့ ပြဿနာက GLIBC (GNU C Library) ဗားရှင်းနဲ့ ဆိုင်ပါတယ်။ Error message အရ Anchor CLI က GLIBC 2.38 နဲ့ 2.39 လိုအပ်ပေမယ့် သင့်စက်မှာ ဒီဗားရှင်းတွေ မရှိဘူးလို့ ပြောနေပါတယ်။ ဒါဟာ သင့် operating system ရဲ့ GLIBC ဗားရှင်းက နောက်ကျနေတာကြောင့်ပါ။

Anchor CLI ကို Source ကနေ Build လုပ်ပါ:
Anchor CLI ရဲ့ source code ကို clone လုပ်ပြီး build လုပ်ပါ:
```
git clone https://github.com/coral-xyz/anchor.git
cd anchor
git checkout v0.31.0
cargo build --release
```

Build လုပ်ထားတဲ့ Binary ကို သုံးပါ:
Build ပြီးရင် binary ကို ./target/release/anchor မှာ တွေ့ပါလိမ့်မယ်။

```
sudo cp ./target/release/anchor /usr/local/bin/
```

## version ပြန်စစ်ပါ

```
anchor --version
```

## Not found ပဲပြနေသေးတယ်ဆိုရင် /root/.avm/bin/anchor-0.31.0 ကို သုံးနေတာကိုပါ။ ဒါက သင်အရင်ထည့်သွင်းထားတဲ့ Anchor CLI (AVM ကနေ ထည့်ထားတဲ့ binary) ကို ဆွဲသုံးနေတာဖြစ်ပြီး သင်အသစ် build လုပ်ထားတဲ့ binary (/usr/local/bin/anchor) ကို မသုံးပါဘူး။ အာ့တော့ သုံးအောင်လုပ်ရပါမယ်

AVM ရဲ့ binary ကို ဖယ်ရှားပါ:
```
sudo rm -rf /root/.avm
```

PATH ထဲက AVM ကို ဖယ်ရှားပါ:

```
cat ~/.bashrc
```

အကယ်၍ /root/.avm/bin နဲ့ ပတ်သက်တဲ့ line တွေ့ရင် (ဥပမာ export PATH="$HOME/.avm/bin:$PATH") အဲဒါကို ဖယ်ရှားပါ။

```
nano ~/.bashrc
```

ဖယ်ရှားပြီးရင် save လုပ်ပြီး:

```
source ~/.bashrc
```

Build လုပ်ထားတဲ့ Anchor Binary ကို သုံးဖို့ အောက်ကအဆင့်တွေ လုပ်မယ်

Binary ရှိမရှိ စစ်ဆေးပါ:

```
ls -l /usr/local/bin/anchor
```

အကယ်၍ binary ရှိရင် ဆက်လုပ်ပါ။ မရှိရင် သင် build လုပ်ထားတဲ့ binary ကို ပြန်ကူးထည့်ပါ:

```
sudo cp ~/anchor/target/release/anchor /usr/local/bin/
```

PATH ကို စစ်ဆေးပါ:
$PATH ထဲမှာ /usr/local/bin ပါမပါ စစ်ပါ:

```
echo $PATH.
```

/usr/local/bin ပါရမယ်။ မပါရင် ထည့်ပါ:

```
echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

## version ပြန်စစ်ပါ

```
anchor --version
```

## Not found တော့မပေါ်တော့ဘူး ဒါပေမယ့် avm not set လို့ပြနေရင် အောက်အဆင့်တွေဆက်လုပ်ပါ

```
sudo rm -rf /root/.avm
sudo rm -rf /root/.cache/avm
sudo rm -rf /root/.local/share/avm
```

avm command က ဘယ်ကလာလဲ စစ်ပါ:

```
which avm
```

## /root/.cargo/bin/avm ဆိုရင် AVM ကို Cargo ထဲက ဖယ်ရှားပါ

```
rm -f /root/.cargo/bin/avm
```

AVM နဲ့ ဆက်စပ်တဲ့ Anchor Binary တွေ ရှိမရှိ စစ်ပါ:
/root/.cargo/bin/ ထဲမှာ anchor binary ရှိမရှိ စစ်ဆေးပြီး ရှိရင် ဖယ်ရှားပါ:

```
ls /root/.cargo/bin/
rm -f /root/.cargo/bin/anchor
```

AVM ဖယ်ရှားပြီးမှန်း စစ်ဆေးပါ:

```
which avm
which anchor
```

which avm က ဘာမှ မပြသင့်ပါဘူး

which anchor က /usr/local/bin/anchor လို့ ပြရမှာပါ


## version ပြန်စစ်ပါ

```
anchor --version
```


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
