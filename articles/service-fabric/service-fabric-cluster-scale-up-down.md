---
title: "aaaScale usługi sieć szkieletowa klastra przychodzący lub wychodzący | Dokumentacja firmy Microsoft"
description: "Skalowanie klastra usługi sieć szkieletowa przychodzący lub wychodzący żądanie toomatch ustawiając zasady automatycznego skalowania dla zestawu skalowania maszyn typu/wirtualnej każdego węzła. Dodawanie lub usuwanie klastra sieci szkieletowej usług tooa węzłów"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: aeb76f63-7303-4753-9c64-46146340b83d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: 37cfeaf80edc016cf6de017d1c2dc6fbcb8acc2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-in-or-out-using-auto-scale-rules"></a>Skalowanie klastra usługi sieć szkieletowa przychodzący lub wychodzący przy użyciu reguł automatycznego skalowania
Zestawy skalowania maszyny wirtualnej są zasobami obliczeń platformy Azure można użyć toodeploy i zarządzanie kolekcją jako zestaw maszyn wirtualnych. Każdy typ węzła który jest zdefiniowany w klastrze usługi sieć szkieletowa jest skonfigurowany jako osobny zestaw skali maszyny wirtualnej. Każdy typ węzła można skalować w lub wychodzących niezależnie, mają różne zestawy otwartych portów i może mieć inną pojemność metryki. Dowiedz się więcej o w hello [elementów sieci szkieletowej usług NodeType](service-fabric-cluster-nodetypes.md) dokumentu. Ponieważ hello typy węzłów sieci szkieletowej usług w klastrze składają się z zestawy skalowania maszyny wirtualnej na powitania wewnętrznej bazy danych, należy tooset reguł automatycznego skalowania dla zestawu skalowania maszyn typu/wirtualnej każdego węzła.

> [!NOTE]
> Subskrypcja musi mieć wystarczająco dużo tooadd rdzeni hello nowe maszyny wirtualne wchodzące w skład tego klastra. Nie ma Weryfikacja modelu nie, aby uzyskać awaria czas wdrażania, jeśli dowolne limity przydziału hello są osiągane.
> 
> 

## <a name="choose-hello-node-typevirtual-machine-scale-set-tooscale"></a>Wybierz tooscale zestawu hello węzła typu/wirtualnej skalowania maszyny
Obecnie nie jest możliwe toospecify hello zasady automatycznego skalowania zestawy skalowania maszyny wirtualnej za pomocą portalu hello, więc poinformować nas, użyj typy węzłów hello toolist programu Azure PowerShell (1.0 +), a następnie dodaj toothem reguły automatycznego skalowania.

Lista hello tooget zestawu skalowania maszyny wirtualnej tworzą klaster, uruchom następujące polecenia cmdlet hello:

```powershell
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Compute/VirtualMachineScaleSets

Get-AzureRmVmss -ResourceGroupName <RGname> -VMScaleSetName <Virtual Machine scale set name>
```

## <a name="set-auto-scale-rules-for-hello-node-typevirtual-machine-scale-set"></a>Zestaw reguł automatycznego skalowania dla zestawu skalowania maszyn hello węzła typu/wirtualnej
Jeśli klaster ma wiele typów węzła, powtórz to dla każdego węzła typy/wirtualnej skalowania maszyny zestawów, które mają tooscale (przychodzący lub wychodzący). Uwzględniać konta hello liczba węzłów potrzebne przed skonfigurowaniem Skalowanie automatyczne. Minimalna liczba węzłów, które muszą mieć dla typu węzła podstawowego hello Hello jest wymuszany przez hello niezawodności poziom, wybrana. Przeczytaj więcej na temat [poziomów niezawodności](service-fabric-cluster-capacity.md).

> [!NOTE]
> Skalowania tooless typu węzła podstawowego hello niż minimalna liczba hello destabilizować hello klastra lub przełączyć go w dół. Może to spowodować utratę danych aplikacji oraz usług systemu hello.
> 
> 

Obecnie hello funkcja automatycznego skalowania nie jest wymuszany przez hello obciążenia mogą być raportowania tooService sieci szkieletowej aplikacji. Więc na powitania tego czasu automatycznego skalowania uzyskasz czysto wynikają z hello liczniki wydajności, które są emitowane przez każde z wystąpień zestawu skalowania maszyn wirtualnych hello.  

