# NillionVerifier-TR

Öncelikle aşağıdaki özelliklerde bir VPS'e ihtiyacımız var.
* 2Core / 4Ram / 50GBSSD

## Docker kurulumu
```
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

docker --version
```

# Verifier
### Docker'dan imajı çekelim
```
docker pull nillion/verifier:v1.0.1
```

### Verifier dosyasını oluşturalım 
```
mkdir -p nillion/verifier
```

### Verifier'ı Ayarlayalım
```console
docker run -v ./nillion/verifier:/var/tmp nillion/verifier:v1.0.1 initialise

# Aşağıdaki komutla cüzdan bilgilerinizi göreceksiniz, kopyalayın
cat ~/nillion/verifier/credentials.json
```
# Dashboard 
## Faucet Alma
> **Başka** bir [keplr](https://chromewebstore.google.com/detail/keplr/dmkamcknogkgcdfhhbddcghachkejeap) cüzdanınızı [siteye](https://faucet.testnet.nillion.com/) bağlayın ve hem az önce kopyaladığınız verifier cüzdanınız hem de siteye bağladığınız cüzdanınız için faucet alın.

## Kayıt
> Dashboard'a gidelim > https://verifier.nillion.com/verifier
> "Linux" seçin ve doğrudan 5. adıma geçin, cat komutu ile görüp kopyaladığınız ```Verifier Account ID``` ve ```Verifier Public Key``` kısımlarını doldurun.

Her şey doğruysa fotoğfraftaki gibi bir çıktı görmelisiniz.
<img width="877" alt="Screenshot 2024-11-15 at 19 05 51" src="https://github.com/user-attachments/assets/df9338d0-06f8-4228-8c79-e002b2482a0d">

# Son adım
### Screen'de çalıştıralım
```
screen -S nillion

docker run -v ./nillion/verifier:/var/tmp nillion/verifier:v1.0.1 verify --rpc-endpoint "https://testnet-nillion-rpc.lavenderfive.com"
```
<img width="1467" alt="Screenshot 2024-11-15 at 19 09 57" src="https://github.com/user-attachments/assets/74334453-0460-4dce-8227-59915da14cb7">

Screenden çıkmak için: ```Ctrl + A + D``` komutunu, tekrar giriş yapmak için ise ```screen -r nillion``` komutunu kullanabilirsiniz. 

# Yedek alma
nillion/verifier/credentials.json dizinindeki credentials dosyasının SFTP ile bilgisayarınıza yedeğini alın.

## Opsiyonel
Dashboard'da Verifier staking impactınızı artırmak isterseniz 0.05 $ETH stake edebilirsiniz. Ekip bunun zorunlu olmadığını, sybil önleme mekanizmasının bir parçası olduğunu belirtti.

> Takıldığınız bir yer olursa: ▪️ X : https://x.com/256_tr ▪️ X : https://x.com/256__en 
> Bol kazançlar 256 fam.
