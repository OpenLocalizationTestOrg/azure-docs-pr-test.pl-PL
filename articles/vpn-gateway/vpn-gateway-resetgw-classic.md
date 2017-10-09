---
title: "Resetuj tooreestablish bramy sieci VPN platformy Azure tuneli protokołu IPsec | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono zresetowanie Twojego tuneli IPsec tooreestablish bramy sieci VPN platformy Azure. Witaj artykuł dotyczy bram tooVPN w klasycznym hello i modeli wdrażania usługi Resource Manager hello."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a>Resetowanie VPN Gateway

Resetowanie bramy Azure VPN Gateway przydaje się w przypadku utraty połączenia sieci VPN obejmującego wiele lokalizacji w jednym lub wielu tunelach VPN typu lokacja-lokacja. W takiej sytuacji lokalnego urządzenia sieci VPN są wszystkie działa poprawnie, ale są nie jest w stanie tooestablish tuneli protokołu IPsec o hello bram sieci VPN platformy Azure. Ten artykuł pomoże Ci zresetować bramy sieci VPN.

### <a name="what-happens-during-a-reset"></a>Co się dzieje podczas resetowania?

Brama sieci VPN składa się z dwóch wystąpień maszyn wirtualnych działających w konfiguracji aktywnego gotowości. Zresetowanie bramy hello nastąpi ponowne uruchomienie hello bramy, a następnie ponownie stosuje hello między lokalizacjami tooit konfiguracji. Witaj bramy przechowuje hello publicznego adresu IP, który jest już. Oznacza to, że nie trzeba konfiguracji routera tooupdate hello sieci VPN przy użyciu nowego publicznego adresu IP dla bramy sieci VPN platformy Azure.

Podczas generowania hello polecenia tooreset hello bramy natychmiast ponownego hello bieżącego aktywnego wystąpienia hello bramy sieci VPN platformy Azure. Będzie krótką przerwę w trybie failover hello z hello aktywnego wystąpienia (Trwa ponowne uruchamianie), toohello rezerwy wystąpienia. Odstęp Hello powinna być mniej niż minutę.

Jeśli hello połączenie nie zostało odzyskane po ponownym hello, problem sam Witaj ponownie polecenie tooreboot hello drugie wystąpienie maszyny Wirtualnej (hello nowej active bramy). Jeśli ponownego uruchomienia hello żądanego tooback Wstecz, można nieco dłużej gdy trwa ponowne uruchamianie obu wystąpień maszyn wirtualnych (active i wstrzymania). To spowoduje przerwę dłużej hello łączność w sieci VPN zapasowej minut too4 too2 ponowne uruchamianie hello toocomplete maszyn wirtualnych.

Po dwóch uruchamiany ponownie Jeśli nadal występują problemy z łącznością między różnymi lokalizacjami, otwórz żądanie obsługi z hello portalu Azure.

## <a name="before"></a>Przed rozpoczęciem

Zanim je zresetujesz bramy, sprawdź hello kluczowych elementów wymienionych poniżej dla każdego tunelu VPN IPsec lokacja-lokacja (S2S). Wszelkie niezgodność w elementach hello spowoduje rozłączenie hello tunel S2S VPN. Sprawdzanie poprawności i korygowanie hello konfiguracji dla usługi lokalnej i bram sieci VPN platformy Azure pozwala uniknąć niepotrzebnych ponownego uruchomienia i zakłóceń dla hello innych połączeń pracy hello bram.

Sprawdź hello poniższych elementach przed zresetowaniem bramy:

* Hello Internet IP adresów (VIP) dla obu hello bramy sieci VPN platformy Azure i hello lokalnej bramy sieci VPN są poprawnie skonfigurowane w obu hello Azure i hello lokalnej sieci VPN zasad.
* klucz wstępny Hello musi hello w tej samej na bramy sieci VPN platformy Azure, jak i dla lokalnego.
* W przypadku zastosowania określonej konfiguracji protokołu IPsec/IKE, takie jak szyfrowania, mieszania algorytmów i doskonałego utajnienia przekazywania (Perfect Forward Secrecy), upewnij się, zarówno hello Azure i lokalnymi bramy sieci VPN mają hello takie same konfiguracje.

## <a name="portal"></a>Azure portal

Można zresetować bramy VPN Resource Manager przy użyciu hello portalu Azure. Jeśli tooreset klasycznego bramy, zobacz hello [PowerShell](#resetclassic) czynności.

### <a name="resource-manager-deployment-model"></a>Model wdrażania usługi Resource Manager

1. Otwórz hello [portalu Azure](https://portal.azure.com) i przejdź toohello bramy sieci wirtualnej dla Menedżera zasobów, które mają tooreset.
2. W bloku hello hello bramy sieci wirtualnej kliknij pozycję "Resetuj".

  ![Resetuj bloku bramy sieci VPN](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. Na powitania resetowania bloku, kliknij hello **zresetować** przycisku.

## <a name="ps"></a>Środowiska PowerShell

### <a name="resource-manager-deployment-model"></a>Model wdrażania usługi Resource Manager

Witaj polecenia cmdlet Resetowanie bramy jest **AzureRmVirtualNetworkGateway resetowania**. Przed wykonaniem resetowanie, upewnij się, że masz najnowszą wersję hello hello [poleceń cmdlet programu PowerShell Menedżera zasobów](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0). Witaj poniższy przykład powoduje zresetowanie bramy sieci wirtualnej o nazwie VNet1GW w grupie zasobów TestRG1 hello:

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

Wynik:

Po wyświetleniu zwracanych wyników można założyć, resetowanie bramy hello zakończyło się pomyślnie. Jednak nie ma w wyniku zwracany hello, która jawnie wskazuje, że resetowania hello zakończyło się pomyślnie. Jeśli chcesz, aby toolook ściśle na powitania historii toosee dokładnie bramy hello zresetowanie wystąpił, można wyświetlić te informacje w hello [portalu Azure](https://portal.azure.com). W portalu hello Przejdź zbyt**"GatewayName" -> kondycja zasobów**.

### <a name="resetclassic"></a>Klasycznego modelu wdrażania

Witaj polecenia cmdlet Resetowanie bramy jest **AzureVNetGateway resetowania**. Przed wykonaniem resetowanie, upewnij się, że masz najnowszą wersję hello hello [poleceń cmdlet programu PowerShell usługi zarządzania (SM)](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0). Witaj poniższy przykład resetuje hello bramy sieci wirtualnej o nazwie "ContosoVNet":

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

Wynik:

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <a name="cli"></a>Interfejs wiersza polecenia platformy Azure

tooreset hello bramy, użyj hello [zresetować bramy sieci wirtualnej sieci az](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) polecenia. Witaj poniższy przykład powoduje zresetowanie bramy sieci wirtualnej o nazwie VNet5GW w grupie zasobów TestRG5 hello:

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

Wynik:

Po wyświetleniu zwracanych wyników można założyć, resetowanie bramy hello zakończyło się pomyślnie. Jednak nie ma w wyniku zwracany hello, która jawnie wskazuje, że resetowania hello zakończyło się pomyślnie. Jeśli chcesz, aby toolook ściśle na powitania historii toosee dokładnie bramy hello zresetowanie wystąpił, można wyświetlić te informacje w hello [portalu Azure](https://portal.azure.com). W portalu hello Przejdź zbyt**"GatewayName" -> kondycja zasobów**.
