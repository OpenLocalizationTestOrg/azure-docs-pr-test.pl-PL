---
title: "aaaOverview usług domenowych Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Omówienie usług domenowych w usłudze Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 0d47178f-773e-45f9-9ff4-9e8cffa4ffa2
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 2b4884b3b8b639fcca438ddbab0bd3361aac53c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Azure AD Domain Services
## <a name="overview"></a>Omówienie
Usług infrastruktury platformy Azure umożliwiają toodeploy szeroką gamę rozwiązań opartych na przetwarzaniu w sposób elastyczne. Z maszyn wirtualnych platformy Azure można wdrożyć niemal natychmiast i płacisz tylko za minutę hello. Przy użyciu pomocy technicznej dla systemu Windows, Linux, SQL Server, Oracle, IBM, SAP i BizTalk, można wdrożyć żadnych obciążenie, dowolnego języka, w niemal dowolnym systemie operacyjnym. Te korzyści Włącz toomigrate starszych aplikacji wdrożonych lokalnie tooAzure, toosave na kosztów operacyjnych.

Kluczowym aspektem migracji w lokalnym tooAzure aplikacji jest zaspokajania potrzeb tożsamości hello te aplikacje. Aplikacje z obsługą katalogu może polegać na LDAP dla katalogu firmy toohello odczytu lub zapisu lub zależą od użytkowników końcowych tooauthenticate zintegrowanego uwierzytelniania systemu Windows (uwierzytelnianie Kerberos lub NTLM). Biznesowych (LOB) w systemie Windows Server zwykle wdrożenia aplikacji na komputerach przyłączonych do domeny, więc będą one zarządzane przy użyciu zasad grupy. too'lift shift "chmury toohello aplikacji lokalnie, te zależności w infrastrukturze tożsamością firmową hello muszą toobe rozwiązane.

Administratorzy często włączyć tooone hello następujące rozwiązania toosatisfy hello tożsamości potrzeby swoich aplikacji wdrożonych na platformie Azure:

* Wdrożyć połączenia sieci VPN lokacja lokacja między obciążeń uruchomionych usług infrastruktury platformy Azure i hello firmowej katalogu lokalnego.
* Konfigurowanie replik kontrolerów domeny przy użyciu maszyn wirtualnych platformy Azure, aby rozszerzyć hello AD firmowej infrastruktury domenie lub lesie.
* Wdrożenie autonomicznej domeny na platformie Azure przy użyciu kontrolery domeny wdrożone jako maszyny wirtualnej platformy Azure.

Tych sposobów obniżenie kosztu wysokiej i koszty administracyjne. Administratorzy są wymagane toodeploy kontrolerów domeny przy użyciu maszyn wirtualnych na platformie Azure. Ponadto potrzebnych toomanage bezpieczny, poprawki, monitor, kopie zapasowe i rozwiązywanie problemów z tych maszyn wirtualnych. Hello zależność od toohello połączeń sieci VPN w lokalnym katalogu powoduje obciążeń wdrożonych błędami występującymi sieci narażone tootransient Azure toobe lub awarie. Te awarii sieci z kolei powoduje niższe przestojów i zmniejszonej niezawodności tych aplikacji.

Firma Microsoft zaprojektowane usług domenowych Azure AD tooprovide alternatywę łatwiejsze.

## <a name="introducing-azure-ad-domain-services"></a>Wprowadzenie do usług domenowych Azure AD
Usługi domenowe Azure AD zapewnia domeny zarządzanej usług, takich jak przyłączanie do domeny, uwierzytelniania Kerberos/NTLM zasad, LDAP, grupy, który są w pełni zgodne z usługą Active Directory systemu Windows Server. Można korzystać z tych usług domenowych, bez potrzeby hello toodeploy możesz, zarządzanie i poprawka kontrolerów domeny w chmurze hello. Usługi domenowe Azure AD jest zintegrowany z istniejących dzierżawy usługi Azure AD, w związku z tym umożliwiające toolog użytkowników przy użyciu swoich poświadczeń firmowych. Możesz użyć istniejących grup i użytkowników kont toosecure dostępu tooresources zapewnić płynność "przyrostu i shift" z lokalnymi zasobami tooAzure usługi infrastruktury w ten sposób.

Azure funkcjonalności usług domenowych AD współdziała niezależnie od tego, czy dzierżawy usługi Azure AD tylko w chmurze lub zsynchronizowanej lokalnej usługi Active Directory.

