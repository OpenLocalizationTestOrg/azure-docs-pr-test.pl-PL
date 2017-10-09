---
title: aaaCreate zestawy skalowania maszyny wirtualnej dla systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Tworzenie i wdrażanie aplikacji wysokiej dostępności na maszynach wirtualnych systemu Linux przy użyciu zestawu skali maszyny wirtualnej"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a>Tworzenie zestawu skali maszyny wirtualnej i wdrażanie aplikacji wysokiej dostępności w systemie Linux
Zestaw skali maszyny wirtualnej umożliwia toodeploy i zarządzać zestawem identyczne, automatyczne skalowanie maszyn wirtualnych. Można ręcznie skalować hello liczbę maszyn wirtualnych w zestawie skalowania hello lub zdefiniuj tooautoscale reguły na podstawie użycia procesora CPU, pamięci żądanie lub ruchu sieciowego. W tym samouczku możesz wdrożyć skali maszyny wirtualnej w usłudze Azure. Omawiane kwestie:

> [!div class="checklist"]
> * Użyj toocreate init chmury tooscale aplikacji
> * Utwórz zestaw skali maszyny wirtualnej
> * Zwiększanie lub zmniejszanie hello liczbę wystąpień w zestawie skalowania
> * Wyświetl informacje o połączeniu dla wystąpień zestawu skali
> * Dysków danych w zestawie skalowania


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="scale-set-overview"></a>Omówienie zestawu skali
Zestaw skali maszyny wirtualnej umożliwia toodeploy i zarządzać zestawem identyczne, automatyczne skalowanie maszyn wirtualnych. Skali ustawia hello Użyj tego samego składniki jako poznanie w samouczku poprzedniej hello zbyt[tworzyć maszyny wirtualne o wysokiej dostępności](tutorial-availability-sets.md). Maszyny wirtualne w zestawie skalowania są tworzone w dostępności ustaw i rozpowszechniane w domenach awarii i aktualizacji logiki.

Maszyny wirtualne są tworzone zgodnie z potrzebami w zestawie skalowania. Zdefiniuj toocontrol reguł skalowania automatycznego, kiedy maszyny wirtualne są dodawane lub usuwane z hello zestaw skali. Te reguły może wyzwolić na podstawie metryk, takich jak obciążenie procesora CPU, pamięć lub ruchu sieciowego.

Obsługa się too1, 000 maszyn wirtualnych, gdy używasz obrazu platformy Azure zestawach skali. W przypadku obciążeń produkcyjnych, warto zapoznać się z zbyt[utworzyć niestandardowy obraz maszyny Wirtualnej](tutorial-custom-images.md). Możesz utworzyć zapasowych maszyn wirtualnych too100 w skali ustawić przy użyciu obrazu niestandardowego.


## <a name="create-an-app-tooscale"></a>Utwórz tooscale aplikacji
W środowisku produkcyjnym, możesz za[utworzyć niestandardowy obraz maszyny Wirtualnej](tutorial-custom-images.md) zawierającą aplikacji zainstalowane i skonfigurowane. W tym samouczku umożliwia dostosowywanie hello maszyn wirtualnych na pierwszym tooquickly rozruchu zobacz zestaw akcji skalowania.

W poprzednich samouczka przedstawiono [jak toocustomize maszyny wirtualnej systemu Linux, po pierwszym uruchomieniu komputera](tutorial-automate-vm-deployment.md) z inicjowaniem chmury. Można użyć tej samej chmurze inicjowania konfiguracji pliku tooinstall NGINX hello i uruchom prostej aplikacji Node.js "Hello World". 

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


## <a name="create-a-scale-set"></a>Utwórz zestaw skali
Przed utworzeniem zestaw skali, Utwórz grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupScaleSet* w hello *eastus* lokalizacji:

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

