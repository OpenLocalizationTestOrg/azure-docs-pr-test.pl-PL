---
title: aaaSelect maszyny Wirtualnej systemu Linux obrazy z hello Azure CLI | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello Azure CLI toodetermine hello wydawcy, oferty, jednostki SKU i wersji dla obrazów maszyn wirtualnych w witrynie Marketplace."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7a858e38-4f17-4e8e-a28a-c7f801101721
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/24/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0b115b8654bc156b5bfadba53a6b002a105acb68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a>Jak obrazy toofind maszyny Wirtualnej systemu Linux w programie hello Azure Marketplace z hello wiersza polecenia platformy Azure
W tym temacie opisano, jak toouse hello Azure CLI 2.0 obrazów maszyn wirtualnych toofind w hello Azure Marketplace. Użyj tej informacji toospecify obrazu z witryny Marketplace, tworząc Maszynę wirtualną systemu Linux.

Upewnij się, że zainstalowane w najnowszej hello [Azure CLI 2.0](/cli/azure/install-az-cli2) i są rejestrowane w tooan konto platformy Azure (`az login`).

## <a name="terminology"></a>Terminologia

Obrazy Marketplace są identyfikowane w hello interfejsu wiersza polecenia i innych narzędzi platformy Azure, zgodnie z tooa hierarchii:

* **Wydawca** — Witaj organizacji, który utworzył obraz powitania. Przykład: kanoniczny
* **Oferują** -grupa powiązanych obrazy utworzone przez wydawcę. Przykład: Ubuntu Server
* **Jednostka SKU** — wystąpienie oferty, takie jak wydaniem dystrybucji. Przykład: 16.04-LTS
* **Wersja** — Witaj numer wersji jednostki SKU obrazu. Podczas określania obrazu hello, numer wersji hello z można zastąpić "najnowszej", który wybiera hello najnowszą wersję dystrybucji hello.

toospecify obrazu z witryny Marketplace, używane zwykle obraz powitania *URN*. te wartości, rozdzielone znakiem dwukropka (:) hello łączy Hello URN: *wydawcy*:*oferują*:*Sku*:*wersji*. 


## <a name="list-popular-images"></a>Listy obrazów popularnych

