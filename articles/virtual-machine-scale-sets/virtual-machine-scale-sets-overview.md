---
title: informacje o zestawach skali maszyn wirtualnych aaaAzure | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o zestawach skalowania maszyn wirtualnych platformy Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 788b2d1636e0bf4ef3fbf94aed9b3303c5fafa82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-virtual-machine-scale-sets-in-azure"></a>Co to są zestawy skalowania maszyn wirtualnych na platformie Azure?
Zestawy skalowania maszyny wirtualnej są zasobami obliczeń platformy Azure można użyć toodeploy i zarządzać zestawem identycznych maszyn wirtualnych. Z wszystkich maszyn wirtualnych skonfigurowanych hello takie same, zestawy skalowania są zaprojektowane toosupport true skalowania automatycznego i nie wstępnego inicjowania obsługi administracyjnej maszyn wirtualnych jest wymagany. Dlatego jest łatwiejsze usług na dużą skalę toobuild, przeznaczonych dla dużych obliczeniowych, dane big data i konteneryzowanych obciążeń.

W przypadku aplikacji wymagających tooscale zasoby obliczeniowe, a w skali operacji niejawnie równoważy w domenach awarii i aktualizacji. Dla dalszego tooscale wprowadzenie zestawy, można znaleźć toohello [anonsu Azure blog](https://azure.microsoft.com/blog/azure-virtual-machine-scale-sets-ga/).

Aby dowiedzieć się więcej o zestawach skalowania, obejrzyj te klipy wideo:

* [Mark Russinovich omawia zestawy skalowania na platformie Azure](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)  
* [Zestawy skalowania maszyn wirtualnych według Guya Bowermana](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

## <a name="creating-and-managing-scale-sets"></a>Tworzenie zestawów skalowania i zarządzanie nimi
Możesz utworzyć skali w hello [portalu Azure](https://portal.azure.com) wybierając **nowe** i wpisując **skali** na pasku wyszukiwania hello. **Zestaw skali maszyny wirtualnej** znajduje się w wynikach hello. Z tego miejsca można wypełniać hello wymagane pola toocustomize i wdrożyć zestaw skali. Masz również tooset opcji skalowania automatycznego podstawowe reguły na podstawie użycia procesora CPU w portalu hello.

Zestawy skalowania można definiować i wdrażać za pomocą szablonów JSON oraz [interfejsów API REST](https://msdn.microsoft.com/library/mt589023.aspx) — podobnie jak poszczególne maszyny wirtualne w ramach usługi Azure Resource Manager. Można zatem użyć dowolnej standardowej metody wdrażania za pomocą usługi Azure Resource Manager. Aby uzyskać więcej informacji na temat szablonów, zobacz [Tworzenie szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Można znaleźć ustawia zbiór przykład szablony na potrzeby skalowania maszyny wirtualnej w hello [repozytorium GitHub szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates). (Wyszukaj szablony z **vmss** w tytule hello.)

Przykłady szablonów Szybki Start hello przycisk "Wdróż tooAzure" hello readme dla każdego szablonu łączy funkcję wdrażania portalu toohello. skali hello toodeploy ustawić, kliknij przycisk hello, a następnie wprowadź parametry, które są wymagane w portalu hello. 

## <a name="scaling-a-scale-set-out-and-in"></a>Skalowanie zestawu skalowania do wewnątrz i na zewnątrz
Możesz zmienić pojemności hello skali, ustaw w hello portalu Azure, klikając hello **skalowanie** w obszarze **ustawienia**. 

pojemność zestawu skalowania toochange hello w wierszu polecenia, użyj hello **skali** w [interfejsu wiersza polecenia Azure](https://github.com/Azure/azure-cli). Na przykład można użyć tego polecenia tooset 10 maszyn wirtualnych o pojemności tooa zestaw skali:

```bash
az vmss scale -g resourcegroupname -n scalesetname --new-capacity 10 
```

tooset hello liczbę maszyn wirtualnych w skali skonfigurowane przy użyciu programu PowerShell, użyj hello **AzureRmVmss aktualizacji** polecenia:

```PowerShell
$vmss = Get-AzureRmVmss -ResourceGroupName resourcegroupname -VMScaleSetName scalesetname  
$vmss.Sku.Capacity = 10
Update-AzureRmVmss -ResourceGroupName resourcegroupname -Name scalesetname -VirtualMachineScaleSet $vmss
```

tooincrease lub Zmniejsz liczbę hello maszyn wirtualnych w skali skonfigurowane przy użyciu szablonu usługi Azure Resource Manager, zmień hello **pojemności** szablonu hello właściwości i wdróż go ponownie. Prostota ten umożliwia łatwe toointegrate zestawy skalowania automatycznego skalowania Azure lub toowrite własnego niestandardowego skalowania warstwy Jeśli potrzebujesz zdarzenia Skala niestandardowa toodefine tego Azure skalowania automatycznego nie obsługuje. 

Jeśli są ponownego wdrożenia usługi Azure Resource Manager szablonu toochange hello pojemność, można zdefiniować dużo mniejsze szablon, który zawiera tylko hello **SKU** pakiet właściwości z hello zaktualizowane pojemności. [Oto przykład](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing).

## <a name="autoscale"></a>Automatyczne skalowanie

Zestaw skali można opcjonalnie można skonfigurować ustawienia skalowania automatycznego podczas jego tworzenia w hello portalu Azure. Witaj liczbę maszyn wirtualnych można następnie zwiększenia lub zmniejszenia zależności od użycia procesora CPU średnia. 

Wiele hello skalować zestaw szablonów w hello [szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates) zdefiniować ustawienia skalowania automatycznego. Można również dodać tooan Ustawienia skalowania automatycznego istniejący zestaw skali. Na przykład ten skrypt programu PowerShell systemu Azure dodaje zestaw skali tooa dla systemów z procesorem CPU skalowania automatycznego:

```PowerShell

$subid = "yoursubscriptionid"
$rgname = "yourresourcegroup"
$vmssname = "yourscalesetname"
$location = "yourlocation" # e.g. southcentralus

$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Increase -ScaleActionValue 1
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator LessThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Decrease -ScaleActionValue 1
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "autoprofile1"
Add-AzureRmAutoscaleSetting -Location $location -Name "autosetting1" -ResourceGroup $rgname -TargetResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -AutoscaleProfiles $profile1
```

Lista tooscale prawidłowy metryki na można znaleźć w [obsługiwane metryki z monitorem Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md) w obszarze hello pozycji "Microsoft.Compute/virtualMachineScaleSets." Bardziej zaawansowane opcje skalowania automatycznego również są dostępne, w tym oparte na harmonogramie skalowania automatycznego i za pomocą elementów webhook toointegrate z systemami alertu.

## <a name="monitoring-your-scale-set"></a>Monitorowanie zestawu skalowania
Witaj [portalu Azure](https://portal.azure.com) skali list ustawia i przedstawiono ich właściwości. Witaj portal obsługuje również operacji zarządzania. Operacje zarządzania można wykonywać zarówno na zestawach skalowania, jak i na poszczególnych maszynach wirtualnych w zestawie skalowania. Hello portal udostępnia również wykres użycia zasobów można dostosowywać. 

Jeśli konieczne toosee lub edytować hello bazowy JSON definicji zasobu platformy Azure, można również użyć [Eksploratora zasobów Azure](https://resources.azure.com). Zestawy skalowania są zasób w hello dostawcy zasobów Microsoft.Compute Azure. Z tej witryny można wyświetlić ich rozwijając hello następującego łącza:

**Subskrypcje** > **Twoja subskrypcja** > **resourceGroups** > **dostawcy** > **Microsoft.Compute** > **virtualMachineScaleSets** > **zestaw skalowania** itd.

## <a name="scale-set-scenarios"></a>Scenariusze dotyczące zestawów skalowania
W tej sekcji przedstawiono niektóre typowe scenariusze dotyczące zestawów skalowania. Te scenariusze mają zastosowanie w przypadku niektórych usług platformy Azure wyższego poziomu (np. Batch, Service Fabric i Container Service).

* **Użyj protokołu RDP lub SSH tooconnect tooscale Ustaw wystąpień**: zestaw skalowania utworzono w sieci wirtualnej, a poszczególnych maszyn wirtualnych w zestawie skalowania hello są przydzielone domyślnie publiczne adresy IP. Ta zasada pozwala uniknąć wydatków hello oraz zarządzania narzut podziału oddzielne publicznego adresu IP adresów węzłów hello tooall w siatce obliczeń. Jeśli potrzebujesz bezpośrednich połączeń zewnętrznych tooscale ustawić maszyn wirtualnych, można skonfigurować skali zestaw tooautomatically Przypisz publicznego adresu IP adresów toonew maszyn wirtualnych. Alternatywnie możesz połączyć tooVMs od innych zasobów w sieci wirtualnej, które mogą być przydzielone publiczne adresy IP, na przykład autonomicznych maszyn wirtualnych i usług równoważenia obciążenia. 
* **Połącz przy użyciu reguł NAT tooVMs**: tworzenie publicznego adresu IP, przypisz do niego tooa modułu równoważenia obciążenia i zdefiniuj puli NAT dla ruchu przychodzącego. Te akcje są mapowane portów hello portu tooa adresu IP na maszynie Wirtualnej w zestawie skalowania hello. Na przykład:
  
  | Element źródłowy | Port źródłowy | Element docelowy | Port docelowy |
  | --- | --- | --- | --- |
  |  Publiczny adres IP |Port 50000 |vmss\_0 |Port 22 |
  |  Publiczny adres IP |Port 50001 |vmss\_1 |Port 22 |
  |  Publiczny adres IP |Port 50002 |vmss\_2 |Port 22 |
  
   W [w tym przykładzie](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-nat), reguł NAT są zdefiniowane tooenable tooevery połączenia SSH maszyny Wirtualnej w zestawie skalowania, korzystając z jednego publicznego adresu IP adresów.
  
   [W tym przykładzie](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-nat) hello sam RDP i systemu Windows.
* **Połącz przy użyciu "jumpbox" tooVMs**: w przypadku utworzenia zestawu skalowania i autonomicznej maszyny Wirtualnej hello sam wirtualnych sieci, hello autonomicznej maszyny Wirtualnej i hello zestaw skali maszyny Wirtualnej można połączyć tooone innego przy użyciu ich wewnętrznym adresem IP adresy, zgodnie z definicją hello wirtualnego sieci lub podsieci. Jeśli tworzenie publicznego adresu IP i przypisz go toohello autonomicznej maszyny Wirtualnej, można użyć protokołu RDP lub SSH autonomiczny toohello tooconnect maszyny Wirtualnej. Można połączyć z czy skalowania tooyour maszyny ustawić wystąpień. Można tutaj zauważyć, że prosty zestaw skalowania jest z natury bezpieczniejszy niż prosta autonomiczna maszyna wirtualna z publicznym adresem IP w konfiguracji domyślnej.
  
   Na przykład [ten szablon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-jumpbox) wdraża prosty zestaw skalowania z autonomiczną maszyną wirtualną. 
* **Tooscale zestaw wystąpień równoważenia obciążenia**: Jeśli chcesz klastra obliczeniowego tooa toodeliver pracy maszyn wirtualnych przy użyciu podejścia okrężnego, można skonfigurować do modułu równoważenia obciążenia Azure przy użyciu reguł równoważenia obciążenia warstwy 4 odpowiednio. Można określić sondy porty tooverify, że aplikacja jest uruchomiona, wysyłając polecenie ping z określonego protokołu, interwał i ścieżki żądania. Usługa [Azure Application Gateway](https://azure.microsoft.com/services/application-gateway/) obsługuje również zestawy skalowania, a także warstwę 7 oraz bardziej zaawansowane scenariusze równoważenia obciążenia.
  
   [W tym przykładzie](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-web-ssl) tworzy zestaw skalowania, który uruchamia Apache serwerów sieci web który korzysta z obciążenia hello toobalance modułu równoważenia obciążenia, który odbiera każdej maszyny Wirtualnej. (Spójrz na typ zasobu Microsoft.Network/loadBalancers hello i networkProfile i extensionProfile w zestawu skalowania maszyn wirtualnych).

   W [tym przykładzie dla systemu Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-app-gateway) i [tym przykładzie dla systemu Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-app-gateway) użyto usługi Application Gateway.  

* **Wdrażanie zestawu skalowania jako klastra obliczeniowego w menedżerze klastra w środowisku PaaS** — zestawy skalowania są czasami określane jako rola procesu roboczego następnej generacji. Chociaż prawidłowy opis, działa on ryzyka hello mylące skali zestaw funkcji z funkcjami usługi w chmurze Azure. W pewnym sensie zestawy skalowania pełnią rolę procesu roboczego lub stanowią zasób procesu roboczego. Są ogólnym zasobem obliczeniowym, który jest niezależny od platformy/środowiska uruchomieniowego oraz możliwy do dostosowania i zintegrowania z infrastrukturą IaaS usługi Azure Resource Manager.
  
   Rola procesu roboczego usług Cloud Services ma ograniczenia w zakresie obsługi platform/środowiska uruchomieniowego (obsługuje wyłącznie obrazy platformy Windows), ale obejmuje także usługi takie jak wymiana wirtualnego adresu IP, konfigurowane ustawienia uaktualniania i określone ustawienia wdrażania środowiska uruchomieniowego/aplikacji. Te usługi nie są *jeszcze* dostępne w zestawach skalowania lub są zapewniane przez inne usługi PaaS wyższego poziomu, takie jak Azure Service Fabric. Zestawy skalowania można rozumieć jako infrastrukturę obsługującą rozwiązanie PaaS. Rozwiązania PaaS takie jak [Service Fabric](https://azure.microsoft.com/services/service-fabric/) są oparte na tej infrastrukturze.
  
   W [tym przykładzie](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos) takiego podejścia usługa [Azure Container Service](https://azure.microsoft.com/services/container-service/) wdraża klaster oparty na zestawach skalowania z koordynatorem kontenera.

## <a name="scale-set-performance-and-scale-guidance"></a>Wytyczne dotyczące wydajności i skalowania zestawów skalowania
* Obsługuje zestaw skalowania w górę too1, 000 maszyn wirtualnych. Jeśli tworzenie i przekazywanie własnych niestandardowych obrazów maszyn wirtualnych, hello limit wynosi 100. Uwagi dotyczące korzystania z dużych zestawów skalowania znajdziesz w temacie [Praca z dużymi zestawami skalowania maszyn wirtualnych](virtual-machine-scale-sets-placement-groups.md).
* Nie masz toopre-utworzyć zestawy skalowania toouse konta magazynu platformy Azure. Obsługa zestawów skalowania Azure zarządzane dyski, które odwrócić problemów z wydajnością o hello liczbę dysków na konto magazynu. Aby uzyskać więcej informacji, zobacz [Zestawy skalowania maszyn wirtualnych i dyski zarządzane](virtual-machine-scale-sets-managed-disks.md).
* Aby uzyskać krótsze i bardziej przewidywalne czasy aprowizacji maszyny wirtualnej oraz lepszą wydajność operacji we/wy, rozważ użycie magazynu Azure Premium Storage zamiast magazynu Azure Storage.
* limit przydziału rdzeni Hello w regionie hello, w której wdrażasz ogranicza hello liczbę maszyn wirtualnych można utworzyć. Konieczne może tooincrease techniczną toocontact limitu przydziału obliczeń, nawet jeśli obecnie istnieje limit wysokiej rdzeni do użycia z usługami w chmurze Azure. tooquery limitu przydziału, uruchom to polecenie wiersza polecenia platformy Azure: `azure vm list-usage`. Alternatywnie uruchom następujące polecenie programu PowerShell: `Get-AzureRmVMUsage`.

## <a name="frequently-asked-questions-for-scale-sets"></a>Często zadawane pytania dotyczące zestawów skalowania
**PYTANIE** Ile maszyn wirtualnych może się znajdować w zestawie skalowania?

**ODPOWIEDŹ** Zestaw skali może mieć 0 too1, 000 maszyn wirtualnych w oparciu obrazy platformy lub 0 too100 maszyny wirtualne oparte na niestandardowych obrazów. 

**PYTANIE** Czy zestawy skalowania obsługują dyski danych?

**ODPOWIEDŹ** Tak. Zestaw skali można zdefiniować konfigurację dysków dołączonych danych, która dotyczy maszyn wirtualnych tooall hello zestawu. Aby uzyskać więcej informacji, zobacz [Zestawy skalowania na platformie Azure i dołączone dyski danych](virtual-machine-scale-sets-attached-disks.md). Oto przykłady innych opcji magazynowania danych:

* Pliki platformy Azure (dyski udostępnione za pośrednictwem protokołu SMB)
* Dysk systemu operacyjnego
* Dysk tymczasowy (lokalny, bez kopii zapasowej w usłudze Azure Storage)
* Usługa danych platformy Azure (na przykład tabele platformy Azure, obiekty blob platformy Azure)
* Zewnętrzne usługi danych (na przykład zdalna baza danych)

**PYTANIE** Które regiony świadczenia usługi Azure obsługują zestawy skalowania?

**ODPOWIEDŹ** Wszystkie regiony obsługują zestawy skalowania.

**PYTANIE** Jak utworzyć zestaw skalowania za pomocą obrazu niestandardowego?

**ODPOWIEDŹ** Utwórz dysk zarządzany na podstawie wirtualnego dysku twardego z obrazem niestandardowym i odwołaj się do niego w szablonie zestawu skalowania. [Oto przykład](https://github.com/chagarw/MDPP/tree/master/101-vmss-custom-os).

**PYTANIE** Czy można zmniejszyć pojemność Moje skali zestawu z too15 20, które maszyny wirtualne są usuwane?

**ODPOWIEDŹ** Maszyny wirtualne są usuwane z skali hello ustawić równomiernie w domenach update i dostępności toomaximize domen błędów. Maszyny wirtualne z powitalne najwyższy identyfikatory są najpierw usunąć.

**PYTANIE** Co zrobić, jeśli dopiero potem zwiększyć pojemność powitania od 15 too18?

**ODPOWIEDŹ** Jeśli zwiększysz too18 pojemność 3 nowe maszyny wirtualne są tworzone. Zawsze, identyfikator wystąpienia maszyny Wirtualnej hello jest zwiększany z hello poprzedniej najwyższej wartości (na przykład, 20, 21, 22). Maszyny wirtualne są równoważone w domenach błędów i domenach aktualizacji.

**PYTANIE** Czy mogę wymusić sekwencję wykonywania w przypadku korzystania z wielu rozszerzeń w zestawie skalowania?

**ODPOWIEDŹ** Nie bezpośrednio, ale dla rozszerzenia customScript hello skrypt może oczekiwać na inny toofinish rozszerzenia. Możesz uzyskać dodatkowe wskazówki na sekwencjonowanie rozszerzenia w blogu hello [sekwencjonowania rozszerzenia w zestawy skalowania maszyny Wirtualnej Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).

**PYTANIE** Czy zestawy skalowania współdziałają z zestawami dostępności platformy Azure?

**ODPOWIEDŹ** Tak. Zestaw skalowania to niejawny zestaw dostępności z 5 domenami błędów i 5 domenami aktualizacji. Skala zestawy więcej niż 100 maszyn wirtualnych span wielu *umieszczania grupy*, które są równoważne toomultiple zestawów dostępności. Aby uzyskać więcej informacji na temat grup umieszczania, zobacz [Praca z dużymi zestawami skalowania maszyn wirtualnych](virtual-machine-scale-sets-placement-groups.md). Zestaw dostępności maszyn wirtualnych może istnieć w hello sam sieci wirtualnej jako zestaw skalowania maszyn wirtualnych. Typowa konfiguracja jest węzeł kontrolny tooput maszyn wirtualnych (które często wymagają unikatowych konfiguracji) w dostępności ustawić i umieszcza węzły danych w zestawie skalowania hello.

Można znaleźć więcej tooquestions odpowiedzi o skali ustawia w hello [zestawach skali maszyny wirtualnej platformy Azure — często zadawane pytania](virtual-machine-scale-sets-faq.md).
