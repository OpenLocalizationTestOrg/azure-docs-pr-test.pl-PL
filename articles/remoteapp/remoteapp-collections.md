---
title: "rodzaj aaaWhat kolekcji potrzebujesz usługi Azure RemoteApp? | Microsoft Docs"
description: "Informacje o typach hello kolekcji dostępne z usługą Azure RemoteApp."
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
ms.openlocfilehash: f00b5fe41af597cf75e26300bf7842c3a8ff94fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-kind-of-collection-do-you-need-for-azure-remoteapp"></a>Jakiego rodzaju kolekcji potrzebujesz w usłudze Azure RemoteApp?
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Usługa Azure RemoteApp pozwala udostępniać aplikacje i zasoby użytkownikom na dowolnym urządzeniu. Firma Microsoft to zrobić, tworząc aplikacji hello toohold kolekcji i zasobów, a następnie udostępnić te kolekcje z użytkownikami. Istnieją 2 Opcje innej kolekcji z inną siecią i opcje uwierzytelniania — które jest odpowiednie dla Ciebie?

Przejdźmy hello różne aspekty i dostępnych wyborów najbardziej potrzebne toomake tooget hello poza kolekcji usługi Azure RemoteApp. 

## <a name="quick-differences-between-hello-collection-types"></a>Szybkie różnice między hello typy kolekcji
|  | Chmura | Połączenie hybrydowe |
| --- | --- | --- |
| Użyj istniejącej sieci Wirtualnej |Tak |Tak |
| Wymaga konta połączenia AD (DirSync) |Nie |Tak |
| Wymaga przyłączania do domeny |Nie |Tak |
| Wymaga tooVNET dostępny kontroler domeny |Nie |Tak |

## <a name="cloud-collections"></a>Kolekcje w chmurze
* Szybkie toocreate - kolekcji hello szybko zainicjowaniu obsługi, co oznacza, że aplikacje pobrać toousers szybciej.
* Umieść własne aplikacje lub udostępnić nasze. Możesz użyć niestandardowego obrazu (zbudowane na podstawie maszyny Wirtualnej platformy Azure) lub jeden z obrazów hello uwzględnionych w subskrypcji.
* Nie trzeba tooconfigure połączenie między kolekcji i domeny lokalnej.
* Jednak można używać własnych sieci Wirtualnej Azure tooprovide dostępu do środowiska lokalnego do uwierzytelniania danych udostępnianie lub toouse z systemem innym niż Windows do zasobów, takich jak SQL Server (przy użyciu uwierzytelniania bazy danych).

OK jak jeden utworzyć?

* Tylko w chmurze? Tworzenie z hello **szybkie tworzenie** opcji w portalu hello.
* Chmura + sieć Wirtualną? Tworzenie przy użyciu hello **Utwórz z sieci Wirtualnej** opcji, ale nie wybierzesz toojoin domeny.

## <a name="hybrid-collections"></a>Kolekcje hybrydowe
* Podaj pełnego dostępu do sieci lokalnej tooon + sieci Wirtualnej platformy Azure.
* Obejmuje domeny sprzężenia dostęp do aplikacji i danych. Zdalne aplikacje mogą uwierzytelniania względem lokalnej usługi Active Directory — one następnie dostęp do zasobów w domenie.
* Zaawansowane monitorowanie oraz zarządzania z istniejących rozwiązań System Center i zasad grupy systemu Windows (za pośrednictwem obraz niestandardowy oparty na systemie Windows Server 2012 R2)
* Obsługa [ExpressRoute](https://azure.microsoft.com/services/expressroute/) tooconnect tooyour Twojej sieci Wirtualnej Azure lokalnej sieci Wirtualnej.

Tworzenie przy użyciu hello **Utwórz z sieci Wirtualnej** opcję i wybierz polecenie toojoin domeny.

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
Z kolekcji w chmurze można użyć konta Microsoft, konta usługi Azure AD lub mieszane hello dwa. Użyj konta hello, które najlepiej dla użytkowników.

Nie ma żadnych określonych wymagań dla za pomocą konta Microsoft. 

Jeśli chcesz toouse konta usługi Azure AD, należy toomake się, że dzierżawy usługi Azure AD odpowiada hello jedną skojarzonych z Twoją subskrypcją. Podczas tworzenia subskrypcji usługi Azure RemoteApp hello dzierżawy usługi Azure AD, który był używany był automatycznie skojarzone z subskrypcją. Każdy użytkownik usługi Azure AD można przyznać uprawnień tooneeds toobe tego samego dzierżawcy. W razie potrzeby można [zmiana dzierżawy usługi Azure AD hello](remoteapp-changetenant.md) skojarzonych z Twoją subskrypcją.

### <a name="hybrid-or-cloud--azure-ad--ad"></a>Hybrydowe (lub w chmurze, jak i Azure AD + AD)
Używanie programu Azure AD i lokalnej usługi Active Directory jest wymagane w przypadku kolekcji hybrydowych. Należy toouse AD Connect toointegrate hello dwa katalogi. Ale masz niektórych wybór po przejściu do toohow skonfigurować AD Connect. 

Istnieją 2 AD Connect scenariusze — przy użyciu synchronizacji haseł lub federacyjnych usługi AD. Zapoznaj się z hello [informacji AD Connect](../active-directory/active-directory-aadconnect.md) toofigure się, które z nich działa najlepiej dla Ciebie.

Można również używać usługi Azure AD + AD z kolekcji w chmurze. Upewnij się, że wykonaj hello skonfigurować takie same czynności.

Zapoznaj się z [usługi Azure AD i wymagania usługi Active Directory dla usługi Azure RemoteApp](remoteapp-ad.md) hello kroki wymagane tooconfigure usługi Azure AD i usługi Active Directory.

## <a name="go-create-your-collection"></a>Wszystko gotowe. Tworzenie kolekcji
OK myślę, firma Microsoft już znalezienia go teraz, tak, aby tylko jeden element toodo po lewej stronie — Tworzenie pierwszej kolekcji usługi Azure RemoteApp.

[Tworzenie kolekcji w chmurze](remoteapp-create-cloud-deployment.md) lub [tworzenie kolekcji hybrydowej](remoteapp-create-hybrid-deployment.md) — wystarczy pobrać tworzenia.

