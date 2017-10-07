---
title: "aaaCannot usunąć sieci wirtualnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootroubleshoot hello problem, w której nie można usunąć sieci wirtualnej na platformie Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a>Rozwiązywanie problemów: Nie powiodło się toodelete sieci wirtualnej na platformie Azure

Błędy może pojawić się podczas próby toodelete sieci wirtualnej na platformie Microsoft Azure. Ten artykuł zawiera toohelp kroki rozwiązywania problemów możesz rozwiązać ten problem. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a>Wskazówki dotyczące rozwiązywania problemów 

1. [Sprawdź, czy brama sieci wirtualnej jest uruchomiony w sieci wirtualnej hello](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).
2. [Sprawdź, czy bramę aplikacji jest uruchomiony w sieci wirtualnej hello](#check-whether-an-application-gateway-is-running-in-the-virtual-network).
3. [Sprawdź, czy usługi Azure Active Directory domeny jest włączone w sieci wirtualnej hello](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).
4. [Sprawdź, czy sieć wirtualna hello zasobów połączonych tooother](#check-whether-the-virtual-network-is-connected-to-other-resource).
5. [Sprawdź, czy maszyna wirtualna nadal działa w sieci wirtualnej hello](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).
6. [Sprawdź, czy sieć wirtualna hello utkwiła w automatycznej migracji](#check-whether-the-virtual-network-is-stuck-in-migration).

## <a name="troubleshooting-steps"></a>Kroki rozwiązywania problemów

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a>Sprawdź, czy brama sieci wirtualnej jest uruchomiony w sieci wirtualnej hello

tooremove hello sieci wirtualnej, należy najpierw usunąć hello bramy sieci wirtualnej.

Dla klasycznych sieci wirtualnych, przejdź toohello **omówienie** strony hello klasycznej sieci wirtualnej w hello portalu Azure. W hello **połączeń sieci VPN** sekcji, jeśli hello brama jest uruchomiona w sieci wirtualnej hello, zobaczysz hello IP adres bramy hello. 

![Sprawdź, czy brama jest uruchomiona](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

Dla sieci wirtualnych, przejdź toohello **omówienie** strony hello sieci wirtualnej. Sprawdź **urządzeń podłączonych** hello bramy sieci wirtualnej.

![Sprawdź hello podłączonym urządzeniu](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

Zanim będzie można usunąć bramy hello, najpierw usuń wszystkie **połączenia** obiektów w hello bramy. 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a>Sprawdź, czy w sieci wirtualnej hello działa bramy aplikacji

Przejdź toohello **omówienie** strony hello sieci wirtualnej. Sprawdź hello **urządzeń podłączonych** hello bramy aplikacji.

![Sprawdź hello podłączonym urządzeniu](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

W przypadku bramy aplikacji, należy usunąć przed usunięciem hello sieci wirtualnej.

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a>Sprawdź, czy w sieci wirtualnej hello jest włączone usług domenowych Azure Active Directory

Jeśli hello usług domenowych w usłudze Active Directory jest włączone i połączone toohello sieci wirtualnej, nie można usunąć tej sieci wirtualnej. 

![Sprawdź hello podłączonym urządzeniu](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

toodisable hello usługi, wykonaj następujące kroki:

1. Przejdź toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Wybierz w okienku po lewej stronie powitania **usługi Active Directory**.
3. Wybierz katalog usługi Azure Active Directory (Azure AD) hello, który ma usług domenowych Active Directory włączone.
4. Wybierz hello **Konfiguruj** kartę.
5. W obszarze **usług domenowych w usłudze**, zmień hello **włączyć usługi domenowe dla tego katalogu** opcję zbyt**nr**.  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a>Sprawdź, czy sieć wirtualna hello tooother połączonych zasobów

Sprawdź, czy łącza obwód, połączeń i komunikacji równorzędnych sieci wirtualnych. Żadnego z nich może spowodować toofail usunięcia sieci wirtualnej. 

Witaj kolejność usuwania zalecana jest następująca:

1. Połączenia bramy
2. Bramy
3. Adresy IP
4. Komunikacji równorzędnych sieci wirtualnych
5. Środowisko usługi aplikacji (ASE)

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a>Sprawdź, czy maszyna wirtualna nadal działa w sieci wirtualnej hello

Upewnij się, nieprawidłowość w sieci wirtualnej hello żadnej maszyny wirtualnej.

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a>Sprawdź, czy sieć wirtualna hello utkwiła w automatycznej migracji

Jeśli w sieci wirtualnej hello jest zablokowana w stanie migracji, nie można usunąć. Uruchom następujące polecenia tooabort hello migracji hello, a następnie usuń hello sieci wirtualnej.

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a>Następne kroki

- [Azure Virtual Network](virtual-networks-overview.md)
- [Często zadawane pytania dotyczące sieci wirtualnych platformy Azure](virtual-networks-faq.md)