---
title: "Jakiego rodzaju kolekcji potrzebujesz w usłudze Azure RemoteApp? | Microsoft Docs"
description: "Więcej informacji na temat typów kolekcji dostępne z usługą Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c13ec78d-07e9-4646-8194-cf3efafc1760
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 10f6c0533027767b6635ebff1e6a9872bde06a68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="what-kind-of-collection-do-you-need-for-azure-remoteapp"></a>Jakiego rodzaju kolekcji potrzebujesz w usłudze Azure RemoteApp?
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Usługa Azure RemoteApp pozwala udostępniać aplikacje i zasoby użytkownikom na dowolnym urządzeniu. Firma Microsoft to zrobić, tworząc kolekcje do przechowywania aplikacji i zasobów, a następnie udostępnić te kolekcje z użytkownikami. Istnieją 2 Opcje innej kolekcji z inną siecią i opcje uwierzytelniania — które jest odpowiednie dla Ciebie?

Przejdźmy różne aspekty i opcji, należy upewnić się na maksymalne wykorzystanie kolekcji usługi Azure RemoteApp. 

## <a name="quick-differences-between-the-collection-types"></a>Szybkie różnice między typy kolekcji
|  | Chmura | Połączenie hybrydowe |
| --- | --- | --- |
| Użyj istniejącej sieci Wirtualnej |Tak |Tak |
| Wymaga konta połączenia AD (DirSync) |Nie |Tak |
| Wymaga przyłączania do domeny |Nie |Tak |
| Wymaga kontrolera domeny jest dostępny dla sieci Wirtualnej |Nie |Tak |

## <a name="cloud-collections"></a>Kolekcje w chmurze
* Szybko utworzyć - kolekcji szybko zainicjowaniu obsługi, co oznacza aplikacji Pobierz użytkownikom szybciej.
* Umieść własne aplikacje lub udostępnić nasze. Możesz użyć niestandardowego obrazu (zbudowane na podstawie maszyny Wirtualnej platformy Azure) lub jeden z obrazów zawartych w ramach subskrypcji.
* Nie trzeba skonfigurować połączenie między kolekcji i domeny lokalnej.
* Jednak w celu zapewnienia dostępu do środowiska lokalnego do udostępniania danych lub z systemem innym niż Windows uwierzytelniania do zasobów, takich jak SQL Server (przy użyciu uwierzytelniania bazy danych) można używać własnej sieci wirtualnej platformy Azure.

OK jak jeden utworzyć?

* Tylko w chmurze? Utwórz z **szybkie tworzenie** opcji w portalu.
* Chmura + sieć Wirtualną? Tworzenie przy użyciu **Utwórz z sieci Wirtualnej** opcji, ale nie chcesz dołączyć do domeny.

## <a name="hybrid-collections"></a>Kolekcje hybrydowe
* Umożliwianie pełnego dostępu do sieci lokalnej + sieci Wirtualnej platformy Azure.
* Obejmuje domeny sprzężenia dostęp do aplikacji i danych. Zdalne aplikacje mogą uwierzytelniania względem lokalnej usługi Active Directory — one następnie dostęp do zasobów w domenie.
* Zaawansowane monitorowanie oraz zarządzania z istniejących rozwiązań System Center i zasad grupy systemu Windows (za pośrednictwem obraz niestandardowy oparty na systemie Windows Server 2012 R2)
* Obsługa [ExpressRoute](https://azure.microsoft.com/services/expressroute/) nawiązywania połączenia z sieci lokalnej sieci wirtualnej platformy Azure.

Tworzenie przy użyciu **Utwórz z sieci Wirtualnej** opcję i wybierz opcję dołączenia do domeny.

## <a name="authentication-options"></a>Opcje uwierzytelniania
Usługa Azure RemoteApp obsługuje konta Microsoft i konta usługi Azure Active Directory, ale nie wszystkie kolekcje obsługują wszystkie metody. 

| Typ konta |  | Chmura | Chmury i sieci Wirtualnej | Połączenie hybrydowe |
| --- | --- | --- | --- | --- |
| Konto Microsoft | |Tak |Tak |Nie |
| Azure Active Directory (Azure AD) | | | | |
| Tylko usługi Azure AD |Tak |Tak |Nie | |
| AD Connect z synchronizacją haseł |Tak |Tak |Tak | |
| Połącz AD bez synchronizacji haseł |Tak |Tak |Nie | |
| AD Connect z usługami AD FS |Tak |Tak |Tak | |
| dostawców tożsamości obsługiwane Azure 3rd firm (takie jak Ping) |Tak |Tak |Tak | |
| Multi-Factor Authentication | |Tak |Tak |Tak |

### <a name="cloud-and-cloud--vnet"></a>Chmury i chmury i sieci Wirtualnej
Z kolekcjami chmury używając konta Microsoft, konta usługi Azure AD lub zmieszanie dwóch. Użyj konta, które najlepiej dla użytkowników.

Nie ma żadnych określonych wymagań dla za pomocą konta Microsoft. 

Jeśli chcesz użyć konta usługi Azure AD, należy się upewnić, że dzierżawy usługi Azure AD jest zgodna z skojarzonych z Twoją subskrypcją. Podczas tworzenia subskrypcji usługi Azure RemoteApp dzierżawy usługi Azure AD, który był używany był automatycznie skojarzone z subskrypcją. Każdy użytkownik usługi Azure AD, które zezwolić na musi być tego samego dzierżawcy. W razie potrzeby można [zmiana dzierżawy usługi Azure AD](remoteapp-changetenant.md) skojarzonych z Twoją subskrypcją.

### <a name="hybrid-or-cloud--azure-ad--ad"></a>Hybrydowe (lub w chmurze, jak i Azure AD + AD)
Używanie programu Azure AD i lokalnej usługi Active Directory jest wymagane w przypadku kolekcji hybrydowych. Należy użyć AD Connect do integracji katalogów dwa. Ale masz niektórych wybór, jeśli chodzi o sposób konfigurowania AD Connect. 

Istnieją 2 AD Connect scenariusze — przy użyciu synchronizacji haseł lub federacyjnych usługi AD. Zapoznaj się z [informacji AD Connect](../active-directory/active-directory-aadconnect.md) Aby ustalić którym te działa najlepiej dla Ciebie.

Można również używać usługi Azure AD + AD z kolekcji w chmurze. Upewnij się, że należy wykonać takie same ustawienia czynności.

Zapoznaj się z [usługi Azure AD i wymagania usługi Active Directory dla usługi Azure RemoteApp](remoteapp-ad.md) kroki wymagane do skonfigurowania usługi Azure AD i usługi Active Directory.

## <a name="go-create-your-collection"></a>Wszystko gotowe. Tworzenie kolekcji
OK myślę, że firma Microsoft już znalezienia go teraz, więc istnieje tylko jeden element na czy — tworzenie pierwszej kolekcji usługi Azure RemoteApp.

[Tworzenie kolekcji w chmurze](remoteapp-create-cloud-deployment.md) lub [tworzenie kolekcji hybrydowej](remoteapp-create-hybrid-deployment.md) — wystarczy pobrać tworzenia.

