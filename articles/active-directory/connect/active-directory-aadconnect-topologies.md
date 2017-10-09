---
title: "Usługi Azure AD Connect: Topologie obsługiwane przez | Dokumentacja firmy Microsoft"
description: "W tym temacie szczegółowo obsługiwane i nieobsługiwane topologie programu Azure AD Connect"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 1034c000-59f2-4fc8-8137-2416fa5e4bfe
ms.service: active-directory
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: identity
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 41632a54e8e85492fbf1a751ef4e618c8870abe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="topologies-for-azure-ad-connect"></a>Topologie obsługiwane w programie Azure AD Connect
W tym artykule opisano różne lokalnymi i topologii usługi Azure Active Directory (Azure AD), używające synchronizacja programu Azure AD Connect jako klucza hello rozwiązania. W tym artykule opisano zarówno obsługiwane i nieobsługiwane konfiguracje.

Oto legendy hello obrazów w artykule hello:

| Opis | Symbol |
| --- | --- |
| W lokalnym lesie usługi Active Directory |![W lokalnym lesie usługi Active Directory](./media/active-directory-aadconnect-topologies/LegendAD1.png) |
| W lokalnej usłudze Active Directory z filtrowanych importu |![Usługi Active Directory z filtrowanych importu](./media/active-directory-aadconnect-topologies/LegendAD2.png) |
| Serwer synchronizacji usługi Azure AD Connect |![Serwer synchronizacji usługi Azure AD Connect](./media/active-directory-aadconnect-topologies/LegendSync1.png) |
| Azure AD Connect serwera synchronizacji "Tryb przejściowy" |![Azure AD Connect serwera synchronizacji "Tryb przejściowy"](./media/active-directory-aadconnect-topologies/LegendSync2.png) |
| Usługi GALSync z programu Forefront Identity Manager (FIM) 2010 lub Microsoft Identity Manager (MIM) 2016 |![Usługi GALSync z programu FIM 2010 lub MIM 2016](./media/active-directory-aadconnect-topologies/LegendSync3.png) |
| Serwer synchronizacji usługi Azure AD Connect, szczegółowe |![Serwer synchronizacji usługi Azure AD Connect, szczegółowe](./media/active-directory-aadconnect-topologies/LegendSync4.png) |
| Azure AD |![Usługa Azure Active Directory](./media/active-directory-aadconnect-topologies/LegendAAD.png) |
| Nieobsługiwany scenariusz |![Nieobsługiwany scenariusz](./media/active-directory-aadconnect-topologies/LegendUnsupported.png) |

## <a name="single-forest-single-azure-ad-tenant"></a>Pojedynczy las, pojedynczy dzierżawy usługi Azure AD
![Topologia jednego lasu i pojedynczej dzierżawy](./media/active-directory-aadconnect-topologies/SingleForestSingleDirectory.png)

Topologia najczęściej Hello jest pojedynczego lokalnego lasu z jednym lub wielu domen i jednej usługi Azure AD dzierżawy. Do uwierzytelniania usługi Azure AD synchronizacja haseł jest używany. Witaj instalacji ekspresowej programu Azure AD Connect obsługuje tylko tej topologii.

### <a name="single-forest-multiple-sync-servers-tooone-azure-ad-tenant"></a>Pojedynczy las, wiele dzierżawy usługi Azure AD tooone serwerów synchronizacji
![Nieobsługiwany topologia filtrowane do jednego lasu](./media/active-directory-aadconnect-topologies/SingleForestFilteredUnsupported.png)

