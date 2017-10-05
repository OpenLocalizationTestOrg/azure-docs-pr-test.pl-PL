---
title: "Samouczek zestawy dostępności dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Informacje na temat zestawów dostępności dla maszyn wirtualnych systemu Linux na platformie Azure."
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 63fe3f165864f06228604cac56d06cc061ab25f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-availability-sets"></a>Jak używać zestawów dostępności


Z tego samouczka dowiesz się, jak zwiększyć dostępność i niezawodność rozwiązań maszyny wirtualnej na platformie Azure przy użyciu funkcji o nazwie zestawów dostępności. Zestawy dostępności upewnij się, czy maszyn wirtualnych, należy wdrożyć na platformie Azure są rozproszone na wielu klastrów izolowanego sprzętu. W ten sposób zapewnia, że jeśli awarii sprzętu lub oprogramowania w systemie Azure wykonywany, jest ograniczona tylko do podzbioru maszyny wirtualne i które rozwiązania ogólną pozostanie dostępny i działa z perspektywy klientów przy użyciu go.

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie zestawu dostępności
> * Tworzenie maszyny Wirtualnej w zestawie dostępności
> * Sprawdź dostępne rozmiary maszyny Wirtualnej


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierzesz do zainstalowania i używania interfejsu wiersza polecenia lokalnie, w tym samouczku wymaga używasz interfejsu wiersza polecenia Azure w wersji 2.0.4 lub nowszej. Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana. Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="availability-set-overview"></a>Omówienie zestawu dostępności

Zestawu dostępności jest możliwość grupę logiczną, która na platformie Azure umożliwia Sprawdź, czy zasobów maszyny Wirtualnej, który można umieścić w nim są odizolowane od siebie, gdy są wdrożone w centrum danych Azure. Azure zapewnia, że maszyny wirtualne, umieść w ramach zestawu dostępności uruchamiania na wielu serwerach fizycznych, obliczeniowe stojakami jednostek magazynowych i przełączniki sieciowe. Dzięki temu w przypadku awarii sprzętu lub oprogramowania Azure awarii, jest ograniczona tylko podzestaw maszyn wirtualnych, a aplikacja ogólna pozostanie w górę i nadal dostępne dla klientów. Przy użyciu zestawów dostępności jest podstawowych możliwości wykorzystać umożliwia tworzenia rozwiązań chmur wiarygodne.

Zastanówmy typowe rozwiązania oparte na Maszynach którym może mieć 4 serwery frontonu sieci web i korzystać z 2 maszyny wirtualne zaplecza, które hostują bazy danych. Przy użyciu platformy Azure, należy zdefiniować dwa zestawy dostępności, przed wdrożeniem maszyn wirtualnych: jeden zbiór dostępności dla warstwy "web" i jeden zbiór dostępności dla warstwy "baza danych". Podczas tworzenia nowej maszyny Wirtualnej można określić zestaw dostępności jako parametr do maszyny wirtualnej az utworzyć polecenie, a Azure zostanie automatycznie upewnij się, że maszyny wirtualne utworzone w zestawie dostępne są izolowane między wieloma zasobami sprzętu fizycznego. Oznacza to, że jeśli sprzęt fizyczny wykorzystywany do jednego serwera sieci Web lub maszyn wirtualnych z serwera bazy danych jest uruchomiona na ma problem, wiesz, że inne wystąpienia serwera sieci Web i bazy danych w maszynach wirtualnych pozostaną uruchomione prawidłowo ponieważ są one na inny komputer.

Zawsze należy używać zestawów dostępności, jeśli chcesz wdrożyć niezawodne rozwiązania na podstawie maszyny Wirtualnej w systemie Azure.


## <a name="create-an-availability-set"></a>Tworzenie zestawu dostępności

