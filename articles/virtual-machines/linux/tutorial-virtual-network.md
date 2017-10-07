---
title: aaaAzure sieci wirtualnych i maszyn wirtualnych systemu Linux | Dokumentacja firmy Microsoft
description: "Samouczek — Zarządzanie sieciami wirtualnymi Azure i maszyn wirtualnych systemu Linux z hello Azure CLI"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a>Zarządzanie sieciami wirtualnymi Azure i maszyn wirtualnych systemu Linux z hello Azure CLI

Maszyny wirtualne platformy Azure używania sieci platformy Azure do komunikacji sieciowej wewnętrznych i zewnętrznych. Ten samouczek przeprowadzi Cię przez wdrożenie dwóch maszyn wirtualnych i konfigurowanie sieci platformy Azure dla tych maszyn wirtualnych. Przykłady Hello w tym samouczku założono hello maszyny wirtualne obsługujące aplikacji sieci web z bazy danych zaplecza, jednak aplikacja nie zostanie wdrożona w samouczku hello. Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Wdrażanie sieci wirtualnej
> * Utwórz podsieć sieci wirtualnej
> * Dołącz podsieci tooa maszyny wirtualne
> * Zarządzanie publicznych adresów IP maszyny wirtualnej
> * Bezpieczny ruch przychodzący z Internetu
> * Bezpieczny ruch tooVM maszyny Wirtualnej


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="vm-networking-overview"></a>Omówienie sieci maszyny Wirtualnej

Sieci wirtualnych platformy Azure włączyć bezpiecznych połączeń sieci między maszynami wirtualnymi, hello internet i innymi usługami Azure, takich jak bazy danych Azure SQL. Sieci wirtualne są podzielone na segmentach logicznej podsieci. Podsieci są używane toocontrol przepływ sieci i funkcję granicy zabezpieczeń. Podczas wdrażania maszyny Wirtualnej, zwykle obejmuje interfejs sieci wirtualnej, która jest dołączona tooa podsieci.

## <a name="deploy-virtual-network"></a>Wdrażanie sieci wirtualnej

W tym samouczku jednej sieci wirtualnej jest tworzony z dwoma podsieciami. Podsieci frontonu do obsługi aplikacji sieci web, a podsieć zaplecza dla hostingu serwera bazy danych.

Przed utworzeniem sieci wirtualnej, Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myRGNetwork* w lokalizacji eastus hello.

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a>Tworzenie sieci wirtualnej

Witaj nam [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create) toocreate polecenia sieci wirtualnej. W tym przykładzie nosi nazwę sieci hello *mvVnet* i podano prefiksu adresu *10.0.0.0/16*. Tworzona jest również podsieć o nazwie *mySubnetFrontEnd* i prefiksem *10.0.1.0/24*. W dalszej części tego samouczka frontonu maszyny Wirtualnej jest połączonych toothis podsieci. 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a>Utwórz podsieć