Posiadanie wielu serwerów synchronizacji Azure AD Connect dzierżawy połączonych toohello tej samej usługi Azure AD nie jest obsługiwana, z wyjątkiem [przemieszczania serwera](#staging-server). Ma on nieobsługiwany, nawet jeśli te serwery są skonfigurowane toosynchronize wykluczają się wzajemnie zestaw obiektów. Użytkownik może mieć uznane za tej topologii Jeśli nie można uzyskać dostęp do wszystkich domen w lesie hello z jednego serwera lub jeśli chcesz toodistribute obciążenia między kilka serwerów.

## <a name="multiple-forests-single-azure-ad-tenant"></a>Wiele lasów, pojedynczy dzierżawy usługi Azure AD
![Topologia wiele lasów i pojedynczej dzierżawy](./media/active-directory-aadconnect-topologies/MultiForestSingleDirectory.png)

Organizacje często mają środowisk z wieloma lokalnymi lasami usługi Active Directory. Istnieją różne przyczyny mających więcej niż jednym lesie usługi Active Directory lokalnymi. Typowymi przykładami są projektów z zasobów konta lasów i hello wynik fuzji lub przejęcia.

Jeśli masz wiele lasów, wszystkich lasach musi być dostępny dla pojedynczego serwera synchronizacji Azure AD Connect. Nie masz toojoin powitania serwera tooa domeny. Jeśli to konieczne tooreach wszystkich lasach, serwer hello można umieścić w sieci obwodowej (również znane jako strefą zdemilitaryzowaną DMZ i podsiecią ekranowaną).

Kreator instalacji Hello Azure AD Connect zapewnia kilka opcji tooconsolidate użytkowników, którzy są reprezentowane w wielu lasach. Celem Hello jest, że użytkownik odpowiada tylko jeden raz w usłudze Azure AD. Brak skonfigurowanych w ścieżce instalacji niestandardowej powitania w Kreatorze instalacji hello typowych topologii. Na powitania **unikatowa identyfikacja użytkowników** strony hello wybierz odpowiednią opcję reprezentujący topologii. Konsolidacja Hello jest skonfigurowany tylko dla użytkowników. Zduplikowany grup nie są konsolidowane z hello domyślnej konfiguracji.

Popularne topologie omówiono w sekcji hello o [oddzielnych topologie](#multiple-forests-separate-topologies), [pełne siatki](#multiple-forests-full-mesh-with-optional-galsync), i [hello topologii zasobów konta](#multiple-forests-account-resource-forest).

Założono Hello domyślnej konfiguracji synchronizacji Azure AD Connect:

* Każdy użytkownik ma tylko jedno konto włączone, a las hello którym znajduje się to konto jest używane tooauthenticate hello użytkownika. Jest to założenie synchronizacji haseł i federacji. UserPrincipalName i sourceAnchor/nazwę immutableID pochodzą z tego lasu.
* Każdy użytkownik ma tylko jedną skrzynkę pocztową.
* Witaj lasu, który obsługuje hello pocztowej użytkownika ma hello najlepszą jakość danych dla atrybutów widoczne w hello globalne listy adresów (GAL) programu Exchange. Jeśli nie ma żadnych skrzynki pocztowej użytkownika hello, dowolnym lesie mogą być używane toocontribute te wartości atrybutów.
* Jeśli masz połączoną skrzynkę pocztową, istnieje również konto w innym lesie używane do logowania.

Jeśli środowisko nie jest zgodny z tych założeń, hello następujące to wiele problemów:

* Jeśli masz więcej niż jedno konto active lub więcej niż jedną skrzynkę pocztową, aparat synchronizacji hello wybiera jeden i ignoruje hello innych.
* Połączoną skrzynkę pocztową z żadnego aktywnego konta nie jest eksportowany tooAzure AD. Witaj, konto użytkownika nie jest reprezentowany jako element członkowski w dowolnej grupie. Połączoną skrzynkę pocztową w DirSync zawsze jest reprezentowany jako normalne skrzynki pocztowej. Ta zmiana jest celowo scenariusze wieloma lasami inaczej toobetter pomocy technicznej.

Szczegółowe informacje można znaleźć [opis hello domyślnej konfiguracji](active-directory-aadconnectsync-understanding-default-configuration.md).

### <a name="multiple-forests-multiple-sync-servers-tooone-azure-ad-tenant"></a>Wiele lasów, wiele dzierżawy usługi Azure AD tooone serwerów synchronizacji
![Nieobsługiwany topologii dla wielu serwerów synchronizacji i wiele lasów](./media/active-directory-aadconnect-topologies/MultiForestMultiSyncUnsupported.png)

O tooa podłączony serwer synchronizacji Azure AD Connect w więcej niż jeden pojedynczy dzierżawy usługi Azure AD nie jest obsługiwane. Witaj wyjątku jest użycie hello [przemieszczania serwera](#staging-server).

### <a name="multiple-forests-separate-topologies"></a>Wiele lasów, oddzielne topologii
![Opcja reprezentujących użytkowników tylko raz we wszystkich katalogach](./media/active-directory-aadconnect-topologies/MultiForestUsersOnce.png)

![Sceny wiele lasów i oddzielne topologii](./media/active-directory-aadconnect-topologies/MultiForestSeperateTopologies.png)

W tym środowisku wszystkich lasach lokalnych są traktowane jako osobne jednostki. Żaden użytkownik nie jest obecny w innym lesie. W każdym lesie jest jego własnej organizacji programu Exchange, i nie ma żadnych usługi GALSync między lasami hello. Ta topologia może być sytuacja powitania po połączeniu/nabycia lub w organizacji, których poszczególnych jednostek biznesowych działa niezależnie. Takich lasach znajdują się w hello tej samej organizacji w usłudze Azure AD i są wyświetlane z ujednoliconego usługi GAL. Każdy obiekt w każdym lesie hello poprzedzających obrazu, jest reprezentowany raz w magazynie metaverse hello i zagregowane w hello dzierżawy docelowej usługi Azure AD.

### <a name="multiple-forests-match-users"></a>Wiele lasów: dopasować użytkowników
Typowe tooall tych scenariuszy jest dystrybucji i grupy zabezpieczeń mogą zawierać zarówno użytkowników, kontaktów i obce podmioty zabezpieczeń (FSP). FSP są używane w elementach członkowskich toorepresent usług domenowych w usłudze Active Directory (AD DS) znajdujących się w innych lasach należących do grupy zabezpieczeń. Wszystkie FSP są toohello rozpoznać rzeczywistego obiektu w usłudze Azure AD.

### <a name="multiple-forests-full-mesh-with-optional-galsync"></a>Wiele lasów: pełne o usługi GALSync opcjonalne
![Opcja przy użyciu atrybutu wiadomości powitania do dopasowania, gdy tożsamości użytkowników istnieją w wielu katalogach](./media/active-directory-aadconnect-topologies/MultiForestUsersMail.png)

![Topologia pełnej sieci dla wielu lasów](./media/active-directory-aadconnect-topologies/MultiForestFullMesh.png)

Topologia pełnej sieci umożliwia użytkownikom i toobe zasobów znajdujących się w dowolnym lesie. Zazwyczaj istnieją dwukierunkowe relacje zaufania między lasami hello.

Jeśli programu Exchange znajduje się w więcej niż jednym lesie, mogą wystąpić (opcjonalnie) używane rozwiązanie lokalne usługi GALSync. Każdy użytkownik, następnie jest reprezentowany jako kontakt w innych lasach. Usługi GALSync często jest implementowane za pośrednictwem programu FIM 2010 lub MIM 2016. Azure AD Connect nie może służyć do lokalnej usługi GALSync.

W tym scenariuszu obiekty tożsamości są łączone za pomocą hello atrybut poczty. Użytkownik, który ma skrzynkę pocztową w jednym lesie jest połączony z kontaktów hello w hello innych lasach.

### <a name="multiple-forests-account-resource-forest"></a>Wiele lasów: lasu zasobów konta
![Opcji korzystania z funkcji hello atrybuty ObjectSID i msExchMasterAccountSID do dopasowania, gdy istnieją tożsamości w wielu katalogach](./media/active-directory-aadconnect-topologies/MultiForestUsersObjectSID.png)

![Topologia lasu zasobów konta dla wielu lasów](./media/active-directory-aadconnect-topologies/MultiForestAccountResource.png)

W topologii lasu zasobów dla konta, masz co najmniej jeden *konta* lasów z aktywne konta użytkowników. Masz również jedną lub więcej *zasobów* lasów z wyłączonych kont.

W tym scenariuszu jeden (lub więcej) lasu zasobów ufa wszystkich lasów kont. las zasobów Hello ma zwykle rozszerzony schemat usługi Active Directory z programem Exchange i usługi Lync. Usługi wszystkie programu Exchange i Lync, wraz z innych usług udostępnionych, znajdują się w tym lesie. Użytkownicy mają wyłączonego konta użytkownika, w tym lesie i skrzynek pocztowych hello jest połączony las kont toohello.

## <a name="office-365-and-topology-considerations"></a>Office 365 i zagadnienia dotyczące topologii
Niektórych obciążeń usługi Office 365 mają niektórych ograniczeń dotyczących obsługiwanych topologii:

| Obciążenie | Ograniczenia |
--------- | ---------
| Exchange Online | Jeśli istnieje więcej niż jednej lokalnej organizacji programu Exchange (oznacza to, Exchange został wdrożony toomore niż jednym lesie), należy użyć programu Exchange 2013 z dodatkiem SP1 lub nowszym. Aby uzyskać więcej informacji, zobacz [hybrydowych wdrożeń z wieloma lasami usługi Active Directory](https://technet.microsoft.com/library/jj873754.aspx). |
| Skype dla firm | Podczas korzystania z wieloma lokalnymi lasami, tylko topologią lasu zasobów konta hello jest obsługiwana. Aby uzyskać więcej informacji, zobacz [środowiska wymagania dla usługi Skype dla firm Server 2015](https://technet.microsoft.com/library/dn933910.aspx). |


## <a name="staging-server"></a>Serwer przemieszczania
![Przemieszczania serwer w topologii](./media/active-directory-aadconnect-topologies/MultiForestStaging.png)

Azure AD Connect obsługuje, instalacji drugiego serwera w *Tryb przejściowy*. Serwer, w tym trybie odczytuje dane ze wszystkich podłączonych katalogów, ale nie zapisuje niczego tooconnected katalogów. Używa cykl synchronizacji normalne hello, a w związku z tym ma zaktualizowanej kopii danych tożsamości hello.

Po awarii, gdy serwer podstawowy hello nie można przełączyć toohello przemieszczania serwera. Możesz to zrobić w hello Kreator Azure AD Connect. Ten drugi serwer może znajdować się w różnych centrach danych, ponieważ bez infrastruktury jest współużytkowany z serwera podstawowego hello. Należy ręcznie skopiować zmiany konfiguracji wprowadzone na powitania serwera podstawowego toohello drugiego serwera.

Możesz użyć przemieszczania tootest serwera nowy niestandardowej konfiguracji i hello efekt mającego na danych. Można wyświetlić podgląd zmian hello i dostosowania hello konfiguracji. Po zakończeniu modyfikowania hello nową konfigurację, możesz ustawić hello przemieszczania active powitania serwera, a hello starego tryb toostaging aktywnego serwera.

Umożliwia także ten serwer ActiveSync hello tooreplace metody. Przygotuj nowy serwer hello i ustaw tryb toostaging. Upewnij się, że jest w dobrym stanie, wyłącz (dzięki czemu active), Tryb przejściowy i zamknąć hello aktualnie aktywnego serwera.

Jest możliwe toohave więcej niż jeden serwer przemieszczania należy toohave wiele kopii zapasowych w różnych centrach danych.

## <a name="multiple-azure-ad-tenants"></a>Wiele dzierżaw usługi Azure AD
Zaleca się o pojedynczej dzierżawy w usłudze Azure AD dla organizacji.
Przed rozpoczęciem planowania toouse wiele dzierżaw usługi Azure AD, zobacz artykuł hello [Zarządzanie jednostkami administracyjnymi w usłudze Azure AD](../active-directory-administrative-units-management.md). Obejmuje on typowe scenariusze, w których można użyć pojedynczej dzierżawy.

![Topologia wiele lasów i wieloma dzierżawcami](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectory.png)

Istnieje relacja 1:1 między serwerem synchronizacji Azure AD Connect i dzierżawa usługi Azure AD. Dla każdego dzierżawcy usługi Azure AD należy jedna instalacja serwera synchronizacji Azure AD Connect. wystąpienia dzierżawy usługi Azure AD Hello są izolowane zgodnie z projektem. Oznacza to użytkownicy w jednej dzierżawy nie widzą użytkowników w hello innymi dzierżawami. Jeśli chcesz, aby ta separacja, jest obsługiwana konfiguracja. W przeciwnym razie należy użyć hello jednego modelu dzierżawy usługi Azure AD.

### <a name="each-object-only-once-in-an-azure-ad-tenant"></a>Każdy obiekt tylko raz w dzierżawie usługi Azure AD
![Filtrowane topologii w przypadku pojedynczego lasu](./media/active-directory-aadconnect-topologies/SingleForestFiltered.png)

W tej topologii dzierżawy tooeach podłączonej usługi Azure AD jest jeden serwer synchronizacji Azure AD Connect. serwery synchronizacji Azure AD Connect Hello musi być skonfigurowany w celu filtrowania tak, aby każdy miał wykluczają się wzajemnie zestaw obiektów toooperate. Można na przykład zakres każdego serwera tooa określonej domeny lub jednostki organizacyjnej.

Domena DNS może być zarejestrowany w tylko jednej dzierżawy usługi Azure AD. Hello nazwy UPN użytkowników hello w wystąpieniu usługi Active Directory lokalne powitania również należy użyć oddzielnych przestrzeni nazw. Na przykład w hello poprzedzających obraz, trzech oddzielnych sufiksy są rejestrowane w wystąpieniu usługi Active Directory lokalne powitania: contoso.com, fabrikam.com i nadrzędnych. Użytkownicy Hello w każdej domenie usługi Active Directory lokalnymi używać różnych przestrzeni nazw.

Między wystąpieniami dzierżawy usługi Azure AD hello nie istnieje żadne usługi GALSync. Witaj książki adresowej w usłudze Exchange Online i Skype dla firm pokazuje tylko do użytkowników w hello tej samej dzierżawy.

Ta topologia ma hello następujące ograniczenia w inny sposób obsługiwane scenariusze:

* Tylko jeden dzierżaw hello Azure AD można włączyć hybrydowym programu Exchange z hello lokalnego wystąpienia usługi Active Directory.
* Urządzenia z systemem Windows 10 można skojarzyć z tylko jedną dzierżawy usługi Azure AD.
* Hello pojedynczego logowania jednokrotnego (SSO) opcji dla uwierzytelniania przekazywanego i synchronizacji haseł można użyć z tylko jedną dzierżawy usługi Azure AD.

wymaganie Hello wykluczają się wzajemnie zestawu obiektów dotyczy również toowriteback. Niektóre funkcje zapisywania zwrotnego nie są obsługiwane z tej topologii, ponieważ zakładają konfiguracji pojedynczym lokalnym. Te funkcje obejmują:

* Grupa zapisywania zwrotnego z konfiguracji domyślnej.
* Zapisywanie zwrotne urządzeń.

### <a name="each-object-multiple-times-in-an-azure-ad-tenant"></a>Każdy obiekt wiele razy w dzierżawie usługi Azure AD
![Nieobsługiwany topologii dla jednego lasu i wieloma dzierżawcami](./media/active-directory-aadconnect-topologies/SingleForestMultiDirectoryUnsupported.png) ![Nieobsługiwany topologii dla jednego lasu i wiele łączników](./media/active-directory-aadconnect-topologies/SingleForestMultiConnectorsUnsupported.png)

Te zadania nie są obsługiwane:

* Witaj synchronizacji, sam dzierżaw usługi Azure AD toomultiple użytkownika.
* Wprowadź zmiany użytkowników w jednej dzierżawy usługi Azure AD będą wyświetlane jako kontakty w innej dzierżawie usługi Azure AD konfiguracji.
* Zmodyfikuj dzierżaw usługi Azure AD toomultiple tooconnect synchronizacji Azure AD Connect.

### <a name="galsync-by-using-writeback"></a>Usługi GALSync przy użyciu zapisywania zwrotnego
![Nieobsługiwany topologii wiele lasów i wiele katalogów, z usługi GALSync koncentrujących się na usługę Azure AD](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync1Unsupported.png) ![Nieobsługiwany topologii wiele lasów i wiele katalogów, z usługi GALSync koncentrujących się na lokalnej usługi Active Directory](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync2Unsupported.png)

Dzierżaw usługi Azure AD są izolowane zgodnie z projektem. Te zadania nie są obsługiwane:

* Zmienianie konfiguracji hello danych tooread synchronizacji Azure AD Connect z innej dzierżawy usługi Azure AD.
* Eksportuj użytkowników jako kontakty tooanother lokalnej usługi Active Directory wystąpienia za pomocą synchronizacji usługi Azure AD Connect.

### <a name="galsync-with-on-premises-sync-server"></a>Usługi GALSync z lokalnego serwera synchronizacji
![Usługi GALSync w topologii wiele lasów i wielu katalogów](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync.png)

Możesz użyć programu FIM 2010 lub MIM 2016 toosync użytkowników lokalnych (przy użyciu usługi GALSync) między dwiema organizacjami Exchange. Użytkownicy Hello w jednej z organizacji są wyświetlane jako obcego użytkowników/contacts w hello z innej organizacji. Te różne lokalnej usługi Active Directory wystąpień mogą następnie zostać zsynchronizowany z własnych dzierżaw usługi Azure AD.

## <a name="next-steps"></a>Następne kroki
toolearn tooinstall Azure AD Connect dotyczących następujących scenariuszy, zobacz temat [Instalacja niestandardowa programu Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

Dowiedz się więcej o hello [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.

Dowiedz się więcej o [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
