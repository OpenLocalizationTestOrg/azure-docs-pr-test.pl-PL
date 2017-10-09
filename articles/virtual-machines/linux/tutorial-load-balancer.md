---
title: aaaHow tooload saldo maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello Azure obciążenia toocreate równoważenia aplikacji wysokiej dostępności i bezpieczne w trzech maszyn wirtualnych systemu Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>Jak tooload saldo maszyn wirtualnych systemu Linux w Azure toocreate wysokiej dostępności aplikacji
Równoważenie obciążenia sieciowego zapewnia wyższy poziom dostępności dzięki rozproszeniu przychodzące żądania między wieloma maszynami wirtualnymi. Z tego samouczka dowiesz się o hello różnych składników usługi równoważenia obciążenia Azure hello dystrybucji ruchu, które zapewniają wysoką dostępność. Omawiane kwestie:

> [!div class="checklist"]
> * Tworzenie usługi równoważenia obciążenia Azure
> * Utwórz kondycji sondę modułu równoważenia obciążenia
> * Tworzenie reguły ruchu usługi równoważenia obciążenia
> * Użyj toocreate init chmury podstawowej aplikacji Node.js
> * Tworzenie maszyn wirtualnych i Dołącz tooa modułu równoważenia obciążenia
> * Wyświetl modułu równoważenia obciążenia w akcji
> * Dodawanie i usuwanie maszyny wirtualne z modułem równoważenia obciążenia


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="azure-load-balancer-overview"></a>Omówienie usługi równoważenia obciążenia Azure
Moduł równoważenia obciążenia Azure jest równoważenia obciążenia warstwy 4 (TCP, UDP), który zapewnia wysoką dostępność, przekazując przychodzący ruch między maszynami wirtualnymi w dobrej kondycji. Kondycji sondę modułu równoważenia obciążenia monitoruje danego portu na każdej maszynie Wirtualnej, a tylko dystrybuuje ruch tooan operacyjne maszyny Wirtualnej.

Należy zdefiniować frontonu konfiguracji adresu IP, który zawiera co najmniej jeden publiczny adres IP. Ta konfiguracja frontonu IP umożliwia toobe, a aplikacje usługi równoważenia obciążenia dostępny za pośrednictwem hello Internet. 

Maszyny wirtualne połączenie usługi równoważenia obciążenia tooa przy użyciu ich karty interfejsu sieci wirtualnej (NIC). toodistribute toohello ruch maszyn wirtualnych, puli adresów zaplecza zawiera adresy IP hello hello wirtualnych (NIC) toohello podłączonej usługi równoważenia obciążenia.

toocontrol hello przepływu ruchu, należy zdefiniować reguły modułu równoważenia obciążenia dla określonych portów i protokołów, które mapują tooyour maszyn wirtualnych.

Po wykonaniu poprzednich samouczek hello zbyt[utworzyć zestaw skali maszyny wirtualnej](tutorial-create-vmss.md), usługi równoważenia obciążenia został utworzony. Wszystkie te składniki zostały skonfigurowane dla Ciebie jako część zestawu skalowania hello.


