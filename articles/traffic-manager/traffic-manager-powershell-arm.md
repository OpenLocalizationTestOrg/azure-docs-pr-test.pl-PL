---
title: "aaaUsing toomanage programu PowerShell Menedżera ruchu na platformie Azure | Dokumentacja firmy Microsoft"
description: "Przy użyciu programu PowerShell dla Menedżera ruchu z usługi Azure Resource Manager"
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a>Przy użyciu programu PowerShell toomanage Menedżera ruchu

Usługa Azure Resource Manager to hello preferowane interfejs dla usług Azure. Azure profilów usługi Traffic Manager mogą być zarządzane przy użyciu usługi Azure Resource Manager na podstawie interfejsów API i narzędzia.

## <a name="resource-model"></a>Model zasobów

Menedżer ruchu Azure jest konfigurowane przy użyciu kolekcję ustawień o nazwie profilu usługi Traffic Manager. Ten profil zawiera ustawienia DNS, ustawienia kierowania ruchu, ustawienia monitorowania punktu końcowego, a jest kierowany listę ruch toowhich punktów końcowych usługi.

Każdy profil Menedżera ruchu jest reprezentowana przez zasób typu "TrafficManagerProfiles". Na powitania poziom interfejsu API REST hello identyfikatora URI dla każdego profilu jest następujący:

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a>Konfigurowanie programu Azure PowerShell

Poniższe instrukcje korzystają z programu Microsoft Azure PowerShell. Witaj artykule wyjaśniono, jak tooinstall i konfigurowanie programu Azure PowerShell.

* [Jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview)

Hello przykłady w tym artykule założono, że masz istniejącą grupę zasobów. Można utworzyć grupy zasobów przy użyciu hello następujące polecenie:

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów miały miejsce. Ta lokalizacja jest używana jako domyślna hello zasoby utworzone w tej grupie zasobów. Jednak ponieważ zasoby profilu Menedżera ruchu są globalne, a nie regionalne, hello wybór lokalizacji grupy zasobów nie ma wpływu na usługi Azure Traffic Manager.

## <a name="create-a-traffic-manager-profile"></a>Tworzenie profilu Menedżera ruchu

toocreate profilu usługi Traffic Manager, użyj hello `New-AzureRmTrafficManagerProfile` polecenia cmdlet:

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

Witaj w poniższej tabeli opisano parametry hello:

| Parametr | Opis |
| --- | --- |
| Nazwa |Nazwa zasobu Hello hello zasobów profilu Menedżera ruchu. Profile w hello sama grupa zasobów muszą mieć unikatowe nazwy. Ta nazwa jest oddzielony od hello DNS nazwę używaną dla zapytań DNS. |
| Grupy zasobów o nazwie |Nazwa Hello hello zasobu zawierającego hello profilu zasób grupy. |
| TrafficRoutingMethod |Określa hello routingu ruchu metodę toodetermine który punkt końcowy jest zwracany w odpowiedzi do zapytania DNS. Możliwe wartości to "Performance", 'Ważone' lub 'Priority'. |
| RelativeDnsName |Określa hello hostname część nazwy DNS hello udostępniane przez ten profil Menedżera ruchu. Ta wartość jest połączona z nazwą domeny DNS hello używane przez usługi Azure Traffic Manager tooform hello pełni kwalifikowaną nazwę domeny (FQDN) hello profilu. Na przykład ustawienie wartości hello "contoso" staje się "contoso.trafficmanager.net." |
| CZAS WYGAŚNIĘCIA |Witaj DNS Time-to-Live (TTL) określa w sekundach. Ten czas wygaśnięcia informuje rozpoznawania nazw DNS lokalne powitania i klientów DNS, jak długo toocache odpowiedzi DNS dla tego profilu usługi Traffic Manager. |
| MonitorProtocol |Określa hello protokołu toouse toomonitor punktu końcowego kondycji. Możliwe wartości to "HTTP" i "HTTPS". |
| MonitorPort |Określa, że hello TCP port używany toomonitor kondycji punktu końcowego. |
| MonitorPath |Określa, że nazwa domeny hello ścieżki względnej toohello punktu końcowego używane tooprobe kondycji punktu końcowego. |

