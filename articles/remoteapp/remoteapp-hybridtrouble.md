---
title: "Tworzenie kolekcji hybrydowej usługi RemoteApp aaaTroubleshoot | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak błędy tworzenia kolekcji tootroubleshoot RemoteApp hybrydowego"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a>Rozwiązywanie problemów związanych z tworzeniem kolekcji hybrydowych Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Kolekcja hybrydowa znajduje się w i przechowuje dane w hello chmury Azure, ale również umożliwia użytkownikom dostęp do danych i zasobów przechowywanych w sieci lokalnej. Użytkownicy mogą uzyskiwać dostęp do aplikacji, logując się przy użyciu poświadczeń firmowych synchronizowanych lub sfederowanych z usługą Azure Active Directory. Można wdrażać kolekcję hybrydową, który korzysta z istniejącej sieci wirtualnej Azure, lub można utworzyć nowej sieci wirtualnej. Zaleca się tworzenia lub za pomocą podsieci sieci wirtualnej wystarczająco duży zakres CIDR oczekiwany przyszły wzrost usługi Azure RemoteApp.

Nie utworzono jeszcze kolekcji? Zobacz [tworzenie kolekcji hybrydowej](remoteapp-create-hybrid-deployment.md) hello czynności.

Jeśli występują problemy podczas tworzenia kolekcji, lub jeśli hello kolekcji nie działa, sposób hello podejrzewasz, że należy, zapoznaj się z następujących informacji hello.

## <a name="your-image-is-invalid"></a>Obraz jest nieprawidłowy
Jeśli zostanie wyświetlony komunikat, takie jak "GoldImageInvalid" podczas oczekiwania dla usługi Azure tooprovision kolekcji, oznacza to, że obraz szablonu nie spełnia wymagań hello [określone wymagania dotyczące obrazu](remoteapp-imagereqs.md). Tak, przejdź do odczytu tych [wymagania](remoteapp-imagereqs.md), Usuń obraz i spróbuj toocreate kolekcji ponownie.

## <a name="does-your-vnet-have-network-security-groups-defined"></a>SIECI wirtualnej ma zdefiniowane grup zabezpieczeń sieci?
Jeśli masz zdefiniowane w podsieci hello używasz kolekcji grup zabezpieczeń sieci, upewnij się, te [adresów URL i portów](remoteapp-ports.md) jest dostępny w obrębie podsieci.

Możesz dodać dodatkowe sieci zabezpieczeń grupy toohello maszyn wirtualnych wdrożonych przez użytkownika w podsieci hello zwiększenie poziomu kontrolki.

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a>Używasz serwery DNS? I są one dostępne z podsieć sieci Wirtualnej?
> [!NOTE]
> Masz toomake powitalne się, że serwery DNS w sieci wirtualnej są zawsze włączone i zawsze możliwe tooresolve maszyn wirtualnych dla hello hostowanych w hello sieci Wirtualnej. Nie należy używać w tym Google DNS.
> 
> 

Dla kolekcji hybrydowych należy używać serwerów DNS. Możesz je określić w schemat konfiguracji sieci lub za pośrednictwem portalu zarządzania powitania po utworzeniu sieci wirtualnej. Serwery DNS używane w kolejności hello, że są one określone w czasie pracy awaryjnej (jak działania okrężnego min. tooround).  
Zobacz zbyt[rozpoznawanie nazwy dla maszyn wirtualnych i wystąpień roli](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake się, że serwery DNS są skonfigurowane correcly.

Upewnij się, że serwery DNS hello kolekcji są dostępne z podsiecią sieci Wirtualnej hello, określone dla tej kolekcji.

Na przykład:

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Zdefiniuj serwery DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a>W kolekcji jest używany kontroler domeny usługi Active Directory?
Obecnie tylko do jednej domeny usługi Active Directory może być skojarzony z usługą Azure RemoteApp. Kolekcja hybrydowa Hello obsługuje tylko konta usługi Azure Active Directory, które zostały zsynchronizowane przy użyciu narzędzia DirSync z wdrożenia usługi Active Directory systemu Windows Server; w szczególności albo zsynchronizowane z opcją synchronizacji haseł hello synchronizowane ze skonfigurowaną Federacją usług federacyjnych Active Directory (AD FS). Należy toocreate domeny niestandardowej, która odpowiada hello sufiks domeny nazwy UPN w domenie lokalnej i konfigurowania integracji katalogu.

Zobacz [Konfigurowanie usługi Active Directory dla usługi Azure RemoteApp](remoteapp-ad.md) Aby uzyskać więcej informacji.

Upewnij się, podane szczegóły domeny hello są prawidłowe i hello kontroler domeny jest dostępny z powitalne maszyny Wirtualnej utworzonej w hello podsieć używana na potrzeby usługi Azure RemoteApp. Upewnij się, że konto usługi hello się, że podane poświadczenia mają uprawnienia tooadd komputery toohello pod warunkiem domeny i że hello nazwa usługi AD, pod warunkiem, mogą zostać rozwiązane z hello DNS podany w hello sieci Wirtualnej.

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a>Jakie nazwy domeny czy określono podczas tworzenia Twojej kolekcji?
Nazwa domeny Hello utworzone lub dodane musi być nazwą domeny wewnętrznej (nie nazwę domeny usługi Azure AD) i musi być w rozpoznawalnym formacie DNS (contoso.local). Na przykład masz wewnętrzna nazwa usługi Active Directory (contoso.local) i Active Directory głównej nazwy użytkownika (contoso.com) - masz toouse hello wewnętrzna nazwa podczas tworzenia Twojej kolekcji.

