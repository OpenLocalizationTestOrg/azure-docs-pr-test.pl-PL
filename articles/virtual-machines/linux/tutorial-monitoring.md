---
title: aaaMonitor maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toomonitor rozruchu diagnostyki i metryki wydajności na maszynie wirtualnej systemu Linux na platformie Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a>Jak toomonitor maszyny wirtualnej systemu Linux na platformie Azure

tooensure maszyn wirtualnych (VM) na platformie Azure działają poprawnie, można przejrzeć diagnostyki rozruchu i metryki wydajności. Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Włącz diagnostykę rozruchu na powitania maszyny Wirtualnej
> * Wyświetlanie diagnostyki rozruchu
> * Wyświetlaj metryki hosta
> * Włącz rozszerzenia diagnostyki na powitania maszyny Wirtualnej
> * Wyświetlaj metryki maszyny Wirtualnej
> * Tworzenie alertów w oparciu metryki diagnostycznych
> * Skonfiguruj zaawansowane monitorowanie


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-vm"></a>Tworzenie maszyny wirtualnej

Diagnostyka toosee i metryki w akcji, należy maszyny Wirtualnej. Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupMonitor* w hello *eastus* lokalizacji.

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

Teraz Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm#create). Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM*:

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a>Włącz diagnostykę rozruchu

Jak rozruchu maszyn wirtualnych systemu Linux, rozszerzenia diagnostyki rozruchu hello przechwytuje dane wyjściowe rozruchu i zapisuje go w magazynie Azure. Może to być problemy rozruchu maszyny Wirtualnej tootroubleshoot używane. Diagnostyki rozruchu nie są automatycznie włączone, podczas tworzenia maszyny Wirtualnej systemu Linux przy użyciu hello wiersza polecenia platformy Azure.