polecenia cmdlet Hello tworzy profil Menedżera ruchu na platformie Azure i zwraca odpowiednie tooPowerShell obiektu profilu. W tym momencie hello profil zastępczy nie zawiera żadnych punktów końcowych. Aby uzyskać więcej informacji na temat dodawania profilu usługi Traffic Manager tooa punktów końcowych, zobacz [Dodawanie punktów końcowych usługi Traffic Manager](#adding-traffic-manager-endpoints).

## <a name="get-a-traffic-manager-profile"></a>Pobierz profil Menedżera ruchu

tooretrieve istniejącego obiektu profilu usługi Traffic Manager, użyj hello `Get-AzureRmTrafficManagerProfle` polecenia cmdlet:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

To polecenie cmdlet zwraca obiekt profilu Menedżera ruchu.

## <a name="update-a-traffic-manager-profile"></a>Zaktualizuj profil Menedżera ruchu

Modyfikowanie profilów usługi Traffic Manager następujący proces krok 3:

1. Przy użyciu profilu hello pobrać `Get-AzureRmTrafficManagerProfile` lub Użyj profilu hello zwrócony przez `New-AzureRmTrafficManagerProfile`.
2. Modyfikowanie hello profilu. Można dodać i usunąć punkty końcowe lub zmień parametry punktu końcowego lub profil. Te zmiany są operacji w trybie offline. Zmieniasz hello lokalnego obiektu w pamięci, która reprezentuje hello profilu.
3. Zatwierdź zmiany przy użyciu hello `Set-AzureRmTrafficManagerProfile` polecenia cmdlet.

Wszystkie właściwości profilu można zmienić z wyjątkiem RelativeDnsName hello profilu. toochange hello RelativeDnsName, należy usunąć profil i nowy profil z nową nazwą.

Witaj poniższy przykład pokazuje, jak toochange hello TTL profilu:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Istnieją trzy typy punktów końcowych usługi Traffic Manager:

1. **Punkty końcowe systemu Azure** są usługi hostowanej na platformie Azure
2. **Zewnętrzne punkty końcowe** usług hostowanych poza platformą Azure
3. **Zagnieżdżone punkty końcowe** są używane tooconstruct zagnieżdżone hierarchie profilów usługi Traffic Manager. Punkty końcowe zagnieżdżonych Włącz zaawansowane konfiguracje routingu ruchu w kontekście aplikacji złożonych.

We wszystkich przypadkach trzy punkty końcowe mogą być dodawane na dwa sposoby:

1. Przy użyciu kroku 3 procedury opisane wcześniej. Hello zaletą tej metody jest, że wiele zmian punktu końcowego można podjąć w pojedynczej aktualizacji.
2. Za pomocą polecenia cmdlet New-AzureRmTrafficManagerEndpoint hello. To polecenie cmdlet dodaje istniejący profil usługi Traffic Manager punktu końcowego tooan w ramach jednej operacji.

## <a name="adding-azure-endpoints"></a>Dodawanie punkty końcowe systemu Azure

Punkty końcowe systemu Azure odwoływać się do usług hostowanych na platformie Azure. Obsługiwane są dwa typy punkty końcowe systemu Azure:

1. Azure Web Apps
2. Azure zasoby publicznego adresu IP (które może być dołączone tooa modułu równoważenia obciążenia lub maszyny wirtualnej karty Sieciowej). Witaj publicznego adresu IP musi mieć nazwę DNS przypisane toobe używane w usłudze Traffic Manager.

W każdym przypadku:

* Usługa Hello jest określona za pomocą parametru "element targetResourceId" hello `Add-AzureRmTrafficManagerEndpointConfig` lub `New-AzureRmTrafficManagerEndpoint`.
* Witaj "Target" i "EndpointLocation" są implikowana przez element TargetResourceId hello.
* Określenie hello "Waga" jest opcjonalne. Wagi są używane tylko w przypadku profilu hello skonfigurowanego toouse metody routingu ruchu "Ważone" hello. W przeciwnym razie są ignorowane. Jeśli jest określony, wartość hello musi być liczbą z zakresu od 1 do 1000. Witaj, wartością domyślną jest "1".
* Określanie hello 'Priority' jest opcjonalna. Priorytety są używane, jeśli profil hello jest skonfigurowany toouse hello 'Priority' metody routingu ruchu. W przeciwnym razie są ignorowane. Prawidłowe wartości to od 1 too1000 o niższych wartościach, wskazując wyższy priorytet. Jeśli określone dla punktów końcowych, musi być określona dla wszystkich punktów końcowych. Pominięcie wartości domyślne, zaczynając od "1" są stosowane w kolejności hello wymieniony hello punktów końcowych.

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a>Przykład 1: Dodawanie punktów końcowych aplikacji sieci Web przy użyciu`Add-AzureRmTrafficManagerEndpointConfig`

W tym przykładzie, możemy utworzyć profil Menedżera ruchu i dodaj dwa punkty końcowe aplikacji sieci Web, przy użyciu hello `Add-AzureRmTrafficManagerEndpointConfig` polecenia cmdlet.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a>Przykład 2: Dodawanie punktu końcowego publicznego adresu IP za pomocą`New-AzureRmTrafficManagerEndpoint`

W tym przykładzie zasób publiczny adres IP jest dodany toohello profilu usługi Traffic Manager. Hello publiczny adres IP musi mieć nazwę DNS skonfigurowane i może być powiązany albo toohello karty Sieciowej maszyny Wirtualnej lub tooa usługi równoważenia obciążenia.

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a>Dodawanie zewnętrzne punkty końcowe

Traffic Manager używa zewnętrzne punkty końcowe toodirect ruchu tooservices hostowanej poza platformą Azure. Zgodnie z punkty końcowe systemu Azure, zewnętrzne punkty końcowe można dodać albo przy użyciu `Add-AzureRmTrafficManagerEndpointConfig` następuje `Set-AzureRmTrafficManagerProfile`, lub `New-AzureRMTrafficManagerEndpoint`.

Podczas określania zewnętrzne punkty końcowe:

* należy podać nazwę domeny punktu końcowego Hello za pomocą parametru 'Target' hello
* Użycie hello metody routingu ruchu "Performance" hello "EndpointLocation" jest wymagana. W przeciwnym razie jest opcjonalne. Witaj, wartość musi być [Nazwa Nieprawidłowa regionu Azure](https://azure.microsoft.com/regions/).
* Witaj, 'Wagi' i 'Priority' są opcjonalne.

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Przykład 1: Dodawanie zewnętrzne punkty końcowe przy użyciu `Add-AzureRmTrafficManagerEndpointConfig` i`Set-AzureRmTrafficManagerProfile`

W tym przykładzie możemy utworzyć profil Menedżera ruchu, dodaj dwa zewnętrzne punkty końcowe i zatwierdź zmiany hello.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Przykład 2: Dodawanie zewnętrzne punkty końcowe przy użyciu`New-AzureRmTrafficManagerEndpoint`

W tym przykładzie dodamy istniejący profil tooan zewnętrznego punktu końcowego. Profil Hello jest określona za pomocą nazwy grupy hello profilu i zasobów.

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a>Dodawanie punktów końcowych 'Nested'

Każdy profil usługi Traffic Manager określa pojedynczej metody routingu ruchu. Istnieją jednak scenariusze, które wymagają bardziej złożone routingu ruchu niż hello routingu udostępniane przez jeden profil Menedżera ruchu. Można zagnieżdżać Traffic Manager profile toocombine hello korzyści z więcej niż jedna metoda routingu ruchu. Zagnieżdżonych profilów pozwalają toooverride hello domyślnego menedżera ruchu zachowanie toosupport większych i bardziej złożone wdrożenia aplikacji. Aby uzyskać bardziej szczegółowe przykłady, zobacz [profilów usługi Traffic Manager zagnieżdżone](traffic-manager-nested-profiles.md).

Zagnieżdżone punkty końcowe zostały skonfigurowane w profilu nadrzędnego hello, przy użyciu typu określonego punktu końcowego "NestedEndpoints". Podczas określania zagnieżdżonych punktów końcowych:

* Witaj punktu końcowego musi być określona za pomocą parametru "element targetResourceId" hello
* Użycie hello metody routingu ruchu "Performance" hello "EndpointLocation" jest wymagana. W przeciwnym razie jest opcjonalne. Witaj, wartość musi być [Nazwa Nieprawidłowa regionu Azure](http://azure.microsoft.com/regions/).
* Witaj, 'Wagi' i 'Priority' są opcjonalne, jak w przypadku punkty końcowe systemu Azure.
* Parametr "MinChildEndpoints" Hello jest opcjonalny. Witaj, wartością domyślną jest "1". Jeśli hello liczba dostępnych punktów końcowych spada poniżej tej wartości progowej, profilu nadrzędnego hello uwzględnia hello podrzędne profil "niższa" i odwracają toohello ruchu z innych punktów końcowych w profilu nadrzędnego hello.

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Przykład 1: Dodawanie zagnieżdżonych punktów końcowych przy użyciu `Add-AzureRmTrafficManagerEndpointConfig` i`Set-AzureRmTrafficManagerProfile`

W tym przykładzie firma Microsoft Tworzenie nowej usługi Traffic Manager nadrzędnym a podrzędnym profilów, Dodaj obiekt podrzędny hello jako element nadrzędny toohello zagnieżdżonych punktu końcowego i zatwierdź zmiany hello.

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Jednak w tym przykładzie firma Microsoft nie dodano żadnych innych punktów końcowych toohello podrzędnej lub nadrzędnej profilów.

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Przykład 2: Dodawanie zagnieżdżonych punktów końcowych przy użyciu`New-AzureRmTrafficManagerEndpoint`

W tym przykładzie dodamy istniejący profil podrzędnych jako zagnieżdżony punktu końcowego tooan istniejącego nadrzędnego profil. Profil Hello jest określona za pomocą nazwy grupy hello profilu i zasobów.

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a>Aktualizowanie punktu końcowego Menedżera ruchu

Istnieją dwa sposoby tooupdate istniejący punkt końcowy Menedżera ruchu:

1. Przy użyciu profilu Menedżera ruchu hello `Get-AzureRmTrafficManagerProfile`, zaktualizować właściwości punktu końcowego hello w profilu hello i zatwierdzić zmiany hello przy użyciu `Set-AzureRmTrafficManagerProfile`. Ta metoda ma zaletą hello jest możliwe tooupdate więcej niż jeden punkt końcowy w ramach jednej operacji.
2. Przy użyciu punktu końcowego Menedżera ruchu hello `Get-AzureRmTrafficManagerEndpoint`, zaktualizować właściwości punktu końcowego hello i zatwierdzić zmiany hello przy użyciu `Set-AzureRmTrafficManagerEndpoint`. Ta metoda jest prostsza, ponieważ nie jest wymagane, przeprowadzane jest indeksowanie do tablicy punkty końcowe hello hello profilu.

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a>Przykład 1: Aktualizowanie punktów końcowych przy użyciu `Get-AzureRmTrafficManagerProfile` i`Set-AzureRmTrafficManagerProfile`

W tym przykładzie mamy zmodyfikować priorytet hello na dwa punkty końcowe w ramach istniejącego profilu.

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a>Przykład 2: Aktualizowanie punktu końcowego za pomocą `Get-AzureRmTrafficManagerEndpoint` i`Set-AzureRmTrafficManagerEndpoint`

W tym przykładzie mamy zmodyfikować hello wagę jeden punkt końcowy w istniejącego profilu.

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a>Włączanie i wyłączanie punktów końcowych i profili

Menedżer ruchu umożliwia toobe poszczególne punkty końcowe włączone i wyłączone, oraz umożliwiając Włączanie i wyłączanie całego profilów.
Tych zmian przez hello pobierania/aktualizowania/ustawienia punktu końcowego lub profilu zasobów. toostreamline tych typowych operacji są również obsługiwane za pośrednictwem dedykowanej polecenia cmdlet.

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a>Przykład 1: Włączanie i wyłączanie profilu Menedżera ruchu

Użyj tooenable profil Menedżera ruchu `Enable-AzureRmTrafficManagerProfile`. Profil Hello można określić za pomocą obiektu profilu. Witaj obiektu profilu mogą zostać przekazane za pośrednictwem potoku hello lub za pomocą hello "-TrafficManagerProfile" parametru. W tym przykładzie określono profil hello hello nazwę grupy profilu i zasobów.

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

toodisable profilu usługi Traffic Manager:

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

polecenie cmdlet Disable-AzureRmTrafficManagerProfile Hello monituje o potwierdzenie. Ten monit można pomijać przy użyciu hello '-Force "parametru.

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a>Przykład 2: Włączanie i wyłączanie punktu końcowego Menedżera ruchu

Użyj tooenable punktu końcowego Menedżera ruchu `Enable-AzureRmTrafficManagerEndpoint`. Istnieją dwa sposoby toospecify hello punktu końcowego

1. Przy użyciu obiektu TrafficManagerEndpoint przekazywane za pośrednictwem potoku hello lub hello "-TrafficManagerEndpoint" parametru
2. Przy użyciu hello Nazwa punktu końcowego, typ punktu końcowego, nazwa profilu i nazwa grupy zasobów:

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Podobnie toodisable punktu końcowego Menedżera ruchu:

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

Jak `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` polecenie cmdlet monituje o potwierdzenie. Ten monit można pomijać przy użyciu hello '-Force "parametru.

## <a name="delete-a-traffic-manager-endpoint"></a>Usuwanie punktu końcowego Menedżera ruchu

poszczególne punkty końcowe tooremove, użyj hello `Remove-AzureRmTrafficManagerEndpoint` polecenia cmdlet:

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

To polecenie cmdlet wyświetli monit o potwierdzenie. Ten monit można pomijać przy użyciu hello '-Force "parametru.

## <a name="delete-a-traffic-manager-profile"></a>Usuwanie profilu Menedżera ruchu

toodelete profilu usługi Traffic Manager, użyj hello `Remove-AzureRmTrafficManagerProfile` polecenia cmdlet, określenie nazwy hello profilu oraz zasobów grupy:

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

To polecenie cmdlet wyświetli monit o potwierdzenie. Ten monit można pomijać przy użyciu hello '-Force "parametru.

usunięte toobe profilu Hello można również określić za pomocą obiektu profilu:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

Ta sekwencja również mogą być przekazywane w potoku:

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a>Następne kroki

[Monitorowanie Menedżera ruchu](traffic-manager-monitoring.md)

[Zagadnienia dotyczące wydajności usługi Traffic Manager](traffic-manager-performance-considerations.md)
