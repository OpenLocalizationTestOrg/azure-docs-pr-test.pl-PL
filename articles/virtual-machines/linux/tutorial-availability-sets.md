---
title: aaaAvailability ustawia samouczek dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o hello zestawów dostępności dla maszyn wirtualnych systemu Linux na platformie Azure."
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
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>Jak zestawy dostępności toouse


Z tego samouczka dowiesz się, jak tooincrease hello dostępność i niezawodność rozwiązań maszyny wirtualnej na platformie Azure przy użyciu funkcji o nazwie zestawów dostępności. Zestawy dostępności upewnij się, tym powitalne wdrażanie na platformie Azure maszyny wirtualne rozproszone na wielu klastrów izolowanego sprzętu. W ten sposób zapewnia, że jeśli awarii sprzętu lub oprogramowania w systemie Azure wykonywany, jest ograniczona tylko do podzbioru maszyny wirtualne i które rozwiązania ogólną pozostanie dostępny i działa z punktu widzenia hello klientów przy użyciu go.

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie zestawu dostępności
> * Tworzenie maszyny Wirtualnej w zestawie dostępności
> * Sprawdź dostępne rozmiary maszyny Wirtualnej


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="availability-set-overview"></a>Omówienie zestawu dostępności

Zestawu dostępności jest funkcją logicznego grupowania, które można użyć w Azure tooensure hello zasobów maszyny Wirtualnej, który można umieścić w niej są odizolowane od siebie, gdy są wdrożone w centrum danych Azure. Azure zapewnia, że hello maszyn wirtualnych zostanie umieszczony w obrębie zestawu dostępności uruchamiania na wielu serwerach fizycznych, obliczeniowe stojakami jednostek magazynowych i przełączniki sieciowe. Dzięki temu w zdarzeniu hello sprzętu lub oprogramowania Azure awarii, jest ograniczona tylko podzestaw maszyn wirtualnych, a pozostanie się i kontynuować klientów dostępne tooyour toobe ogólną aplikacji. Przy użyciu zestawów dostępności jest tooleverage podstawowych możliwości, gdy trzeba toobuild niezawodne rozwiązania.

Zastanówmy typowe rozwiązania oparte na Maszynach którym może mieć 4 serwery frontonu sieci web i korzystać z 2 maszyny wirtualne zaplecza, które hostują bazy danych. Przy użyciu platformy Azure, trzeba będzie toodefine dwa zestawy dostępności przed wdrożeniem maszyny wirtualne: zbiór jednej dostępności dla warstwy "web" hello i jeden zbiór dostępności dla warstwy "baza danych" hello. Podczas tworzenia nowej maszyny Wirtualnej można określić zestaw jako maszynę wirtualną az toohello parametr Utwórz polecenie, a Azure zostanie automatycznie upewnij się, że hello maszyny wirtualne utworzone w hello dostępne dostępności hello zestawu są izolowane między wieloma zasobami sprzętu fizycznego. Oznacza to, że jeśli hello sprzętem fizycznym, który działa jeden z serwera sieci Web lub maszyn wirtualnych z serwera bazy danych na ma problem, wiesz, że hello inne wystąpienia serwera sieci Web i bazy danych w maszynach wirtualnych pozostanie uruchomione prawidłowo, ponieważ znajdują się na inny komputer.

Zawsze należy używać zestawów dostępności, jeśli chcesz toodeploy niezawodnej wirtualna rozwiązań opartych na platformie Azure.


## <a name="create-an-availability-set"></a>Tworzenie zestawu dostępności

