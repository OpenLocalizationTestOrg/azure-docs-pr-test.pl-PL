---
title: "Usługi Azure Active Directory Domain Services: Scenariusze wdrażania | Dokumentacja firmy Microsoft"
description: "Scenariusze wdrażania usług domenowych Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c5216ec9-4c4f-4b7e-830b-9d70cf176b20
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: maheshu
ms.openlocfilehash: 8a64bd8f7c6eba8f6490e10fa62bef195b6b3d5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-scenarios-and-use-cases"></a>Scenariusze wdrażania i przypadki użycia
W tej sekcji przyjrzymy się kilka scenariuszy i przypadków użycia, które korzystają z usług domenowych w usłudze Azure Active Directory (AD).

## <a name="secure-easy-administration-of-azure-virtual-machines"></a>Bezpieczne i łatwe zarządzanie maszyn wirtualnych platformy Azure
Toomanage usług domenowych Azure Active Directory można użyć maszynach wirtualnych Azure w sposób prostsze. Maszyny wirtualne platformy Azure można toohello przyłączone do domeny zarządzanej, dzięki czemu toouse toolog w poświadczeń firmowych usługi AD. To rozwiązanie pomaga uniknąć problemu zarządzania poświadczeń, takich jak obsługa kont administratora lokalnego na wszystkich maszynach wirtualnych platformy Azure.

Serwer maszyn wirtualnych, które są toohello przyłączone do domeny zarządzanej można również zarządzane i chronione przy użyciu zasad grupy. Możesz zastosować tooyour linie bazowe zabezpieczeń wirtualnej Azure maszyny i zablokowanie zgodnie z zasadami bezpieczeństwa firmowych. Na przykład można użyć grupy zarządzania możliwości toorestrict hello typów zasad aplikacji, które mogą zostać uruchomione na tych maszynach wirtualnych.

![Usprawnione zarządzanie maszyn wirtualnych platformy Azure](./media/active-directory-domain-services-scenarios/streamlined-vm-administration.png)

Serwery i pozostałą infrastrukturą osiągnie z eksploatacji, Contoso jest przenoszona wiele aplikacji aktualnie obsługiwana w chmurze toohello lokalne. Bieżący standardowego IT ma, że serwery hostujące aplikacje firmowe musi być przyłączony do domeny i zarządzane przy użyciu zasad grupy. Firmy Contoso maszyn wirtualnych sprzężenia toodomain wdrożonych na platformie Azure, administracja toomake łatwiejsze preferuje administratora IT. W związku z tym administratorzy i użytkownicy mogą Zaloguj się za pomocą poświadczeń firmowych. Na powitania tym samym czasie maszyny może być skonfigurowany toocomply z linie bazowe zabezpieczeń za pomocą zasad grupy. Contoso wolisz nie toohave toodeploy, monitorowanie i Zarządzanie kontrolerami domeny w Azure toosecure maszyn wirtualnych platformy Azure. W związku z tym usługi domenowe Azure AD jest doskonałym rozwiązaniem dla przypadek użycia.

**Uwagi dotyczące wdrażania**

Należy wziąć pod uwagę hello następujące punkty ważne dla tego scenariusza wdrażania:

* Domen zarządzanych udostępniane przez usługi domenowe Azure AD Podaj pojedynczy płaska struktura OU (jednostki organizacyjnej), domyślnie. Wszystkie komputery przyłączone do domeny znajdują się w jednej jednostce Organizacyjnej płaskim. Można jednak wybrać toocreate niestandardowych jednostek organizacyjnych.
* Usługi domenowe Azure AD obsługuje prosty zasad grupy w formie hello wbudowanego obiektu zasad grupy Każdy hello użytkownicy i komputery kontenerów. Można tworzyć niestandardowe obiekty zasad grupy i adresować je toocustom jednostek organizacyjnych.
* Usługi domenowe Azure AD obsługuje schematu obiektu komputera AD hello podstawowego. Nie można rozszerzyć schematu obiektu hello komputera.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-bind-authentication-tooazure-infrastructure-services"></a>Przyrostu i shift aplikacji lokalnej, która używa tooAzure uwierzytelniania wiązania LDAP usługi infrastruktury
![Wiązanie LDAP](./media/active-directory-domain-services-scenarios/ldap-bind.png)