Uruchom hello [listy obrazów maszyny wirtualnej az](/cli/azure/vm/image#list) polecenia bez hello `--all` opcji, toosee obrazy listę popularnych maszyny Wirtualnej w programie hello Azure Marketplace. Na przykład uruchom następujące polecenie toodisplay hello buforowaną listę popularnych obrazów w formacie tabeli:

```azurecli
az vm image list --output table
```

Hello dane wyjściowe zawierają hello URN (hello wartość hello *Urn* kolumny), który możesz użyć obrazu hello toospecify. Podczas tworzenia maszyny Wirtualnej przy użyciu jednej z tych popularnych obrazów Marketplace, można alternatywnie określić hello URN aliasu, takich jak *UbuntuLTS*.

```
You are viewing an offline list of images, use --all tooretrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
...
```

## <a name="find-specific-images"></a>Znajdowanie określonych obrazów

toofind określonego obrazu maszyny Wirtualnej w hello Marketplace, użyj hello `az vm image list` z hello `--all` opcji. Ta wersja polecenia hello przyjmuje niektórych toocomplete czasu i może zwrócić długich danych wyjściowych, co zwykle filtrowanie listy hello `--publisher` lub inny parametr. 

Na przykład następujące polecenie hello Wyświetla wszystkie oferty Debian (należy pamiętać, że bez hello `--all` przełącznika, tylko wyszukuje hello lokalnej pamięci podręcznej obrazów wspólnej):

```azurecli
az vm image list --offer Debian --all --output table 

```

Częściowe dane wyjściowe: 
```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  --------------
Debian   credativ     7                  credativ:Debian:7:7.0.201602010                  7.0.201602010
Debian   credativ     7                  credativ:Debian:7:7.0.201603020                  7.0.201603020
Debian   credativ     7                  credativ:Debian:7:7.0.201604050                  7.0.201604050
Debian   credativ     7                  credativ:Debian:7:7.0.201604200                  7.0.201604200
Debian   credativ     7                  credativ:Debian:7:7.0.201606280                  7.0.201606280
Debian   credativ     7                  credativ:Debian:7:7.0.201609120                  7.0.201609120
Debian   credativ     7                  credativ:Debian:7:7.0.201611020                  7.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
Debian   credativ     8                  credativ:Debian:8:8.0.201708040                  8.0.201708040
...
```

Stosowanie filtrów podobne z hello `--location`, `--publisher`, i `--sku` opcje. Wyniki pasujące częściowo można wykonywać nawet w filtrze, takie jak wyszukiwanie `--offer Deb` toofind wszystkie obrazy Debian.

Jeśli nie określisz określonej lokalizacji z hello `--location` opcji wartości hello `westus` zwracane są domyślnie. (Ustaw domyślną inną lokalizację, uruchamiając `az configure --defaults location=<location>`.)

Na przykład hello następujące polecenie wyświetla listę wszystkich Debian SKU 8 w `westeurope`:

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

Częściowe dane wyjściowe:

```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  -------------
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
...
```

## <a name="navigate-hello-images"></a>Przejdź hello obrazów 
Inny sposób toofind obrazu w lokalizacji jest toorun hello [obrazu maszyny wirtualnej az listy wydawców](/cli/azure/vm/image#list-publishers), [obrazu maszyny wirtualnej az listy oferty](/cli/azure/vm/image#list-offers), i [obrazu maszyny wirtualnej az listy SKU](/cli/azure/vm/image#list-skus) polecenia w sekwencji. Przy użyciu następujących poleceń można określić te wartości:

1. Lista wydawców obraz powitania.
2. Dla danego wydawcy wyświetl listę ofert.
3. Dla danej oferty wyświetl listę wersji SKU.


Na przykład hello następujące polecenie wyświetla listę wydawców obraz powitania w hello lokalizacji zachodnie stany USA:

```azurecli
az vm image list-publishers --location westus --output table
```

Częściowe dane wyjściowe:

```
Location    Name
----------  ----------------------------------------------------
westus      1e
westus      4psa
westus      7isolutions
westus      a10networks
westus      abiquo
westus      accellion
westus      Acronis
westus      Acronis.Backup
westus      actian_matrix
westus      actifio
westus      activeeon
westus      adatao
...
```
Użyj tego toofind informacji oferuje od określonego wydawcy. Na przykład jeśli Canonical wydawcy obrazu w hello lokalizacji zachodnie stany USA, Znajdź ofert uruchamiając `azure vm image list-offers`. Przekaż hello lokalizacji i wydawcy hello jak hello poniższy przykład:

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

Dane wyjściowe:

```
Location    Name
----------  -------------------------
westus      Ubuntu15.04Snappy
westus      Ubuntu15.04SnappyDocker
westus      UbunturollingSnappy
westus      UbuntuServer
westus      Ubuntu_Core
westus      Ubuntu_Snappy_Core
westus      Ubuntu_Snappy_Core_Docker
```
Zostanie wyświetlony w hello regionu zachodnie stany USA, Canonical publikuje hello **UbuntuServer** oferują na platformie Azure. Jakie wersje produktu, ale? Uruchom te wartości tooget `azure vm image list-skus` i Ustaw lokalizację hello, wydawcy i oferty, które zostały odnalezione:

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

Dane wyjściowe:

```
Location    Name
----------  -----------------
westus      12.04.3-LTS
westus      12.04.4-LTS
westus      12.04.5-DAILY-LTS
westus      12.04.5-LTS
westus      12.10
westus      14.04.0-LTS
westus      14.04.1-LTS
westus      14.04.2-LTS
westus      14.04.3-LTS
westus      14.04.4-LTS
westus      14.04.5-DAILY-LTS
westus      14.04.5-LTS
westus      16.04-beta
westus      16.04-DAILY-LTS
westus      16.04-LTS
westus      16.04.0-LTS
westus      16.10
westus      16.10-DAILY
westus      17.04
westus      17.04-DAILY
westus      17.10-DAILY
```

Na koniec użyj hello `az vm image list` toofind polecenia określonej wersji hello wersję produktu, na przykład **16.04 LTS**:

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

Dane wyjściowe:

```
Offer         Publisher    Sku        Urn                                               Version
------------  -----------  ---------  ------------------------------------------------  ---------------
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611220  16.04.201611220
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611300  16.04.201611300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612050  16.04.201612050
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612140  16.04.201612140
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612210  16.04.201612210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201701130  16.04.201701130
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702020  16.04.201702020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702200  16.04.201702200
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702210  16.04.201702210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702240  16.04.201702240
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703020  16.04.201703020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703030  16.04.201703030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703070  16.04.201703070
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703270  16.04.201703270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703280  16.04.201703280
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703300  16.04.201703300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705080  16.04.201705080
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705160  16.04.201705160
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706100  16.04.201706100
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706191  16.04.201706191
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707210  16.04.201707210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707270  16.04.201707270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708030  16.04.201708030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708110  16.04.201708110
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708151  16.04.201708151
```
## <a name="next-steps"></a>Następne kroki
Teraz można wybrać dokładnie hello obraz ma toouse przez biorąc pod uwagę hello URN wartość. Przekaż tę wartość z hello `--image` parametru podczas tworzenia maszyny Wirtualnej z hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia. Należy pamiętać, że można opcjonalnie zastąpić numeru wersji hello hello URN "najnowszej". Ta wersja jest zawsze hello najnowszą wersję hello dystrybucji. toocreate maszynę wirtualną, szybko, używając hello URN informacji, zobacz [tworzenie i zarządzanie maszyn wirtualnych systemu Linux z hello Azure CLI](tutorial-manage-vm.md).