Przed włączeniem diagnostyki rozruchu, konto magazynu na potrzeby toobe utworzony do przechowywania dzienników rozruchu. Konta magazynu musi mieć globalnie unikatowej nazwy należeć do zakresu od 3 do 24 znaków i musi zawierać tylko cyfry i małe litery. Utwórz konto magazynu z hello [Tworzenie konta magazynu az](/cli/azure/storage/account#create) polecenia. W tym przykładzie losowy ciąg jest używany toocreate nazwy konta magazynu unikatowy. 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

Podczas włączania diagnostyki rozruchu, wymagany jest kontener magazynu obiektów blob toohello URI hello. Witaj następujące kwerendy polecenia hello tooreturn konta magazynu tego identyfikatora URI. Witaj wartość identyfikatora URI jest przechowywany w nazwach zmiennych *bloburi*, która jest używana w hello następnego kroku.

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

Teraz Włącz diagnostyki rozruchu z [włączyć diagnostyki rozruchu az wirtualna](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable). Witaj `--storage` wartość jest hello obiektu blob identyfikatora URI zebrane w poprzednim kroku hello.

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a>Wyświetlanie diagnostyki rozruchu

Po włączeniu diagnostyki rozruchu zawsze zatrzymywania i uruchamiania hello maszyny Wirtualnej, informacje na temat procesu rozruchu hello są zapisywane tooa pliku dziennika. W tym przykładzie najpierw cofnąć hello maszyny Wirtualnej z hello [deallocate wirtualna az](/cli/azure/vm#deallocate) polecenia w następujący sposób:

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

Teraz uruchomić hello maszyny Wirtualnej z hello [uruchomienia maszyny wirtualnej az]( /cli/azure/vm#stop) polecenia w następujący sposób:

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

Można uzyskać hello danych diagnostyki rozruchu dla *myVM* z hello [az maszyny wirtualnej diagnostyki rozruchu get rozruchu — dziennik](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) polecenia w następujący sposób:

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a>Wyświetlaj metryki hosta

Maszynę wirtualną systemu Linux zawiera dedykowany hosta na platformie Azure, która współdziała ona z. Metryki są automatycznie pobierane hello hosta i mogą być wyświetlane w portalu Azure hello w następujący sposób:

1. W hello portalu Azure, kliknij przycisk **grup zasobów**, wybierz pozycję **myResourceGroupMonitor**, a następnie wybierz **myVM** hello listy zasobów.
1. toosee wykonuje hello hosta maszyny Wirtualnej, kliknij **metryki** na powitania bloku maszyny Wirtualnej, następnie wybierz jedno z hello *[Host]* metryki w obszarze **dostępne metryki**.

    ![Wyświetlaj metryki hosta](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a>Zainstaluj rozszerzenie diagnostyki

> [!IMPORTANT]
> Ten dokument zawiera opis wersji 2.3 hello diagnostycznych rozszerzenia systemu Linux, która została wycofana. Wersja 2.3 będzie obsługiwana do 30 czerwca 2018.
>
> Zamiast tego można włączyć w wersji 3.0 hello rozszerzenia diagnostyczne systemu Linux. Aby uzyskać więcej informacji, zobacz [hello dokumentacji](./diagnostic-extension.md).

Witaj hosta podstawowe metryki są dostępne, ale toosee bardziej szczegółowe i metryki specyficzne dla maszyny Wirtualnej, możesz tooneed tooinstall hello Azure diagnostics rozszerzenia na powitania maszyny Wirtualnej. Witaj rozszerzenia diagnostyki Azure umożliwia dodatkowe funkcje monitorowania i diagnostyki toobe dane pobrane z hello maszyny Wirtualnej. Możesz wyświetlić te metryki wydajności i tworzyć alerty oparte na sposób wykonywania hello maszyny Wirtualnej. rozszerzenie diagnostycznych Hello jest instalowany za pośrednictwem portalu Azure hello:

1. W hello portalu Azure, kliknij przycisk **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** hello listy zasobów.
1. Kliknij przycisk **ustawienia diagnostyki**. Lista Hello wskazuje, że *diagnostyki rozruchu* są już włączone w poprzedniej sekcji hello. Kliknij pole wyboru hello *podstawowe metryki*.
1. W hello *konta magazynu* Przejdź hello wybierz tooand *mydiagdata [1234]* konto utworzone w poprzedniej sekcji hello.
1. Kliknij przycisk hello **zapisać** przycisku.

    ![Wyświetlaj metryki diagnostycznych](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a>Wyświetlaj metryki maszyny Wirtualnej

Witaj metryki maszyny Wirtualnej można wyświetlić w hello taki sam sposób, aby wyświetlić metryki maszyny Wirtualnej hosta hello:

1. W hello portalu Azure, kliknij przycisk **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** hello listy zasobów.
1. toosee wykonuje hello maszyny Wirtualnej, kliknij **metryki** na hello bloku maszyny Wirtualnej, a następnie wybierz dowolną hello diagnostyki metryki w obszarze **dostępne metryki**.

    ![Wyświetlaj metryki maszyny Wirtualnej](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a>Tworzenie alertów

Można tworzyć alertów w oparciu metryki dotyczące wydajności. Alerty można używane toonotify, który podczas średniego użycia procesora CPU przekracza określonego progu lub wolnego miejsca na dysku spada poniżej pewnego, np. Alerty są wyświetlane w portalu Azure hello lub mogą być wysyłane za pośrednictwem poczty e-mail. W odpowiedzi tooalerts generowaną może także wyzwolić elementu runbook usługi Automatyzacja Azure lub usługi Azure Logic Apps.

Witaj poniższy przykład tworzy alert dla średniego użycia procesora CPU.

1. W hello portalu Azure, kliknij przycisk **grup zasobów**, wybierz pozycję **myResourceGroup**, a następnie wybierz **myVM** hello listy zasobów.
2. Kliknij przycisk **reguły alertów** na powitania bloku maszyny Wirtualnej, następnie kliknij przycisk **Dodaj alert metryki** hello górze hello blok alerty.
4. Podaj **nazwa** alertu, takie jak *myAlertRule*
5. tootrigger alert, gdy procent użycia procesora CPU przekracza 1.0 przez pięć minut, pozostaw hello wszystkich innych wartości domyślnych wybrane.
6. Opcjonalnie, zaznacz pole hello *E-mail właściciele, współautorzy i czytelnicy* toosend powiadomienia e-mail. Akcja domyślna Hello jest toopresent powiadomienia w portalu hello.
7. Kliknij przycisk hello **OK** przycisku.


## <a name="advanced-monitoring"></a>Zaawansowane monitorowanie 

Możliwość bardziej zaawansowane monitorowanie maszyny wirtualnej za pomocą [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview). Jeśli nie zostało to jeszcze zrobione, należy zarejestrować się w celu [bezpłatnej wersji próbnej](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) programu Operations Management Suite.

Jeśli masz portalu OMS toohello dostępu można znaleźć identyfikator obszaru roboczego hello klucza i obszar roboczy w bloku ustawień hello. Zastąp < klucz obszaru roboczego > i < identyfikator obszaru roboczego > z wartościami hello z Twojej OMS można użyć obszaru roboczego, a następnie możesz **zestaw rozszerzenia maszyny wirtualnej az** tooadd hello OMS rozszerzenia toohello maszyny Wirtualnej:

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

W bloku dziennika wyszukiwania hello portalu OMS hello, powinien zostać wyświetlony *myVM* takich jak co przedstawiono na poniższej ilustracji hello:

![Blok OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>Następne kroki

W tym samouczku został skonfigurowany i przejrzeć maszyn wirtualnych w Centrum zabezpieczeń Azure. W tym samouczku omówiono:

> [!div class="checklist"]
> * Włącz diagnostykę rozruchu na powitania maszyny Wirtualnej
> * Wyświetlanie diagnostyki rozruchu
> * Wyświetlaj metryki hosta
> * Włącz rozszerzenia diagnostyki na powitania maszyny Wirtualnej
> * Wyświetlaj metryki maszyny Wirtualnej
> * Tworzenie alertów w oparciu metryki diagnostycznych
> * Skonfiguruj zaawansowane monitorowanie

Przejdź dalej toolearn samouczka toohello temat Centrum zabezpieczeń Azure.

> [!div class="nextstepaction"]
> [Zarządzanie zabezpieczeniami maszyn wirtualnych](./tutorial-azure-security.md)