Firma Contoso ma aplikacji lokalnych, które zostało zakupione od niezależnego dostawcy oprogramowania wielu lat temu. Aplikacja Hello jest obecnie w trybie konserwacji przez hello niezależnego dostawcy oprogramowania i żądania zmiany toohello aplikacji jest zbyt duży dla Contoso. Ta aplikacja ma frontonu sieci web, służąca do zbierania poświadczeń użytkownika za pomocą formularza sieci web i następnie uwierzytelnia użytkowników, wykonując toohello wiązania LDAP firmowej usługi Active Directory. Contoso chcieliby toomigrate tooAzure tej aplikacji usługi infrastruktury. Jest pożądane, czy aplikacja hello działa zgodnie z jest bez konieczności wprowadzania żadnych zmian. Ponadto użytkownicy powinna być stanie tooauthenticate przy użyciu istniejących poświadczeń firmowych i bez o tooretrain użytkowników toodo rzeczy inaczej. Innymi słowy użytkownicy końcowi powinna być oblivious, z którym jest uruchomiona aplikacja hello i migracji hello powinien być toothem przezroczysty.

**Uwagi dotyczące wdrażania**

Należy wziąć pod uwagę hello następujące punkty ważne dla tego scenariusza wdrażania:

* Upewnij się, aplikacja hello nie jest konieczne katalogu toohello toomodify/zapisu. Domen toomanaged zapisu LDAP udostępniane przez usługi domenowe Azure AD nie jest obsługiwane.
* Nie można zmienić hasła bezpośrednio przed hello domeny zarządzanej. Użytkownicy końcowi mogą zmieniać swoje hasła albo przy użyciu mechanizmu zmiany hasła samoobsługi usługi Azure AD lub względem hello katalogu lokalnego. Te zmiany są automatycznie synchronizowane i dostępne w hello domeny zarządzanej.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-read-tooaccess-hello-directory-tooazure-infrastructure-services"></a>Przyrostu shift aplikacji lokalnej, która używa protokołu LDAP odczytu tooaccess hello katalogu tooAzure usługi infrastruktury
Firma Contoso ma lokalnego aplikacji — biznesowych (LOB), która został opracowany niemal dekadę temu. Ta aplikacja jest katalogiem aware i została zaprojektowana toowork z systemem Windows Server AD. Aplikacja Hello używa protokołu LDAP (Lightweight Directory Access Protocol) tooread informacji/atrybutów dotyczących użytkowników z usługi Active Directory. Aplikacja Hello zmodyfikować atrybuty lub nie w przeciwnym razie zapisu toohello katalogu. Contoso chcieliby toomigrate tooAzure tej aplikacji usługi infrastruktury i wycofywania urządzeń lokalnych przedawnienia hello aktualnie obsługujący tej aplikacji. Aplikacja Hello nie może zostać ponownie zapisane toouse nowoczesnych katalogu interfejsów API, takich jak hello opartego na interfejsie REST API Azure AD Graph. W związku z tym wymagane jest opcja przyrostu i shift, zgodnie z którą aplikacja hello mogą być migrowane toorun w chmurze hello, bez modyfikowania kodu lub ponowne zapisywanie aplikacji hello.

**Uwagi dotyczące wdrażania**

Należy wziąć pod uwagę hello następujące punkty ważne dla tego scenariusza wdrażania:

* Upewnij się, aplikacja hello nie jest konieczne katalogu toohello toomodify/zapisu. Domen toomanaged zapisu LDAP udostępniane przez usługi domenowe Azure AD nie jest obsługiwane.
* Upewnij się, aplikacja hello nie wymaga niestandardowych/rozszerzony schemat usługi Active Directory. Rozszerzenia schematu nie są obsługiwane w usługach domenowych Azure AD.

## <a name="migrate-an-on-premises-service-or-daemon-application-tooazure-infrastructure-services"></a>Migrowanie lokalnych usługa lub demon aplikacji tooAzure usługi infrastruktury
Niektóre aplikacje składają się z wielu warstw, gdy jeden z poziomów hello musi tooperform uwierzytelnionego połączenia tooa zaplecza warstwy, takie jak warstwy bazy danych. Konta usługi Active Directory są często używane dla tych przypadków użycia. Można przyrostu shift takich aplikacji tooAzure usługi infrastruktury i używania usługi domenowe Azure AD na potrzeby hello tożsamości z tych aplikacji. Możesz wybrać toouse hello tego samego konta usługi synchronizowanych z tooAzure katalogu z lokalnej usługi AD. Alternatywnie można najpierw utworzyć niestandardowy jednostkę Organizacyjną, a następnie utworzyć osobnego konta usługowego w tej jednostce Organizacyjnej, toodeploy takich aplikacji.

![Konto usługi za pomocą WIA](./media/active-directory-domain-services-scenarios/wia-service-account.png)

Firma Contoso ma niestandardowej magazynu aplikacji frontonu sieci web, programu SQL server i serwera wewnętrznej bazy danych FTP. Uwierzytelnianie zintegrowane systemu Windows kont usług jest serwer frontonu sieci web używanych tooauthenticate hello w toohello FTP. Fronton sieci web Hello skonfigurowano toorun jako konto usługi. Witaj serwera wewnętrznej bazy danych skonfigurowano tooauthorize dostęp z konta usługi hello hello sieci web frontonu. Contoso preferuje nie toohave toodeploy maszyny wirtualnej kontrolera domeny w toomove chmury hello tooAzure tej aplikacji usługi infrastruktury. Firmy Contoso administratora IT można wdrożyć serwery hello hostowania frontonu sieci web hello, programu SQL server i maszyny wirtualne tooAzure serwera hello FTP. Te maszyny są przyłączone do tooan usługi domenowe Azure AD zarządzaną domeny. Następnie można użyć tego samego konta usługi w ich katalogu lokalnego na potrzeby uwierzytelniania aplikacji hello hello. To konto usługi domeny zarządzanej usług domenowych Azure AD synchronizowane toohello i jest dostępny do użycia.

**Uwagi dotyczące wdrażania**

Należy wziąć pod uwagę hello następujące punkty ważne dla tego scenariusza wdrażania:

* Upewnij się, że aplikacja hello używa nazwy użytkownika i hasła do uwierzytelnienia. Uwierzytelnianie certyfikatu/karty inteligentnej na podstawie nie jest obsługiwane przez usługi domenowe Azure AD.
* Nie można zmienić hasła bezpośrednio przed hello domeny zarządzanej. Użytkownicy końcowi mogą zmieniać swoje hasła albo przy użyciu mechanizmu zmiany hasła samoobsługi usługi Azure AD lub względem hello katalogu lokalnego. Te zmiany są automatycznie synchronizowane i dostępne w hello domeny zarządzanej.

## <a name="windows-server-remote-desktop-services-deployments-in-azure"></a>Wdrożenia na platformie Azure usług pulpitu zdalnego serwera systemu Windows
Za pomocą usług domenowych Azure AD tooprovide zarządzane AD z usług domenowych tooyour zdalnych serwerów pulpitu wdrożona na platformie Azure.

Aby uzyskać więcej informacji na temat tego scenariusza wdrażania, zobacz temat jak zbyt[Integrowanie usług domenowych Azure AD z wdrożeniem usług pulpitu zdalnego](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-azure-adds).