## <a name="create-azure-load-balancer"></a>Tworzenie usługi równoważenia obciążenia Azure
W tej sekcji Szczegóły, jak można tworzyć i konfigurować poszczególnych składników usługi równoważenia obciążenia hello. Przed utworzeniem przez moduł równoważenia obciążenia, Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupLoadBalancer* w hello *eastus* lokalizacji:

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a>Tworzenie publicznego adresu IP
tooaccess aplikacji na hello Internet, należy publicznego adresu IP dla modułu równoważenia obciążenia hello. Utwórz publiczny adres IP z [utworzyć az sieci publicznej ip](/cli/azure/network/public-ip#create). Witaj poniższy przykład tworzy publiczny adres IP o nazwie *myPublicIP* w hello *myResourceGroupLoadBalancer* grupy zasobów:

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a>Tworzenie modułu równoważenia obciążenia
Tworzenie modułu równoważenia obciążenia z [utworzyć równoważeniem obciążenia sieciowego az](/cli/azure/network/lb#create). Witaj poniższy przykład tworzy moduł równoważenia obciążenia o nazwie *myLoadBalancer* i przypisuje hello *myPublicIP* konfiguracji IP frontonu toohello adresu:

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a>Utworzyć sondy kondycji
tooallow hello stanu usługi równoważenia obciążenia toomonitor hello aplikacji, możesz użyć sondy kondycji. sondy kondycji Hello dynamicznie dodaje lub usuwa maszyn wirtualnych z obrotu usługi równoważenia obciążenia hello oparte na ich kontroli toohealth odpowiedzi. Domyślnie maszyny Wirtualnej zostanie usunięte z dystrybucji modułu równoważenia obciążenia powitania po dwóch kolejnych błędów na 15 sekund. Można utworzyć sondy kondycji, na podstawie protokołu lub stronę wyboru kondycji określonych aplikacji. 

Witaj poniższy przykład tworzy badanie TCP. Można również utworzyć niestandardowe sond HTTP więcej kontroli kondycji szczegółowe. Podczas korzystania z niestandardowego badanie HTTP, należy utworzyć hello strona sprawdzania kondycji, takich jak *healthcheck.js*. Sonda Hello musi zwracać **HTTP 200 OK** odpowiedzi dla hosta usługi równoważenia obciążenia hello hello tookeep rotacji.

Użyj toocreate sondy kondycji TCP [utworzyć sondy równoważeniem obciążenia sieciowego az](/cli/azure/network/lb/probe#create). Witaj poniższy przykład tworzy badanie kondycji o nazwie *myHealthProbe*:

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a>Tworzenie reguły modułu równoważenia obciążenia
Reguły modułu równoważenia obciążenia jest używany toodefine sposób ruch jest rozproszonej toohello maszyn wirtualnych. Należy zdefiniować hello frontonu konfigurację adresu IP dla ruchu przychodzącego hello i hello zaplecza IP puli tooreceive hello ruchu, wraz z hello wymagane źródłowy i port docelowy. toomake się, że tylko dobrej kondycji maszyn wirtualnych odbieranie ruchu, możesz również definiować toouse sondy kondycji hello.

Tworzenie reguły modułu równoważenia obciążenia z [utworzyć regułę równoważeniem obciążenia sieciowego az](/cli/azure/network/lb/rule#create). Witaj poniższy przykład powoduje utworzenie reguły o nazwie *myLoadBalancerRule*, używa hello *myHealthProbe* badania kondycji i równoważy ruch na porcie *80*:

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a>Konfigurowanie sieci wirtualnej
Przed wdrożeniem niektórych maszyn wirtualnych i przetestować z usługi równoważenia, Utwórz hello obsługi zasobów sieci wirtualnej. Aby uzyskać więcej informacji o sieciach wirtualnych, zobacz hello [Zarządzanie sieciami wirtualnymi Azure](tutorial-virtual-network.md) samouczka.

### <a name="create-network-resources"></a>Utwórz zasoby sieciowe
Tworzenie sieci wirtualnej z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create). Witaj poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* z podsiecią o nazwie *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

tooadd sieciowej grupy zabezpieczeń, użyj [utworzyć nsg sieci az](/cli/azure/network/nsg#create). Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

Tworzenie reguły grupy zabezpieczeń sieci z [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create). Witaj poniższy przykład tworzy regułę grupy zabezpieczeń sieci o nazwie *myNetworkSecurityGroupRule*:

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

Wirtualne karty sieciowe są tworzone za pomocą [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create). Witaj poniższy przykład tworzy trzy wirtualne karty sieciowe. (Jedną wirtualną kartę Sieciową dla każdej maszyny Wirtualnej można utworzyć dla aplikacji w hello następujące kroki). Można tworzyć dodatkowe wirtualne karty sieciowe i maszyn wirtualnych w dowolnym momencie i dodać je toohello usługi równoważenia obciążenia:

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a>Tworzenie maszyn wirtualnych

### <a name="create-cloud-init-config"></a>Tworzenie konfiguracji init chmury
W poprzednim samouczek dotyczący [jak toocustomize maszyny wirtualnej systemu Linux, po pierwszym uruchomieniu komputera](tutorial-automate-vm-deployment.md), możesz przedstawiono sposób dostosowywania maszyny Wirtualnej tooautomate z inicjowaniem chmury. Można użyć tej samej chmurze inicjowania konfiguracji pliku tooinstall NGINX hello i uruchom prostej aplikacji Node.js "Hello World".

W bieżącym powłoki, Utwórz plik o nazwie *init.txt chmury* i Wklej powitania po konfiguracji. Na przykład utworzyć plik hello w hello powłoki chmury nie na komputerze lokalnym. Wprowadź `sensible-editor cloud-init.txt` toocreate hello pliku i wyświetlić listę dostępnych edytory. Upewnij się, że plik całego init chmury hello został poprawnie skopiowany, szczególnie hello pierwszy wiersz:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-virtual-machines"></a>Tworzenie maszyn wirtualnych
tooimprove hello wysoką dostępność aplikacji, umieść maszyn wirtualnych w zestawie dostępności. Aby uzyskać więcej informacji na temat zestawów dostępności, zobacz poprzednie hello [jak maszyn wirtualnych o wysokiej dostępności toocreate](tutorial-availability-sets.md) samouczka.

Utwórz zestaw o dostępności [tworzenia maszyny wirtualnej az zestawu dostępności](/cli/azure/vm/availability-set#create). Witaj poniższy przykład tworzy zbiór nazwanego dostępności *myAvailabilitySet*:

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

Teraz można tworzyć maszyn wirtualnych hello o [tworzenia maszyny wirtualnej az](/cli/azure/vm#create). Witaj poniższy przykład tworzy trzech maszyn wirtualnych i generuje klucze SSH, jeśli jeszcze nie istnieje:

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

Istnieją zadania w tle, które nadal toorun po hello Azure CLI zwraca toohello wiersza. Witaj `--no-wait` parametru nie oczekuje dla wszystkich hello toocomplete zadania. Może to być inny kilka minut, w celu uzyskania dostępu do aplikacji hello. Witaj sondy kondycji modułu równoważenia obciążenia automatycznie wykrywa aplikacji hello jest uruchomiona na każdej maszynie Wirtualnej. Po uruchomieniu aplikacji hello reguły modułu równoważenia obciążenia hello uruchamia toodistribute ruchu.


## <a name="test-load-balancer"></a>Test usługi równoważenia obciążenia
Uzyskaj hello publicznego adresu IP z usługi równoważenia obciążenia z [az sieci ip publicznego Pokaż](/cli/azure/network/public-ip#show). Witaj poniższy przykład uzyskuje hello adres IP dla *myPublicIP* utworzony wcześniej:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

W przeglądarce sieci web tooa można następnie wprowadzić hello publicznego adresu IP. Pamiętaj — zajmuje kilka minut hello hello maszyn wirtualnych toobe gotowe przed toothem ruchu toodistribute rozpoczyna się hello modułu równoważenia obciążenia. Aplikacja Hello jest wyświetlana, łącznie z nazwą hosta hello hello maszyny Wirtualnej tego modułu równoważenia obciążenia hello rozproszonych tooas ruchu w hello poniższy przykład:

![Uruchomionej aplikacji Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

Moduł równoważenia obciążenia hello toosee Dystrybuuj ruch we wszystkich trzech maszyn wirtualnych z tą aplikacją, użytkownik może życie odświeżania przeglądarki sieci web.


## <a name="add-and-remove-vms"></a>Dodawanie i usuwanie maszyny wirtualne
Może być konieczne tooperform konserwacji na powitania maszyn wirtualnych z tą aplikacją, takich jak instalowanie aktualizacji systemu operacyjnego. toodeal z aplikacją tooyour zwiększenie obciążenia, może być konieczne tooadd kolejnych maszyn wirtualnych. W tej sekcji opisano sposób tooremove lub dodać maszyny Wirtualnej z hello modułu równoważenia obciążenia.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Usuń Maszynę wirtualną z hello modułu równoważenia obciążenia
Możesz usunąć Maszynę wirtualną z puli adresów zaplecza hello z [az kart konfiguracji ip puli adresów sieciowych — Usuń](/cli/azure/network/nic/ip-config/address-pool#remove). następujące przykładowe usuwa Hello hello wirtualnej karty Sieciowej dla **myVM2** z *myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

Moduł równoważenia obciążenia hello toosee rozpowszechniają ruchu hello dwóch pozostałych maszyn wirtualnych z tą aplikacją możesz można życie odświeżania przeglądarki sieci web. Teraz można przeprowadzać konserwacji na powitania maszynę Wirtualną, takie jak instalowanie aktualizacji systemu operacyjnego lub wykonywania ponownego uruchomienia maszyny Wirtualnej.

### <a name="add-a-vm-toohello-load-balancer"></a>Dodaj usługi równoważenia obciążenia toohello maszyny Wirtualnej
Po wykonaniu obsługi maszyny Wirtualnej lub tooexpand pojemności, należy dodać pula adresów zaplecza toohello maszyny Wirtualnej z [az kart konfiguracji ip puli adresów sieciowych — Dodaj](/cli/azure/network/nic/ip-config/address-pool#add). Witaj poniższy przykład umożliwia dodanie hello wirtualnej karty Sieciowej dla **myVM2** za*myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a>Następne kroki
W tym samouczku utworzony moduł równoważenia obciążenia i dołączyć tooit maszyn wirtualnych. W tym samouczku omówiono:

> [!div class="checklist"]
> * Tworzenie usługi równoważenia obciążenia Azure
> * Utwórz kondycji sondę modułu równoważenia obciążenia
> * Tworzenie reguły ruchu usługi równoważenia obciążenia
> * Użyj toocreate init chmury podstawowej aplikacji Node.js
> * Tworzenie maszyn wirtualnych i Dołącz tooa modułu równoważenia obciążenia
> * Wyświetl modułu równoważenia obciążenia w akcji
> * Dodawanie i usuwanie maszyny wirtualne z modułem równoważenia obciążenia

Więcej informacji na temat składników sieci wirtualnej platformy Azure poprawić toohello dalej toolearn samouczka.

> [!div class="nextstepaction"]
> [Zarządzanie maszynami wirtualnymi i sieciami wirtualnymi](tutorial-virtual-network.md)