### <a name="azure-ad-domain-services-for-cloud-only-organizations"></a>Usługi domenowe Azure AD dla organizacji, tylko w chmurze
Dzierżawy usługi Azure AD tylko w chmurze (często określonego tooas zł "zarządzane dzierżaw") nie ma żadnych wpływ tożsamości lokalnych. Innymi słowy konta użytkowników, hasła i członkostwa w grupach są wszystkie chmury natywnego toohello — to znaczy tworzone i zarządzane w usłudze Azure AD. Należy wziąć pod uwagę chwilę czy firma Contoso jest tylko w chmurze dzierżawę usługi Azure AD. Jak pokazano na następującej ilustracji hello, administrator firmy Contoso została skonfigurowana sieć wirtualną w usługi infrastruktury platformy Azure. Aplikacje i obciążenia serwera są wdrażane w tej sieci wirtualnej w maszynach wirtualnych platformy Azure. Ponieważ firma Contoso używa dzierżawy tylko w chmurze, wszystkie tożsamości użytkownika, poświadczeń i członkostwa w grupach są tworzone i zarządzane w usłudze Azure AD.

![Omówienie usług domenowych Azure AD](./media/active-directory-domain-services-overview/aadds-overview.png)

Firmy Contoso administratora IT można włączyć usługi domenowe Azure AD dla swojej dzierżawy usługi Azure AD i wybrać toomake domeny usług dostępnych w tej sieci wirtualnej. Później usługi domenowe Azure AD obsługuje domeną zarządzaną i udostępnia go w sieci wirtualnej hello. Wszystkie konta użytkowników, członkostwa w grupach i poświadczeń użytkownika należące do firmy Contoso dzierżawy usługi Azure AD są dostępne również w tej domenie nowo utworzony. Ta funkcja umożliwia użytkownikom w toosign organizacji hello w domenie toohello przy użyciu swoich poświadczeń firmowych — na przykład podczas nawiązywania połączenia zdalne toodomain przyłączone do maszyn za pośrednictwem pulpitu zdalnego. Administratorzy mogą zapewnić obsługę administracyjną tooresources dostępu w domenie hello przy użyciu istniejącego członkostwa w grupach. Aplikacje wdrożone na maszynach wirtualnych na powitania sieci wirtualnej można użyć funkcji, takich jak przyłączanie do domeny, LDAP odczytu LDAP bind, uwierzytelniania NTLM i Kerberos i zasad grupy.

Oto kilka istotne aspekty hello domeny zarządzanej, które jest udostępniane przez usługi domenowe Azure AD:

* Firmy Contoso IT administrator nie musi toomanage, patch lub monitorowanie ta domena lub dowolnym kontrolerze domeny dla tej domeny zarządzanej.
* Nie ma żadnych replikacji toomanage AD należy dla tej domeny. Konta użytkowników, członkostwa w grupach i poświadczeń z dzierżawy usługi Azure AD firmy Contoso są automatycznie dostępne w ramach tej domeny zarządzanej.
* Ponieważ domeny hello jest zarządzana przez usługi domenowe Azure AD, Contoso przez administratora IT nie ma uprawnień administratora domeny lub administratora przedsiębiorstwa w tej domenie.

### <a name="azure-ad-domain-services-for-hybrid-organizations"></a>Usługi domenowe Azure AD dla organizacji hybrydowego
Organizacje z hybrydowym infrastruktury IT używać różnych zasobów w chmurze i zasobów lokalnych. Takie organizacje zsynchronizować informacji o tożsamości ze swojej dzierżawy usługi Azure AD tootheir katalogu lokalnego. Organizacje hybrydowego Szukaj toomigrate więcej chmury w toohello ich lokalnych aplikacji, szczególnie starszych aplikacji obsługujących katalogu, usługi domenowe Azure AD mogą być przydatne toothem.

Wdrożono litware Corporation [Azure AD Connect](../active-directory/active-directory-aadconnect.md), informacje o tożsamości toosynchronize ich dzierżawy usługi Azure AD tootheir katalogu lokalnego. informacje o tożsamości Hello, który jest synchronizowany zawiera konta użytkowników, ich skrótów poświadczeń uwierzytelniania (synchronizacja haseł) i członkostwa w grupach.

> [!NOTE]
> **Synchronizacja haseł jest obowiązkowa w przypadku hybrydowych organizacje toouse usługi domenowe Azure AD**. To wymaganie jest ponieważ hello zarządzane nie są wymagane poświadczenia użytkowników domeny udostępniane przez usługi domenowe Azure AD, tooauthenticate tych użytkowników przy użyciu metody uwierzytelniania NTLM lub Kerberos.
>
>