Nowa podsieć jest dodawany toohello sieci wirtualnej przy użyciu hello [Utwórz podsieć sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#create) polecenia. W tym przykładzie hello podsieci o nazwie *mySubnetBackEnd* i podano prefiksu adresu *10.0.2.0/24*. Ta podsieć jest używany ze wszystkimi usługami zaplecza.

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

W tym momencie sieci zostało utworzone i podzielone na dwie podsieci, jeden dla usługi frontonu i drugi dla usług zaplecza. W następnej sekcji hello maszyny wirtualne są tworzone i połączone toothese podsieci.

## <a name="understand-public-ip-address"></a>Zrozumienie publicznego adresu IP

Publiczny adres IP umożliwia toobe zasobów platformy Azure dostępna w hello internet. W tej sekcji samouczka hello maszyny Wirtualnej jest tworzony toodemonstrate jak adresy toowork z publicznym adresem IP.

### <a name="allocation-method"></a>Metoda alokacji

Publiczny adres IP można przypisać jako dynamicznej lub statycznej. Domyślnie dynamicznie przydzielane publicznego adresu IP. Dynamiczne adresy IP są wydawane po cofnięciu przydziału maszyny Wirtualnej. To działanie powoduje toochange adres IP hello podczas żadnej operacji, która obejmuje dezalokacji maszyny Wirtualnej.

Metoda alokacji Hello można ustawić toostatic, który zapewnia pozostawienie hello adres IP przypisany tooa maszyny Wirtualnej, nawet podczas deallocated stanu. Korzystając z statycznie przydzielony adres IP, nie można określić sam adres IP hello. Zamiast tego jest ona przydzielone z puli dostępnych adresów.

### <a name="dynamic-allocation"></a>Dynamiczna alokacja

Podczas tworzenia maszyny Wirtualnej przy użyciu hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia hello domyślnego publicznego metoda adresu IP alokacji jest dynamiczny. W hello poniższy przykład maszyna wirtualna zostanie utworzona z dynamicznego adresu IP. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a>Statycznych alokacji

Podczas tworzenia maszyny wirtualnej z wykorzystaniem hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia, obejmują hello `--public-ip-address-allocation static` tooassign argumentu statycznego publicznego adresu IP. Ta operacja nie jest prezentowana w tym samouczku, jednak w następnej sekcji hello dynamicznie przydzielonego adresu IP jest zmienione tooa statycznie przydzielony adres. 

### <a name="change-allocation-method"></a>Zmień metodę alokacji

Metoda alokacji adresu IP Hello można zmienić za pomocą hello [az sieci ip publicznego aktualizacji](/cli/azure/network/public-ip#update) polecenia. W tym przykładzie hello metoda alokacji adresów IP hello frontonu maszyny Wirtualnej zostanie zmieniona toostatic.

Najpierw cofnąć hello maszyny Wirtualnej.

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

Użyj hello [az sieci ip publicznego aktualizacji](/cli/azure/network/public-ip#update) metodę alokacji hello tooupdate polecenia. W takim przypadku hello `--allocation-method` jest ustawiany za*statycznych*.

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

Uruchom hello maszyny Wirtualnej.

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a>Nie publicznego adresu IP

Często maszyny Wirtualnej nie jest konieczne toobe dostępna przez hello internet. toocreate Maszynę wirtualną bez publicznego adresu IP, użyj hello `--public-ip-address ""` argumentu z pustego zestawu cudzysłowów. Ta konfiguracja jest przedstawiona w dalszej części tego samouczka

## <a name="secure-network-traffic"></a>Zabezpieczanie ruchu sieciowego

Grupa zabezpieczeń sieci (NSG) zawiera listę reguł zabezpieczeń, które Zezwalaj lub Odmów tooresources ruchu sieciowego połączone sieci wirtualne tooAzure (VNet). Grupy NSG mogą być skojarzone toosubnets lub do interfejsów sieciowych poszczególnych. Grupa NSG jest skojarzona z karty sieciowej, stosuje się tylko hello skojarzonego VM. Gdy grupa NSG jest skojarzona tooa podsieci, mają zastosowanie reguły hello tooall zasobów połączonych toohello podsieci. 

### <a name="network-security-group-rules"></a>Reguły grupy zabezpieczeń sieci

Reguły NSG definiują portów sieciowych za pośrednictwem których ruch jest dozwolony lub niedozwolony. reguły Hello mogą obejmować źródłowe i docelowe zakresów adresów IP tak, aby ruch jest kontrolowany między konkretnych systemów lub podsieci. Reguły NSG obejmują także priorytet (od 1 — i 4096). Reguły są sprawdzane hello według priorytetu. Reguła o priorytecie 100 jest oceniane przed regułą z priorytetem 200.

Wszystkie sieciowe grupy zabezpieczeń zawierają zestaw reguł domyślnych. Nie można usunąć reguły domyślne Hello, ale ponieważ mają przypisany najniższy priorytet hello, mogą być zastąpione przez hello utworzonych reguł.

- **Sieć wirtualna** — ruch pochodzący i kończenie w sieci wirtualnej jest dozwolony zarówno w kierunkach przychodzących i wychodzących.
- **Internet** — ruch wychodzący jest dozwolone, ale ruch przychodzący jest zablokowany.
- **Moduł równoważenia obciążenia** — Zezwalaj Azure kondycji hello tooprobe usługi równoważenia obciążenia maszyn wirtualnych i wystąpień ról. Tę zasadę można zastąpić, jeśli nie używasz zestawu o zrównoważonym obciążeniu.

### <a name="create-network-security-groups"></a>Utwórz grupy zabezpieczeń sieci

Grupy zabezpieczeń sieci można tworzyć na powitania sam czasu jako Maszynę wirtualną przy użyciu hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia. W takiej hello grupa NSG jest skojarzona z interfejsu sieciowego maszyn wirtualnych hello i reguły NSG jest automatycznie utworzona tooallow ruch na porcie *22* z dowolnego źródła. Wcześniej w tym samouczku powitalne frontonu NSG został utworzony automatycznie z hello frontonu maszyny Wirtualnej. Reguły NSG również został automatycznie utworzony dla portu 22. 

W niektórych przypadkach może być przydatne toopre — Utwórz grupy NSG, takie jak kiedy nie należy tworzyć reguły domyślne SSH lub gdy hello NSG powinna być dołączone tooa podsieci. 

Użyj hello [utworzyć nsg sieci az](/cli/azure/network/nsg#create) toocreate polecenia sieciowej grupy zabezpieczeń.

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

Zamiast skojarzenie interfejsu sieciowego tooa NSG hello, jest skojarzona z podsiecią. W tej konfiguracji żadnej maszyny Wirtualnej, która jest dołączona toohello podsieci dziedziczy hello reguły NSG.

Aktualizuj istniejącą podsieć hello o nazwie *mySubnetBackEnd* z hello Nowa grupa NSG.

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

Teraz Utwórz maszynę wirtualną, która jest dołączona toohello *mySubnetBackEnd*. Zwróć uwagę, że hello `--nsg` argument ma wartość pustą cudzysłowów. Grupy NSG toobe utworzone za pomocą hello maszyny Wirtualnej nie jest konieczne. Hello maszyny Wirtualnej jest dołączone toohello zaplecza podsieci, które są chronione za pomocą hello wstępnie utworzone NSG zaplecza. Ta grupa NSG stosowana toohello maszyny Wirtualnej. Ponadto Zauważ, że hello `--public-ip-address` argument ma wartość pustą cudzysłowów. Ta konfiguracja tworzy Maszynę wirtualną bez publicznego adresu IP. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a>Bezpieczny ruch przychodzący

Gdy hello frontonu maszyna wirtualna została utworzona, NSG utworzono regułę ruchu przychodzącego tooallow port 22. Ta zasada umożliwia toohello połączenia SSH maszyny Wirtualnej. Na przykład ruch powinno być dozwolone na porcie *80*. Ta konfiguracja pozwala toobe aplikacji sieci web, dostępny na powitania maszyny Wirtualnej.

Użyj hello [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) toocreate polecenia reguły portu *80*.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

Witaj frontonu maszyny Wirtualnej jest obecnie dostępny tylko na porcie *22* i port *80*. Cały ruch przychodzący jest zablokowany na powitania sieciowej grupy zabezpieczeń. Może to być przydatne toovisualize hello NSG reguły konfiguracji. Konfiguracja reguły NSG hello zwracany z hello [listy reguł sieciowej az](/cli/azure/network/nsg/rule#list) polecenia. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

Dane wyjściowe:

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a>Bezpieczny ruch tooVM maszyny Wirtualnej

Reguły grupy zabezpieczeń sieci można także zastosować między maszynami wirtualnymi. Na przykład hello frontonu maszyny Wirtualnej musi toocommunicate z hello wirtualna zaplecza na porcie *22* i *3306*. Taka konfiguracja pozwala połączeń SSH z hello frontonu maszyny Wirtualnej, a także zezwolić aplikacji na powitania frontonu toocommunicate maszyny Wirtualnej z wewnętrznej bazy danych MySQL. Powinien zostać zablokowany cały ruch między maszynami wirtualnymi hello frontonu i zaplecza.

Użyj hello [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) toocreate polecenia regułę port 22. Zwróć uwagę, że hello `--source-address-prefix` argument określa wartość *10.0.1.0/24*. Taka konfiguracja powoduje, że tylko na ruch z podsieci frontonu hello jest dozwolone przez hello NSG.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

Teraz Dodaj regułę dla ruchu danych MySQL na porcie 3306.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

Na koniec, ponieważ stosowanie reguły domyślnej grupy NSG cały ruch między maszynami wirtualnymi w hello sam sieci wirtualnej, regułę można utworzyć hello zaplecza grup NSG tooblock cały ruch. Zauważ, że hello `--priority` znajduje się wartość *300*, która jest niższe, że oba hello reguły NSG i MySQL. Taka konfiguracja powoduje, że ruchu SSH i MySQL nadal uzyskuje zezwolenie za pośrednictwem hello NSG.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

Witaj zaplecza maszyna wirtualna jest teraz dostępny tylko na porcie *22* i port *3306* z podsieci frontonu hello. Cały ruch przychodzący jest zablokowany na powitania sieciowej grupy zabezpieczeń. Może to być przydatne toovisualize hello NSG reguły konfiguracji. Konfiguracja reguły NSG hello zwracany z hello [listy reguł sieciowej az](/cli/azure/network/nsg/rule#list) polecenia. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

Dane wyjściowe:

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a>Następne kroki

W tym samouczku zostało utworzone i zabezpieczonej sieci platformy Azure jako powiązane toovirtual maszyny. W tym samouczku omówiono:

> [!div class="checklist"]
> * Wdrażanie sieci wirtualnej
> * Utwórz podsieć sieci wirtualnej
> * Dołącz podsieci tooa maszyny wirtualne
> * Zarządzanie publicznych adresów IP maszyny wirtualnej
> * Bezpieczny ruch przychodzący z Internetu
> * Bezpieczny ruch tooVM maszyny Wirtualnej

Przejdź dalej toolearn samouczka toohello Zabezpieczanie danych w przypadku maszyn wirtualnych przy użyciu kopii zapasowej systemu Azure. 

> [!div class="nextstepaction"]
> [Tworzenie kopii zapasowych maszyn wirtualnych systemu Linux na platformie Azure](./tutorial-backup-vms.md)
