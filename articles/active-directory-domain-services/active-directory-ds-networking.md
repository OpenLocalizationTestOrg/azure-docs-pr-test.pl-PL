---
title: "Usługi domenowe Azure AD: Wskazówki dotyczące sieci | Dokumentacja firmy Microsoft"
description: "Zagadnienia dotyczące sieci dla usług domenowych Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 23a857a5-2720-400a-ab9b-1ba61e7b145a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: maheshu
ms.openlocfilehash: 804d4ea7d1b3b07b6d224855c7adb90bdfe24022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-azure-ad-domain-services"></a>Zagadnienia dotyczące sieci dla usług domenowych Azure AD
## <a name="how-tooselect-an-azure-virtual-network"></a>Jak tooselect sieci wirtualnej platformy Azure
Witaj poniższe wskazówki ułatwiają wybierz toouse sieci wirtualnej, z usług domenowych Azure AD.

### <a name="type-of-azure-virtual-network"></a>Typ sieci wirtualnej platformy Azure
* Można włączyć usługi domenowe Azure AD w klasycznej sieci wirtualnej platformy Azure.
* Usługi domenowe Azure AD **nie można włączyć w sieciach wirtualnych utworzonych przy użyciu usługi Azure Resource Manager**.
* Możesz połączyć sieci wirtualnej na podstawie Menedżera zasobów tooa klasycznej sieci wirtualnej w której włączono usługi domenowe Azure AD. Następnie można użyć usług domenowych Azure AD w sieciach wirtualnych opartych na Menedżera zasobów hello. Aby uzyskać więcej informacji, zobacz hello [połączeń sieciowych](active-directory-ds-networking.md#network-connectivity) sekcji.
* **Regionalne wirtualne sieci**: Jeśli planujesz toouse istniejącej sieci wirtualnej, upewnij się, że jest regionalną sieć wirtualną.

  * Sieci wirtualne, które używają hello starszego mechanizmu grup koligacji nie można używać z usług domenowych Azure AD.
  * Usługi domenowe Azure AD toouse [migracja starszych sieci wirtualnych tooregional wirtualnych sieci](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).

### <a name="azure-region-for-hello-virtual-network"></a>Region platformy Azure dla sieci wirtualnej hello
* Usługi domenowe Azure AD domeny zarządzanej zostało wdrożone w hello tego samego regionu Azure co sieć wirtualna hello wybrane usługi hello tooenable w.
* Wybierz sieć wirtualną w regionie platformy Azure obsługiwane przez usługi domenowe Azure AD.
* Zobacz hello [usług Azure według regionu](https://azure.microsoft.com/regions/#services/) tooknow strony hello regiony platformy Azure, w których są dostępne usługi domenowe Azure AD.

### <a name="requirements-for-hello-virtual-network"></a>Wymagania dotyczące hello sieci wirtualnej
* **Zbliżeniowe tooyour Azure obciążeń**: Wybierz hello sieci wirtualnej, która obecnie hostuje/będzie hostować maszyny wirtualne, które należy uzyskać dostępu do usług domenowych w usłudze tooAzure AD.
* **Niestandardowe/bring your own serwerów DNS**: Sprawdź, czy żadnych niestandardowych serwerów DNS, które są skonfigurowane dla hello sieci wirtualnej.
* **Domen z hello tą samą nazwą domeny**: Upewnij się, że nie masz istniejącej domeny hello tej samej nazwy domeny jest dostępny w tej sieci wirtualnej. Na przykład załóżmy, że masz domenę o nazwie "contoso.com" już dostępną na powitania wybranej sieci wirtualnej. Później, spróbuj tooenable domeny zarządzanej usług domenowych Azure AD z hello tej samej nazwy domeny ("contoso.com") w tej sieci wirtualnej. Podczas próby usług domenowych w usłudze Azure AD tooenable wystąpi awaria. Ten błąd jest powodu konfliktów tooname hello nazwy domeny w sieci wirtualnej. W takiej sytuacji należy użyć tooset inną nazwę zapasowej domeny zarządzanej usług domenowych Azure AD. Alternatywnie można anulować aprowizację istniejącej domeny hello, a następnie przejdź usług domenowych w usłudze tooenable usługi Azure AD.

> [!WARNING]
> Nie można przenieść usług domenowych w usłudze tooa innej sieci wirtualnej, po włączeniu usługi hello.
>
>

## <a name="network-security-groups-and-subnet-design"></a>Grupy zabezpieczeń sieci i podsieci
A [grupy zabezpieczeń sieci (NSG)](../virtual-network/virtual-networks-nsg.md) zawiera listę reguł listy kontroli dostępu (ACL), które akceptować lub odrzucać ruch sieciowy tooyour wystąpień maszyn wirtualnych w sieci wirtualnej. Grupy NSG można kojarzyć z podsieciami lub poszczególnymi wystąpieniami maszyn wirtualnych w danej podsieci. Gdy grupa NSG jest skojarzona z podsiecią, reguły listy ACL hello zastosować wystąpień maszyn wirtualnych hello tooall w tej podsieci. Ponadto ruch tooan poszczególnych maszyn wirtualnych można ograniczyć jeszcze bardziej przez skojarzenie grupy NSG bezpośrednio toothat maszyny Wirtualnej.

![Zalecane podsieci](./media/active-directory-domain-services-design-guide/vnet-subnet-design.png)

### <a name="best-practices-for-choosing-a-subnet"></a>Najlepsze rozwiązania dotyczące wybierania podsieci
* Wdrażanie usług domenowych Azure AD tooa **oddzielnych dedykowanych podsieci** w ramach sieci wirtualnej platformy Azure.
* Nie należy stosować grupy NSG podsieci toohello dedykowane dla domeny zarządzanej. Jeśli musisz zastosować grupy NSG podsieci toohello w wersji dedykowanej, upewnij się, możesz **nie blokuj tooservice wymagane porty hello i zarządzanie nimi domenę**.
* Nie ograniczaj zbyt hello liczba adresów IP dostępne w ramach podsieci hello dedykowane dla domeny zarządzanej. Tego ograniczenia zapobiega hello usługi Udostępnianie dwa kontrolery domeny do domeny zarządzanej.
* **Nie należy włączać usługi domenowe Azure AD w podsieci bramy hello** z sieci wirtualnej.

> [!WARNING]
> Po skojarzeniu grupy NSG z podsiecią, w którym usługi domenowe Azure AD jest włączona, może zakłócać tooservice możliwości firmy Microsoft i zarządzanie nimi hello domeny. Ponadto synchronizacja dzierżawy usługi Azure AD i domeny zarządzanej jest zakłócona. **Hello SLA nie obejmuje toodeployments gdzie grupy NSG zastosowano blokujący usług domenowych Azure AD z aktualizacji i Zarządzanie domeną.**
>
>

### <a name="ports-required-for-azure-ad-domain-services"></a>Porty wymagane przez usługi domenowe Azure AD
Witaj następujące porty są wymagane dla tooservice usługi domenowe Azure AD i obsługa domeny zarządzanej. Upewnij się, że te porty nie są blokowane dla podsieci hello, w którym włączono domeny zarządzanej.

| Numer portu | Przeznaczenie |
| --- | --- |
| 443 |Synchronizacja z dzierżawy usługi Azure AD |
| 3389 |Zarządzanie domeny |
| 5986 |Zarządzanie domeny |
| 636 |Bezpiecznego protokołu LDAP (LDAPS) dostępu tooyour domeny zarządzanej |

### <a name="sample-nsg-for-virtual-networks-with-azure-ad-domain-services"></a>Przykład grupy NSG dla sieci wirtualnych z usług domenowych Azure AD
Witaj w poniższej tabeli przedstawiono przykład grupy NSG można skonfigurować sieć wirtualną z domeny zarządzanej usług domenowych Azure AD. Ta zasada umożliwia ruch przychodzący z hello powyżej tooensure określonych portów domeny zarządzanej pozostaje poprawkami, aktualizacji i mogą być monitorowane przez firmę Microsoft. Hello domyślne "DenyAll" reguła ma zastosowanie tooall pozostały przychodzący ruch z hello internet.

Ponadto hello NSG także przedstawiono sposób toolock dół bezpiecznego dostępu LDAP za pośrednictwem hello internet. Pomiń tę regułę, jeśli nie włączono bezpiecznego LDAP dostępu tooyour domeny zarządzanej za pośrednictwem hello internet. Hello NSG zawiera zestaw reguł, które zezwolić na przychodzący LDAPS dostęp za pośrednictwem portu TCP 636 tylko z określonego zestawu adresów IP. Witaj NSG reguły tooallow LDAPS dostęp za pośrednictwem hello internet z określonych adresów IP ma wyższy priorytet niż hello reguły DenyAll NSG.

![Przykład grupy NSG toosecure LDAPS dostęp za pośrednictwem hello internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Więcej informacji** - [Utwórz grupę zabezpieczeń sieci](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).


## <a name="network-connectivity"></a>Połączenie sieciowe
Domeny zarządzanej usług domenowych Azure AD można włączyć tylko w obrębie jednego klasycznej sieci wirtualnej na platformie Azure. Sieci wirtualne utworzone za pomocą usługi Azure Resource Manager nie są obsługiwane.

### <a name="scenarios-for-connecting-azure-networks"></a>Scenariusze dotyczące łączenia sieci platformy Azure
Połącz domeny zarządzanej hello toouse sieci wirtualnych platformy Azure w żadnym hello następujące scenariusze wdrażania:

#### <a name="use-hello-managed-domain-in-more-than-one-azure-classic-virtual-network"></a>Użyj hello zarządzane domeny w więcej niż jeden klasycznej sieci wirtualnej platformy Azure
Możesz połączyć inne toohello Azure klasycznych sieci wirtualnych Azure klasycznej sieci wirtualnej, w której włączono usługi domenowe Azure AD. To połączenie VPN umożliwia domeny zarządzanej hello toouse z obciążeń wdrożonych w innych sieciach wirtualnych.

![Łączność klasycznej sieci wirtualnej](./media/active-directory-domain-services-design-guide/classic-vnet-connectivity.png)

#### <a name="use-hello-managed-domain-in-a-resource-manager-based-virtual-network"></a>Użyj hello domeny zarządzanej w sieci wirtualnej Resource Manager
Możesz połączyć toohello sieciach wirtualnych opartych na protokole Menedżera zasobów Azure klasycznej sieci wirtualnej, w której włączono usługi domenowe Azure AD. To połączenie umożliwia domeny zarządzanej hello toouse z obciążeń wdrożonych w sieciach wirtualnych opartych na Menedżera zasobów hello.

![Połączenie wirtualnej sieci tooclassic Menedżera zasobów](./media/active-directory-domain-services-design-guide/classic-arm-vnet-connectivity.png)

### <a name="network-connection-options"></a>Opcje połączeń sieciowych
* **Wirtualnymi do połączeń przy użyciu połączeń VPN lokacja lokacja**: połączenie sieci wirtualnej tooanother sieci wirtualnej (aby wirtualnymi) to podobne tooconnecting lokalizacji sieci wirtualnej tooan lokalnej lokacji. Oba typy łączności Użyj tooprovide bramy sieci VPN przy użyciu protokołu IPsec/IKE bezpiecznego tunelu.

    ![Łączność sieci wirtualnej przy użyciu bramy sieci VPN](./media/active-directory-domain-services-design-guide/vnet-connection-vpn-gateway.jpg)

    [Więcej informacji - połączyć sieci wirtualnych za pomocą bramy sieci VPN](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* **Aby wirtualnymi połączenia wirtualnej sieci komunikacji równorzędnej**: sieci wirtualnej komunikacji równorzędnej jest mechanizm, który łączy dwie sieci wirtualne w hello tego samego regionu hello Azure szkieletu sieci. Po połączyć za pomocą, Witaj dwie sieci wirtualne są wyświetlane jako jeden dla wszystkich celów łączności. Są one nadal zarządzane jako oddzielne zasoby, ale maszyny wirtualne w tych sieciach wirtualnych mogą komunikować się bezpośrednio przy użyciu prywatnych adresów IP.

    ![Łączność sieci wirtualnej za pomocą komunikacji równorzędnej](./media/active-directory-domain-services-design-guide/vnet-peering.png)

    [Więcej informacji - wirtualnych sieci komunikacji równorzędnej](../virtual-network/virtual-network-peering-overview.md)

<br>

## <a name="related-content"></a>Powiązana zawartość
* [Komunikacja równorzędna sieci wirtualnej platformy Azure](../virtual-network/virtual-network-peering-overview.md)
* [Konfigurowanie połączenia do wirtualnymi hello klasycznego modelu wdrażania](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* [Grupy zabezpieczeń sieci platformy Azure](../virtual-network/virtual-networks-nsg.md)
* [Utwórz grupę zabezpieczeń sieci](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