Teraz Utwórz zestaw o skali maszyny wirtualnej [az vmss utworzyć](/cli/azure/vmss#create). Witaj poniższy przykład tworzy zestaw o nazwie skalowania *myScaleSet*, używa hello init chmury pliku toocustomize hello maszyny Wirtualnej i generuje klucze SSH, jeśli nie istnieją:

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

Go zajmuje kilka minut toocreate i skonfiguruje wszystkie zasoby zestaw skalowania hello maszyn wirtualnych. Istnieją zadania w tle, które nadal toorun po hello Azure CLI zwraca toohello wiersza. Może to być inny kilka minut, w celu uzyskania dostępu do aplikacji hello.


## <a name="allow-web-traffic"></a>Zezwalaj na ruch w sieci web
Moduł równoważenia obciążenia został utworzony automatycznie jako część zestawu skali maszyny wirtualnej hello. Moduł równoważenia obciążenia Hello dystrybuuje ruch zestawu zdefiniowanego maszyn wirtualnych przy użyciu reguły modułu równoważenia obciążenia. Dowiedz się więcej o pojęcia dotyczące usługi równoważenia obciążenia i konfiguracji w następnym samouczku hello [jak tooload złoty środek między maszynami wirtualnymi na platformie Azure](tutorial-load-balancer.md).

Aplikacja sieci web tooallow ruchu tooreach hello, tworzenia reguły za pomocą [utworzyć regułę równoważeniem obciążenia sieciowego az](/cli/azure/network/lb/rule#create). Witaj poniższy przykład powoduje utworzenie reguły o nazwie *myLoadBalancerRuleWeb*:

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a>Testowanie aplikacji
toosee aplikacji Node.js w sieci web hello uzyskać hello publicznego adresu IP z usługi równoważenia obciążenia z [az sieci ip publicznego Pokaż](/cli/azure/network/public-ip#show). Witaj poniższy przykład uzyskuje hello adres IP dla *myScaleSetLBPublicIP* utworzone jako część zestawu skalowania hello:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

Wprowadź hello publicznego adresu IP w przeglądarce sieci web tooa. Aplikacja Hello jest wyświetlana, łącznie z nazwą hosta hello hello hello tej maszyny Wirtualnej obciążenia ruchu równoważenia dystrybuowane do:

![Uruchomionej aplikacji Node.js](./media/tutorial-create-vmss/running-nodejs-app.png)

zestaw w akcji skalowania hello toosee, możesz można życie odświeżania obciążenia hello toosee przeglądarki sieci web równoważenia rozpowszechniają wszystkich aplikacji uruchomionych maszyn wirtualnych hello ruchu.


## <a name="management-tasks"></a>Zadania zarządzania
W całym cyklu życia hello zestawu skali hello, może być konieczne toorun jednego lub więcej zadań zarządzania. Ponadto można toocreate skrypty, które automatyzacji różnych zadań cyklu życia. Hello Azure CLI 2.0 zapewnia toodo szybko tych zadań. Poniżej przedstawiono kilka typowych zadań.

### <a name="view-vms-in-a-scale-set"></a>Maszyny wirtualne widoku w zestawie skalowania
Ustaw listę maszyn wirtualnych uruchomionych w skali sieci tooview, użyj [wystąpienia listy az vmss](/cli/azure/vmss#list-instances) w następujący sposób:

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a>Zwiększanie lub zmniejszanie wystąpień maszyn wirtualnych
toosee hello liczbę wystąpień obecnie w skali ustawiono, użyj [Pokaż vmss az](/cli/azure/vmss#show) i wykonywać zapytania na *sku.capacity*:

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

Możesz ręcznie zwiększyć lub zmniejszyć liczbę hello maszyn wirtualnych w skali hello ustawiony za pomocą [skali vmss az](/cli/azure/vmss#scale). Witaj poniższy przykład przedstawia hello liczbę maszyn wirtualnych w sieci za zestaw skalowania*5*:

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

Reguły automatycznego skalowania umożliwiają definiowanie konfiguracji tooscale w górę lub w dół hello liczbę maszyn wirtualnych w skali sieci toodemand odpowiedzi, takie jak ruch w sieci i użycie procesora CPU. Obecnie te zasady nie można ustawić w 2.0 interfejsu wiersza polecenia platformy Azure. Użyj hello [portalu Azure](https://portal.azure.com) tooconfigure automatycznego skalowania.

### <a name="get-connection-info"></a>Pobierz informacje o połączeniu
informacje o połączeniu tooobtain około hello w Twojej zestawy skalowania maszyn wirtualnych, użyj [az vmss listy--połączenia — informacje o wystąpieniu](/cli/azure/vmss#list-instance-connection-info). To polecenie wyświetla hello publicznego adresu IP i portu dla każdej maszyny Wirtualnej, która pozwala tooconnect przy użyciu protokołu SSH:

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a>Dyski danych za pomocą zestawów skali
Można tworzyć i dysków z danymi za pomocą zestawów skali. W poprzednich samouczek przedstawiono sposób zbyt[dysków Azure zarządzanie](tutorial-manage-disks.md) najlepszych rozwiązań i ulepszenia wydajności umożliwiające tworzenie aplikacji na dysków z danymi, a nie na dysku systemu operacyjnego hello tekst hello opisanych.

### <a name="create-scale-set-with-data-disks"></a>Utwórz zestaw skali z dysków z danymi
toocreate skali ustawić i dołączyć dysków z danymi, Dodaj hello `--data-disk-sizes-gb` toohello parametru [az vmss utworzyć](/cli/azure/vmss#create) polecenia. Witaj poniższy przykład tworzy zestaw o skali *50*wystąpienia tooeach dołączone dyski danych Gb:

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

Usunięcie wystąpienia z zestawu skalowania żadnych dysków dołączonych danych są również usuwane.

### <a name="add-data-disks"></a>Dodawanie dysków z danymi
Ustaw tooinstances dysku danych, w Twojej skali tooadd, użyj [dołączyć dysku vmss az](/cli/azure/vmss/disk#attach). Witaj poniższy przykład umożliwia dodanie *50*wystąpienia tooeach dysku Gb:

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a>Odłączanie dysku z danymi
Ustaw tooinstances dysku danych, w Twojej skali tooremove, użyj [odłączyć dysku vmss az](/cli/azure/vmss/disk#detach). Witaj poniższy przykład umożliwia usunięcie hello dysk z danymi o numerze LUN *2* z każde wystąpienie:

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a>Następne kroki
W tym samouczku utworzony zestaw skali maszyny wirtualnej. W tym samouczku omówiono:

> [!div class="checklist"]
> * Użyj toocreate init chmury tooscale aplikacji
> * Utwórz zestaw skali maszyny wirtualnej
> * Zwiększanie lub zmniejszanie hello liczbę wystąpień w zestawie skalowania
> * Wyświetl informacje o połączeniu dla wystąpień zestawu skali
> * Dysków danych w zestawie skalowania

Więcej informacji na temat pojęć dla maszyn wirtualnych równoważenia obciążenia poprawić toohello dalej toolearn samouczka.

> [!div class="nextstepaction"]
> [Równoważyć obciążenie maszyn wirtualnych](tutorial-load-balancer.md)