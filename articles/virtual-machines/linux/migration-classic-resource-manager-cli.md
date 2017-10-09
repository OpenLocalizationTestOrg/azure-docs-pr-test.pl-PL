---
title: "aaaMigrate tooResource maszyn wirtualnych Menedżera przy użyciu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono hello obsługiwane platformy migracji zasobów z klasycznym tooAzure Resource Manager przy użyciu wiersza polecenia platformy Azure"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a>Migracja zasobów IaaS z klasycznym tooAzure Menedżera zasobów przy użyciu wiersza polecenia platformy Azure
Te kroki pokazują, jak toouse Azure interfejsu wiersza polecenia (CLI) polecenia toomigrate infrastruktura jako usługa (IaaS) zasoby z modelu wdrażania usługi Azure Resource Manager toohello hello wdrażania klasycznego modelu. Artykuł Hello wymaga hello [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md).

> [!NOTE]
> Wszystkie operacje hello opisane w tym miejscu są idempotentności. Jeśli masz problem niż nieobsługiwanej funkcji lub błąd konfiguracji, zalecamy możesz ponowić próbę hello przygotowanie, przerwania lub przekazania operacji. Platforma Hello spróbuj hello akcję ponownie.
> 
> 

<br>
Poniżej przedstawiono kolejność hello tooidentify schemat blokowy, w którym kroki należy wykonać podczas procesu migracji toobe