Możesz utworzyć zestaw przy użyciu danych o dostępności [tworzenia maszyny wirtualnej az zestawu dostępności](/cli/azure/vm/availability-set#create). W tym przykładzie ustawiliśmy na obu hello liczby domen aktualizacji i odporność na *2* dla zestawu o nazwie dostępności hello *myAvailabilitySet* w hello *myResourceGroupAvailability*grupy zasobów.

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

Zestawy dostępności pozwalają tooisolate zasobów między "domen błędów" i "Aktualizuj domeny". A **domeny błędów** reprezentuje kolekcję izolowanego server + sieć i Magazyn zasobów. W hello poprzedzających przykład możemy wskazać chcemy zestawu dostępności naszych toobe dystrybuowana do co najmniej dwóch domen błędów po naszej maszyny wirtualne są wdrażane. Również wskazywać czy chcemy naszego zestawu rozproszonych w dwóch dostępności **zaktualizować domen**.  Dwie domeny aktualizacji Sprawdź, czy gdy platforma Azure stosuje aktualizacje oprogramowania naszych zasobów maszyny Wirtualnej są izolowane uniemożliwia całe oprogramowanie hello systemem poniżej naszych maszyny Wirtualnej z aktualizacji na powitania tym samym czasie.

## <a name="configure-virtual-network"></a>Konfigurowanie sieci wirtualnej
Przed wdrożeniem niektórych maszyn wirtualnych i przetestować z usługi równoważenia, Utwórz hello obsługi zasobów sieci wirtualnej. Aby uzyskać więcej informacji o sieciach wirtualnych, zobacz hello [Zarządzanie sieciami wirtualnymi Azure](tutorial-virtual-network.md) samouczka.

### <a name="create-network-resources"></a>Utwórz zasoby sieciowe
Tworzenie sieci wirtualnej z [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create). Witaj poniższy przykład tworzy sieć wirtualną o nazwie *myVnet* z podsiecią o nazwie *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
Wirtualne karty sieciowe są tworzone za pomocą [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create). Witaj poniższy przykład tworzy trzy wirtualne karty sieciowe. (Jedną wirtualną kartę Sieciową dla każdej maszyny Wirtualnej można utworzyć dla aplikacji w hello następujące kroki). Można tworzyć dodatkowe wirtualne karty sieciowe i maszyn wirtualnych w dowolnym momencie i dodać je toohello usługi równoważenia obciążenia:

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

Maszyny wirtualne, musi zostać utworzony w toomake zestaw dostępności hello się, że poprawnie dystrybuowana ich hello sprzętu. Nie można dodać istniejącej maszyny Wirtualnej tooan zestaw danych o dostępności po jego utworzeniu. 

Po utworzeniu maszyny Wirtualnej przy użyciu [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) Określ dostępności hello ustawić za pomocą hello `--availability-set` parametru toospecify hello nazwa zbioru dostępności hello.

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

Mamy teraz dwie maszyny wirtualne w naszym zestawie dostępności nowo utworzony. Ponieważ są one takie same hello zestawu dostępności Azure zapewnia tego hello maszyn wirtualnych i wszystkich ich zasobów (w tym dysków z danymi) są rozproszone na izolowanego sprzętu fizycznego. Tej dystrybucji zapewnia znacznie wyższą dostępność naszych ogólnego rozwiązania maszyny Wirtualnej.

Jedyną operacją, której można napotkać podczas dodawania maszyn wirtualnych jest, że dla określonego rozmiaru maszyny Wirtualnej nie jest już dostępne toouse w zestawie dostępności. Ten problem może się zdarzyć, jeśli nie ma wystarczającej liczby tooadd pojemności, które przy zachowaniu zestawu dostępności hello zasady izolacji hello wymusza. Możesz sprawdzić toosee rozmiarów maszyn wirtualnych, które są dostępne toouse istniejących dostępność ustawić za pomocą hello `--availability-set list-sizes` parametru.

## <a name="check-for-available-vm-sizes"></a>Sprawdź, czy dostępne rozmiary maszyny Wirtualnej 

Możesz dodać więcej maszyn wirtualnych później zestaw dostępności toohello, ale trzeba się tooknow rozmiarów maszyn wirtualnych, które są dostępne na powitania sprzętu. Użyj [az listy rozmiarów maszyn wirtualnych zestawu dostępności](/cli/azure/availability-set#list-sizes) toolist wszystkie dostępne rozmiary hello na powitania sprzętu klastra hello zestawu dostępności.

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

Przejdź dalej toolearn samouczka toohello o zestawy skalowania maszyny wirtualnej.

> [!div class="nextstepaction"]
> [Tworzenie zestawu skalowania maszyn wirtualnych](tutorial-create-vmss.md)