![W przypadku Litware usługi domenowe Azure AD](./media/active-directory-domain-services-overview/aadds-overview-synced-tenant.png)

Hello poprzedniego ilustracji przedstawiono sposób organizacji mających hybrydowej infrastruktury IT, takich jak Litware Corporation, można użyć usług domenowych Azure AD. Aplikacje i obciążenia serwera, które wymagają usług domenowych w usłudze litware's są wdrażane w sieci wirtualnej w usługi infrastruktury platformy Azure. Litware's administratora IT można włączyć usługi domenowe Azure AD dla swojej dzierżawy usługi Azure AD i wybrać toomake domeny zarządzanej dostępne w tej sieci wirtualnej. Ponieważ Litware organizacji z hybrydowej infrastruktury IT, kont użytkowników, grup i poświadczenia są dzierżawy zsynchronizowane tootheir usługi Azure AD z katalogiem lokalnym. Ta funkcja umożliwia toosign użytkowników w domenie toohello przy użyciu swoich poświadczeń firmowych — na przykład przy połączeniu zdalnym toomachines przyłączone do domeny toohello za pośrednictwem pulpitu zdalnego. Administratorzy mogą zapewnić obsługę administracyjną tooresources dostępu w domenie hello przy użyciu istniejącego członkostwa w grupach. Aplikacje wdrożone na maszynach wirtualnych na powitania sieci wirtualnej można użyć funkcji, takich jak przyłączanie do domeny, LDAP odczytu LDAP bind, uwierzytelniania NTLM i Kerberos i zasad grupy.

Oto kilka istotne aspekty hello domeny zarządzanej, które jest udostępniane przez usługi domenowe Azure AD:

* domeny zarządzanej Hello jest autonomiczna domeny. Nie jest rozszerzeniem Litware's lokalnej domeny.
* Litware's IT administrator nie potrzebuje toomanage, patch lub monitor kontrolery domeny dla tej domeny zarządzanej.
* Nie ma potrzeby toomanage AD replikacji toothis domeny nie istnieje. Konta użytkowników, członkostwa w grupach i poświadczeń z katalogiem lokalnym Litware's są synchronizowane tooAzure AD za pomocą usługi Azure AD Connect. Te konta użytkowników, członkostwa w grupach i poświadczeń są automatycznie dostępne w hello domeny zarządzanej.
* Ponieważ domeny hello jest zarządzana przez usługi domenowe Azure AD, Litware przez administratora IT nie ma uprawnień administratora domeny lub administratora przedsiębiorstwa w tej domenie.

## <a name="benefits"></a>Korzyści
Z usług domenowych Azure AD można korzystać z hello następujące korzyści:

* **Proste** — mogą spełniać potrzeby tożsamości hello maszyn wirtualnych wdrożonych tooAzure infrastruktury usług za pomocą kilku kliknięć proste. Nie należy toodeploy i zarządzanie infrastrukturą tożsamości w Azure lub ustawienia łączności tooyour wstecz lokalnej infrastruktury tożsamości.
* **Zintegrowane** — usługi domenowe Azure AD jest ściśle zintegrowana z dzierżawy usługi Azure AD. Usługi Azure AD można teraz używać jak katalog zintegrowanego przedsiębiorstwa oparte na chmurze przeznaczoną toohello potrzeby nowoczesnych aplikacji i tradycyjnych aplikacjom obsługującym architekturę katalogu.
* **Zgodne** — usługi domenowe Azure AD jest zbudowany na powitania sprawdzonych klasy infrastrukturze usługi Active Directory systemu Windows Server. W związku z tym aplikacji może polegać na wysoki stopień zgodności z funkcji usługi Active Directory systemu Windows Server. Nie wszystkie funkcje dostępne w systemie Windows Server AD są obecnie dostępne w usługach domenowych Azure AD. Jednak funkcje dostępne są zgodne z hello odpowiednie funkcje systemu Windows Server AD wykorzystywany w infrastrukturze lokalnej. Hello LDAP protokołu Kerberos, NTLM, zasady grupy i domeny możliwości sprzężenia stanowią dojrzałe oferty, które zostały przetestowane i wprowadzono ulepszenia w różnych wersjach systemu Windows Server.
* **Ekonomiczne** — z usługami domenowymi w usłudze Azure AD, można uniknąć obciążenia infrastruktury i zarządzania hello skojarzony z zasadami zarządzania tradycyjnych aplikacji obsługujących katalogu tożsamości infrastruktury toosupport. Można przenieść te aplikacje tooAzure usługi infrastruktury i korzystać z niższych kosztów operacyjnych.