Możesz utworzyć zestaw przy użyciu danych o dostępności [tworzenia maszyny wirtualnej az zestawu dostępności](/cli/azure/vm/availability-set#create). W tym przykładzie umieszczania liczba domen aktualizacji i odporność na *2* dla zestawu o nazwie dostępności *myAvailabilitySet* w *myResourceGroupAvailability* grupy zasobów.

Utwórz grupę zasobów.

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

Zestawy dostępności umożliwiają izolować zasobów między "domen błędów" i "Aktualizuj domeny". A **domeny błędów** reprezentuje kolekcję izolowanego server + sieć i Magazyn zasobów. W powyższym przykładzie mamy wskazać, że firma Microsoft ma naszych dostępności ustawioną być rozproszone na co najmniej dwóch domen błędów, gdy naszych maszyny wirtualne są wdrażane. Również wskazywać czy chcemy naszego zestawu rozproszonych w dwóch dostępności **zaktualizować domen**.  Dwie domeny aktualizacji Sprawdź, czy w gdy platforma Azure stosuje aktualizacje oprogramowania naszych zasobów maszyny Wirtualnej są izolowane, co uniemożliwia całe oprogramowanie uruchomione poniżej naszych maszyny Wirtualnej z aktualizacji w tym samym czasie.

## <a name="configure-virtual-network"></a>Skonfiguruj sieć wirtualną
Przed wdrożeniem niektórych maszyn wirtualnych i przetestować z usługi równoważenia, Utwórz pomocnicze zasoby sieci wirtualnej. Aby uzyskać więcej informacji o sieciach wirtualnych, zobacz [Zarządzanie sieciami wirtualnymi Azure](tutorial-virtual-network.md) samouczka.

### <a name="create-network-resources"></a>Utwórz zasoby sieciowe
Tworzenie sieci wirtualnej z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create). Poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* z podsiecią o nazwie *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
Wirtualne karty sieciowe są tworzone za pomocą [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create). Poniższy przykład tworzy trzy wirtualne karty sieciowe. (Jedną wirtualną kartę Sieciową dla każdej maszyny Wirtualnej można utworzyć dla aplikacji w poniższych krokach). Można utworzyć dodatkowe wirtualne karty sieciowe i maszyn wirtualnych w dowolnym momencie i dodaj je do usługi równoważenia obciążenia:

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a>Tworzenie maszyn wirtualnych w zestawie dostępności

Maszyny wirtualne muszą być tworzone dostępność ustawioną upewnij się, że są one poprawnie dystrybuowana sprzętu. Nie można dodać istniejącej maszyny Wirtualnej do dostępności po jego utworzeniu. 

Po utworzeniu maszyny Wirtualnej przy użyciu [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) określ zestaw, za pomocą dostępności `--availability-set` parametr, aby określić nazwę zestawu dostępności.

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

Mamy teraz dwie maszyny wirtualne w naszym zestawie dostępności nowo utworzony. Ponieważ są one w tym samym zestawie dostępności, Azure zapewni, że maszyn wirtualnych i ich zasobów (w tym dysków z danymi) są rozmieszczane izolowanego sprzętu fizycznego. Tej dystrybucji zapewnia znacznie wyższą dostępność naszych ogólnego rozwiązania maszyny Wirtualnej.

Jedyną operacją, której można napotkać podczas dodawania maszyn wirtualnych jest, że określonego rozmiaru maszyny Wirtualnej nie jest już dostępny do użycia w zestawie dostępności. Ten problem może się zdarzyć, jeśli nie jest dostępna wystarczająca pojemność dodać ją przy zachowaniu zasady izolacji wymusza zestawu dostępności. Można sprawdzić, jakie rozmiarów maszyn wirtualnych są dostępne do użycia w istniejących dostępności ustawić za pomocą `--availability-set list-sizes` parametru.

## <a name="check-for-available-vm-sizes"></a>Sprawdź, czy dostępne rozmiary maszyny Wirtualnej 

Możesz dodać więcej maszyn wirtualnych do później zestaw dostępności, ale musisz wiedzieć, jaki rozmiarów maszyn wirtualnych są dostępne na sprzęcie. Użyj [az listy rozmiarów maszyn wirtualnych zestawu dostępności](/cli/azure/availability-set#list-sizes) Aby wyświetlić listę wszystkich dostępnych rozmiarów na sprzęcie klastra dla zestawu dostępności.

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a>Następne kroki

W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie zestawu dostępności
> * Tworzenie maszyny Wirtualnej w zestawie dostępności
> * Sprawdź dostępne rozmiary maszyny Wirtualnej

Przejdź do następnego samouczkiem, aby poznać zestawy skalowania maszyny wirtualnej.

> [!div class="nextstepaction"]
> [Tworzenie zestawu skalowania maszyn wirtualnych](tutorial-create-vmss.md)