![Zrzut ekranu pokazujący hello kroków migracji](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a>Krok 1: Przygotowanie do migracji
Poniżej przedstawiono kilka najlepsze rozwiązania, które firma Microsoft zaleca jako ocenić migracji zasobów IaaS z klasycznym tooResource Menedżera:

* Zapoznaj się z artykułem hello [lista nieobsługiwanych konfiguracji lub funkcji](../windows/migration-classic-resource-manager-overview.md). Jeśli masz maszyn wirtualnych, które używają nieobsługiwane konfiguracje i funkcje, firma Microsoft zaleca, poczekaj toobe obsługi funkcji/konfiguracji hello anonsowania. Alternatywnie można usunąć tej funkcji lub wychodzenia z tej konfiguracji tooenable migracji, jeśli go odpowiada Twoim potrzebom.
* Jeśli mają automatyczny skrypty, które obecnie wdrażanie infrastruktury i aplikacji, spróbuj toocreate podobnych konfiguracji testu przy użyciu tych skryptów do migracji. Można też skonfigurować próbkę środowiskami przy użyciu hello portalu Azure.

> [!IMPORTANT]
> Migracji z klasycznym tooResource Menedżera bramy aplikacji nie są obecnie obsługiwane. toomigrate klasycznej sieci wirtualnej z bramy aplikacji usunąć bramę hello przed uruchomieniem operacji Prepare toomove hello sieci. Po zakończeniu migracji hello ponownie hello bramy w usłudze Azure Resource Manager. 
>
>Łączenie obwody tooExpressRoute w innej subskrypcji bram usługi ExpressRoute nie może być migrowane automatycznie. W takiej sytuacji należy usunąć bramę usługi ExpressRoute hello, migrację sieci wirtualnej hello i Utwórz ponownie hello bramy. Zobacz [ExpressRoute migracji obwody i skojarzone sieci wirtualne od modelu wdrażania Menedżera zasobów klasycznych toohello hello](../../expressroute/expressroute-migration-classic-resource-manager.md) Aby uzyskać więcej informacji.
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a>Krok 2: Ustaw swoją subskrypcję i zarejestrować dostawcę hello
Scenariusze migracji należy tooset Twojego środowiska dla obu classic i Menedżera zasobów. [Zainstaluj interfejs wiersza polecenia Azure](../../cli-install-nodejs.md) i [Wybierz subskrypcję](../../xplat-cli-connect.md).

Konto logowania tooyour.

    azure login

Wybierz hello subskrypcji platformy Azure przy użyciu następującego polecenia hello.

    azure account set "<azure-subscription-name>"

> [!NOTE]
> Rejestracja jest jeden raz krok jednak wymaga toobe wykonywane raz, przed podjęciem próby wykonania migracji. Bez rejestracji zostanie wyświetlony następujący komunikat o błędzie hello 
> 
> *Element BadRequest: Subskrypcja nie jest zarejestrowana do migracji.* 
> 
> 

Zarejestruj się w dostawcy zasobów hello migracji za pomocą następującego polecenia hello. Należy pamiętać, że w niektórych przypadkach to polecenie upłynie limit czasu. Jednak hello będzie można pomyślnie.

    azure provider register Microsoft.ClassicInfrastructureMigrate

Poczekaj pięć minut hello toofinish rejestracji. Za pomocą następującego polecenia hello można sprawdzić stan hello hello zatwierdzania. Upewnij się, że jest RegistrationState `Registered` przed kontynuowaniem.

    azure provider show Microsoft.ClassicInfrastructureMigrate

Teraz przełącznik CLI toohello `asm` tryb.

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>Krok 3: Upewnij się, że masz wystarczająco dużo rdzeni maszyny wirtualnej Azure Resource Manager w hello region platformy Azure dla bieżącego wdrożenia lub sieci Wirtualnej
W tym kroku musisz tooswitch zbyt`arm` tryb. W tym z hello następujące polecenia.

```
azure config mode arm
```

Możesz użyć powitania po interfejsu wiersza polecenia polecenie toocheck hello Bieżąca ilość rdzeni, do których masz usługi Azure Resource Manager. toolearn więcej informacji na temat przydziały core, zobacz [limity i hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

Po zakończeniu sprawdzenia tego kroku, możesz przełączyć ponownie zbyt`asm` tryb.

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a>Krok 4: Opcja 1 — migracji maszyn wirtualnych w usłudze w chmurze
Pobranie listy hello usługi w chmurze przy użyciu hello następujące polecenie, a następnie usługa w chmurze hello pobrania, które mają toomigrate. Należy pamiętać, że jeśli hello maszyn wirtualnych w usłudze w chmurze hello znajdują się w sieci wirtualnej lub mają one role sieć web/proces roboczy, zostanie wyświetlony komunikat o błędzie.

    azure service list

Witaj uruchom następujące polecenie Nazwa wdrożenia hello tooget dla usługi w chmurze hello z hello pełne dane wyjściowe. W większości przypadków hello Nazwa wdrożenia jest hello taka sama jak nazwa usługi w chmurze hello.

    azure service show <serviceName> -vv

Po pierwsze sprawdzanie poprawności w przypadku migrowania usługi w chmurze hello za pomocą następującego polecenia hello:

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

Przygotuj maszyny wirtualne hello hello w usłudze w chmurze do migracji. Masz dwie opcje toochoose z.

Toomigrate hello maszyn wirtualnych tooa utworzone platformy sieci wirtualnej firmy, należy użyć hello następujące polecenia.

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

Tooan toomigrate istniejącej sieci wirtualnej w modelu wdrażania usługi Resource Manager hello firmy, należy użyć hello następujące polecenia.

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

Po przygotowanie hello operacja się powiodła, można przeglądać hello pełne dane wyjściowe tooget hello migracji stanu hello maszyn wirtualnych i upewnij się, że są one hello `Prepared` stanu.

    azure vm show <vmName> -vv

Sprawdź konfigurację hello hello przygotowany zasobów przy użyciu interfejsu wiersza polecenia lub hello portalu Azure. Jeśli nie jest jeszcze gotowa do migracji i ma toogo toohello wstecz poprzedni stan, użyj hello następujące polecenia.

    azure service deployment abort-migration <serviceName> <deploymentName>

Jeśli hello przygotowane Konfiguracja wygląda dobrze, można przejść do przodu i zatwierdzić hello zasobów za pomocą następującego polecenia hello.

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a>Krok 4: Opcja 2 — migracji maszyn wirtualnych w sieci wirtualnej
Pobranie hello sieci wirtualnej, które mają toomigrate. Należy pamiętać, że jeśli hello sieć wirtualna zawiera role sieć web/proces roboczy lub maszyn wirtualnych z nieobsługiwaną konfiguracją, otrzymasz komunikat o błędzie weryfikacji.

Pobierz wszystkie sieci wirtualne hello w subskrypcji hello za pomocą następującego polecenia hello.

    azure network vnet list

Witaj dane wyjściowe będą wyglądać następująco:

![Zrzut ekranu przedstawiający hello wiersza polecenia o nazwie całej sieci wirtualnej hello wyróżnione.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

W hello powyżej przykładzie, hello **virtualNetworkName** jest hello całą nazwę **"Classicubuntu16 classicubuntu16 grupy"**.

Po pierwsze sprawdzanie poprawności w przypadku migrowania hello sieci wirtualnej przy użyciu hello następujące polecenie:

```shell
azure network vnet validate-migration <virtualNetworkName>
```

Przygotowania do migracji sieci wirtualnej hello wybranych przez użytkownika, za pomocą następującego polecenia hello.

    azure network vnet prepare-migration <virtualNetworkName>

Sprawdź konfigurację hello hello przygotowany maszyn wirtualnych przy użyciu interfejsu wiersza polecenia lub hello portalu Azure. Jeśli nie jest jeszcze gotowa do migracji i ma toogo toohello wstecz poprzedni stan, użyj hello następujące polecenia.

    azure network vnet abort-migration <virtualNetworkName>

Jeśli hello przygotowane Konfiguracja wygląda dobrze, można przejść do przodu i zatwierdzić hello zasobów za pomocą następującego polecenia hello.

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a>Krok 5: Migrowanie konta magazynu
Po zakończeniu migracji maszyn wirtualnych hello, zaleca się migrowanie hello konta magazynu.

Przygotuj hello konta magazynu do migracji za pomocą następującego polecenia hello

    azure storage account prepare-migration <storageAccountName>

Sprawdź konfigurację hello hello przygotowane konta magazynu przy użyciu interfejsu wiersza polecenia lub hello portalu Azure. Jeśli nie jest jeszcze gotowa do migracji i ma toogo toohello wstecz poprzedni stan, użyj hello następujące polecenia.

    azure storage account abort-migration <storageAccountName>

Jeśli hello przygotowane Konfiguracja wygląda dobrze, można przejść do przodu i zatwierdzić hello zasobów za pomocą następującego polecenia hello.

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a>Następne kroki

* [Omówienie migracji zasobów IaaS z klasycznym tooAzure Resource Manager obsługiwane platformy](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Techniczne szczegółowe informacje na temat migracji z obsługiwanych platform z klasycznym tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Planowanie migracji zasobów IaaS z klasycznym tooAzure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Użyj programu PowerShell toomigrate IaaS zasobów z klasycznym tooAzure Resource Manager](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Narzędzia z migracji zasobów IaaS z klasycznym tooAzure Menedżera zasobów społeczności](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Przegląd najbardziej typowych błędów migracji](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello przeglądu najczęściej zadawane pytania dotyczące migracji zasobów IaaS z klasycznym tooAzure Menedżera zasobów](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