Wykonaj te instrukcje [tooset się automatycznego skalowania dla każdego zestawu skali maszyny wirtualnej](../virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview.md).

> [!NOTE]
> W skali w dół scenariusza, chyba że danego typu węzła ma poziom trwałości Gold lub Silver należy toocall hello [polecenia cmdlet Remove-ServiceFabricNodeState](https://msdn.microsoft.com/library/azure/mt125993.aspx) nazwą hello odpowiedni węzeł.
> 
> 

## <a name="manually-add-vms-tooa-node-typevirtual-machine-scale-set"></a>Ręcznie Dodaj maszyny wirtualne tooa węzła typu/wirtualnej zestawu skali maszyny
Wykonaj przykładowe hello/instrukcje hello [galerię szablonów szybki start](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello liczbę maszyn wirtualnych w każdym Nodetype. 

> [!NOTE]
> Dodawanie maszyn wirtualnych jest czasochłonne, więc nie będzie toobe dodatków hello natychmiastowe. Dlatego planowania pojemności tooadd również w czasie, tooallow przez ponad 10 minut przed hello pojemności maszyny Wirtualnej jest dostępna dla replik hello / service tooget wystąpień umieszczona.
> 
> 

## <a name="manually-remove-vms-from-hello-primary-node-typevirtual-machine-scale-set"></a>Ręcznie usuń maszyny wirtualne z zestawu skali maszyny hello węzła podstawowego typu/wirtualnej
> [!NOTE]
> Witaj Usługa sieci szkieletowej systemu usługi uruchomione w hello typu podstawowego węzła w klastrze. Nigdy nie należy zamknąć lub dół hello liczba wystąpień w tym typy węzłów mniejsza niż jakie warstwa niezawodności hello gwarantuje. Odwołuje się zbyt[hello szczegółowe informacje w tym miejscu warstwach niezawodności](service-fabric-cluster-capacity.md). 
> 
> 

Należy tooexecute hello następujące kroki jedno wystąpienie maszyny Wirtualnej w czasie. Dzięki temu usługi systemowe hello (i usługi stanowej) toobe prawidłowe zamknięcie na powitania wystąpienia maszyny Wirtualnej spowoduje usunięcie i nowej repliki utworzony w innych węzłach.

1. Uruchom [ServiceFabricNode Wyłącz](https://msdn.microsoft.com/library/mt125852.aspx) konwersji "RemoveNode" toodisable hello węzeł ma tooremove (hello najwyższy wystąpienie tego typu węzła).
2. Uruchom [Get-ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake się, że ten węzeł hello przeszła w rzeczywistości toodisabled. Jeśli nie, poczekaj, aż hello węzła jest wyłączone. Nie można Pospiesz się w tym kroku.
3. Wykonaj przykładowe hello/instrukcje hello [galerię szablonów szybki start](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello liczbę maszyn wirtualnych o jeden w tym typie Nodetype. wystąpienie Hello usunięte jest hello najwyższy wystąpienia maszyny Wirtualnej. 
4. Powtórz kroki od 1 do 3 zgodnie z potrzebami, ale nigdy nie będą skalowane hello liczbę wystąpień w typach węzła podstawowego hello mniej niż gwarantuje, jakie hello warstwa niezawodności. Odwołuje się zbyt[hello szczegółowe informacje w tym miejscu warstwach niezawodności](service-fabric-cluster-capacity.md). 

## <a name="manually-remove-vms-from-hello-non-primary-node-typevirtual-machine-scale-set"></a>Ręcznie usuń maszyny wirtualne z hello węzła innego niż podstawowy typ/wirtualnej zestawu skali maszyny
> [!NOTE]
> Dla usługi stanowej trzeba pewną liczbę węzłów toobe zawsze toomaintain dostępności i Zachowaj stan usługi. W bardzo minimalna hello należy hello liczba węzłów równy toohello docelowej repliki zestaw liczby partycji hello/usługi. 
> 
> 

Należy hello hello następujące kroki jedno wystąpienie maszyny Wirtualnej w czasie wykonywania. Dzięki temu usług systemowych hello (i usługi stanowej) toobe prawidłowe zamknięcie na powitania wystąpienia maszyny Wirtualnej, które są usuwane, a nowej repliki utworzony else where.

1. Uruchom [ServiceFabricNode Wyłącz](https://msdn.microsoft.com/library/mt125852.aspx) konwersji "RemoveNode" toodisable hello węzeł ma tooremove (hello najwyższy wystąpienie tego typu węzła).
2. Uruchom [Get-ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake się, że ten węzeł hello przeszła w rzeczywistości toodisabled. Jeśli nie, zaczekaj hello węzła jest wyłączone. Nie można Pospiesz się w tym kroku.
3. Wykonaj przykładowe hello/instrukcje hello [galerię szablonów szybki start](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello liczbę maszyn wirtualnych o jeden w tym typie Nodetype. Spowoduje to usunięcie teraz hello najwyższy wystąpienia maszyny Wirtualnej. 
4. Powtórz kroki od 1 do 3 zgodnie z potrzebami, ale nigdy nie będą skalowane hello liczbę wystąpień w typach węzła podstawowego hello mniej niż gwarantuje, jakie hello warstwa niezawodności. Odwołuje się zbyt[hello szczegółowe informacje w tym miejscu warstwach niezawodności](service-fabric-cluster-capacity.md).

## <a name="behaviors-you-may-observe-in-service-fabric-explorer"></a>Zachowania można zaobserwować w narzędziu Service Fabric Explorer
Skalowanie w górę hello klastra Eksploratora usługi sieć szkieletowa będzie odzwierciedlać hello liczba węzłów (wystąpienia zestawu skalowania maszyn wirtualnych), które są częścią klastra hello.  Jednak podczas skalowania klastra w dół możesz zobaczą hello usunięty węzeł/wystąpienia maszyny Wirtualnej wyświetlane w złej kondycji, chyba że wywołujesz [cmd ServiceFabricNodeState Usuń](https://msdn.microsoft.com/library/mt125993.aspx) nazwą hello odpowiedni węzeł.   

Oto hello wyjaśnienia tego zachowania.

Hello węzły wymienionych w narzędziu Service Fabric Explorer są odbicie hello usługi sieć szkieletowa systemu usług (FM specjalnie) zna hello liczby węzłów klastra hello miał ma. Skalowanie hello skalowania maszyny wirtualnej określa hello maszyny Wirtualnej został usunięty, ale usługa systemowa FM nadal podejrzewać, że ten węzeł hello, (które były mapowane toohello maszyny Wirtualnej, który został usunięty) będzie wrócić. Dlatego Service Fabric Explorer nadal toodisplay tego węzła (chociaż może to być błąd lub nieznany stan kondycji hello).

W kolejności toomake się upewnić, że węzeł zostanie usunięta po usunięciu maszyny Wirtualnej dostępne są dwie opcje:

1) Wybierz poziom trwałości Gold lub Silver (dostępne wkrótce) dla hello typy węzłów w klastrze, które zapewnia hello integracji infrastruktury. Które następnie automatycznie usunie hello węzłów z naszych stanu usługi (FM) systemu skalowanie w.
Odwołuje się zbyt[hello szczegółów dotyczących poziomów trwałości tutaj](service-fabric-cluster-capacity.md)

2) Po wystąpieniu maszyny Wirtualnej hello zostały skalowany w dół, należy toocall hello [polecenia cmdlet Remove-ServiceFabricNodeState](https://msdn.microsoft.com/library/mt125993.aspx).

> [!NOTE]
> Usługi sieci szkieletowej klastry wymagają określonej liczby węzłów toobe się na cały czas hello w kolejności toomaintain dostępności i Zachowaj stan — określonego tooas "utrzymywania kworum". Tak, jest zazwyczaj niebezpieczne tooshut dół wszystkich maszyn hello w klastrze hello, chyba że najpierw wykonali [pełnej kopii zapasowej według stanu](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Następne kroki
Po tooalso hello odczytu więcej informacji na temat planowania pojemności klastra, Uaktualnianie klastra i partycjonowanie usług:

* [Planowanie pojemności sieci klastra](service-fabric-cluster-capacity.md)
* [Uaktualnienia klastra](service-fabric-cluster-upgrade.md)
* [Usługi stanowej partycji dla maksymalną skalę](service-fabric-concepts-partitioning.md)

<!--Image references-->
[BrowseServiceFabricClusterResource]: ./media/service-fabric-cluster-scale-up-down/BrowseServiceFabricClusterResource.png
[ClusterResources]: ./media/service-fabric-cluster-scale-up-down/ClusterResources.png
