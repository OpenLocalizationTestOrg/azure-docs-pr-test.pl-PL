---
title: aaaIsolation w hello chmury publicznej Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat przetwarzania danych usług w chmurze zawierających szeroką gamę wystąpienia obliczeniowe i usług, które można skalować w górę i w dół automatycznie toomeet hello potrzeb aplikacji lub przedsiębiorstwa."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 271e5f0d00abcfd404ce6c50cfb7d1ac26360c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="isolation-in-hello-azure-public-cloud"></a>Izolacja w hello Azure chmury publicznej
##  <a name="introduction"></a>Wprowadzenie
### <a name="overview"></a>Omówienie
informacje o tooassist aktualnych i potencjalnych klientów platformy Azure i wykorzystywać hello różnych funkcjach zabezpieczeń dostępnych w i otaczającego je hello platformy Azure, firma Microsoft opracowała serii oficjalne dokumenty, omówienie zabezpieczeń, najlepsze rozwiązania i Listy kontrolne.
Tematy Hello zakresu pod względem szerokości i głębokość i są okresowo aktualizowane. Ten dokument jest częścią tej serii, zgodnie z opisem w sekcji abstrakcyjny powitania po.

### <a name="azure-platform"></a>Platformy Azure
Azure to platforma usługi chmury Otwórz i elastyczne, która obsługuje hello wybór najszerszych systemów operacyjnych, programowania języków, struktury, narzędzia, baz danych i urządzeń. Można na przykład:
- Uruchom kontenery Linux z integracją rozwiązania Docker;
- Tworzenie aplikacji za pomocą języka JavaScript, Python, .NET, PHP, Java i Node.js; i
- Kompilacja zapleczy dla systemu iOS, Android i Windows urządzeń.

Microsoft Azure obsługuje hello już polegać na tej samej technologii miliony deweloperów i specjalistów IT i zaufania.

Podczas tworzenia lub migracji zasobów informatycznych do dostawcy usług w chmurze publicznej, są zależne tooprotect możliwości organizacji w aplikacji i danych za pomocą hello kontroli usług i hello zapewniają toomanage hello bezpieczeństwa sieci opartej na chmurze zasoby.

Zaprojektowano infrastruktury platformy Azure z tooapplications zakładzie hello jednocześnie hostingu miliony klientów i zapewnia foundation godne zaufania, na którym firmy mogą ich potrzeb zabezpieczeń. Ponadto Azure zapewnia szereg zabezpieczeń można skonfigurować opcje i hello toocontrol możliwości ich, dzięki czemu można dostosować toomeet hello unikatowe wymagania dotyczące zabezpieczeń wdrożeń. Ten dokument pomaga spełnić te wymagania.

### <a name="abstract"></a>Abstrakcyjny

Microsoft Azure pozwala aplikacji toorun, maszynach wirtualnych (VM) na bazie infrastruktury fizycznej udostępnionego. Jedna z aplikacji toorunning motywacji gospodarczej główne hello w środowisku chmury jest hello możliwości toodistribute hello koszt zasobów udostępnionych między wielu klientów. To rozwiązanie dotyczące obsługi wielu dzierżawców zwiększa wydajność przez multipleksowania zasobów między różnymi klientów przy niskich kosztach. Niestety również wprowadza ryzyko hello udostępniania serwerów fizycznych i innych toorun zasobów infrastruktury poufnych aplikacji i maszyn wirtualnych, które mogą należeć tooan dowolnego i potencjalnie złośliwy użytkownik.

W tym artykule opisano, jak Microsoft Azure zapewnia izolację zarówno złośliwe i złośliwych użytkowników i służy jako przewodnik dla projektowania rozwiązań w chmurze, oferując różnych tooarchitects opcji izolacji. Ten dokument koncentruje się na powitania technologii platformy Azure i opcji zabezpieczeń umożliwiających dostęp klienta i nie będzie podejmował tooaddress SLA cennik modeli i zagadnienia dotyczące praktyki DevOps.

## <a name="tenant-level-isolation"></a>Poziom izolacji dzierżawców
Jedną z zalet głównej hello chmura obliczeniowa koncepcji udostępnionego, wspólnej infrastruktury przez wielu klientów jednocześnie, początkowe tooeconomies skali. To pojęcie jest nazywane obsługi wielu dzierżawców. Microsoft stale pracuje tooensure, że architektura wielodostępnej hello Microsoft chmury Azure obsługuje standardów zabezpieczeń, poufność zachowania poufności, integralności i dostępności.

W pracy z włączoną obsługę chmury hello dzierżawcy można zdefiniować jako klienta lub organizacja, która jest właścicielem i określone wystąpienie danej usługi w chmurze. Z platformą tożsamości hello udostępniane przez Microsoft Azure dzierżawa to po prostu dedykowane wystąpienie usługi Azure Active Directory (Azure AD), który organizacja otrzymuje i posiada po zarejestrowaniu się do usługi w chmurze firmy Microsoft.

Każdy katalog usługi Azure AD jest odrębny i oddzielony od innych katalogów usługi Azure AD. Podobnie jak budynek biurowy jest tooonly określonych zabezpieczonym zasobem organizacji, katalog usługi Azure AD został również toobe zaprojektowany jako zabezpieczony zasób do użytku tylko Twojej organizacji. Architektura usługi Azure AD Hello izoluje klienta dane i informacje o tożsamości przez zmieszaniem. Oznacza to, że użytkownicy i administratorzy jednego katalogu usługi Azure AD nie mogą przypadkowo ani złośliwie uzyskać dostępu do danych w innym katalogu.

### <a name="azure-tenancy"></a>Dzierżawy usługi Azure
Dzierżawy Azure (Azure Subscription) odwołuje się relacja "odbiorcy/billing" tooa i unikatowego [dzierżawy](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant) w [usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis). Poziom izolacji dzierżawców w Microsoft Azure jest osiągane przy użyciu usługi Azure Active Directory i [opartej na rolach kontroli](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) oferowane przez nią. Każda subskrypcja platformy Azure jest skojarzony z jednego katalogu usługi Azure Active Directory (AD).

Użytkownicy, grupy i aplikacje z katalogu mogą zarządzać zasobami w hello subskrypcji platformy Azure. Można przypisać te prawa dostępu przy użyciu hello portalu Azure, narzędzi wiersza polecenia platformy Azure i interfejsów API zarządzania platformy Azure. Dzierżawa usługi Azure AD jest logicznie odizolowane za pomocą granic zabezpieczeń, dzięki czemu klienta można uzyskać dostępu do lub naruszyć wspólnej dzierżaw złośliwe lub przypadkowo. Usługi Azure AD jest uruchamiany na serwerach "od zera" izolowany w segmencie sieci rozdzielone, gdzie filtrowanie pakietów na poziomie hosta i zapory systemu Windows blokować ruchu i niechciane połączenia.

- Toodata dostępu w usłudze Azure AD wymaga uwierzytelnienia użytkownika za pośrednictwem [usługi tokenu zabezpieczającego (STS)](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization). Informacje dotyczące istnienia, włączona i roli użytkownika hello jest używany przez hello autoryzacji systemu toodetermine czy hello żądany dostęp toohello docelowej dzierżawy jest autoryzowany do tego użytkownika w tej sesji.

![Dzierżawy usługi Azure](./media/azure-isolation/azure-isolation-fig1.png)


- Dzierżaw są kontenerami odrębny i nie ma żadnych zależności między tymi.

- Brak dostępu między dzierżawy, chyba że administrator dzierżawy spowoduje przyznanie za pośrednictwem federacyjnego lub inicjowania obsługi administracyjnej kont użytkowników z innych dzierżawców.

- Tooservers fizycznego dostępu, która obejmuje usługi hello Azure AD i systemy bezpośredni dostęp do zaplecza tooAzure przez usługi AD jest ograniczone.

- Azure AD użytkownicy mają nie dostępu toophysical zasobów lub lokalizacji, a w związku z tym nie jest możliwe ich toobypass hello RBAC zasad testy logiczne podać następujące.

Diagnostyka i konserwacyjnych modelu operacyjnego infrastruktury używającego systemu podniesienia uprawnień w czasie jest wymagany i używać. Azure AD Privileged Identity Management (PIM) wprowadzono pojęcie hello kwalifikujących się uprawnień administratora. [Administratorzy kwalifikujących się](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure) powinna być użytkowników, które wymagają uprzywilejowanego dostępu teraz, a następnie, ale nie każdego dnia. Rola Hello jest nieaktywny, dopóki hello użytkownik będzie potrzebował dostępu, a następnie zakończyć proces aktywacji i stają się aktywne administratora dla wstępnie określoną ilość czasu.

![Azure AD Privileged Identity Management](./media/azure-isolation/azure-isolation-fig2.png)

Usługa Azure Active Directory obsługuje każdego dzierżawcy w jego własnej chronionych kontenerze z tooand zasad i uprawnień w kontenerze hello wyłącznie własnością i zarządzane przez dzierżawcę hello.

koncepcja Hello kontenerów dzierżawy jest głęboko ingrained w usłudze katalogowej hello na wszystkich warstwach, z portali wszystkie hello sposób toopersistent magazynu.

Nawet wtedy, gdy metadane z wieloma dzierżawcami usługi Azure Active Directory są przechowywane na hello sam fizycznego dysku, nie ma żadnych zależności między kontenery hello innych niż to, co jest definiowana za pomocą usługi katalogowej hello, który z kolei jest zależna hello administratora dzierżawy.

### <a name="azure-role-based-access-control-rbac"></a>Kontrola dostępu oparta na rolach na platformie Azure (RBAC)
[Azure opartej na rolach kontroli dostępu (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) pomaga różnych składników dostępnych w ramach subskrypcji platformy Azure możesz tooshare zapewniając precyzyjne zarządzanie dostępem dla platformy Azure. Azure RBAC umożliwia toosegregate opłat w ramach organizacji i Udziel dostępu oparte na jakie użytkownicy muszą tooperform swoich zadań. Zamiast nadanie każdy nieograniczonych uprawnień w subskrypcji platformy Azure lub zasobów, można zezwolić tylko pewne akcje.

Azure RBAC ma trzy podstawowe role dotyczące typów zasobów tooall:

- **Właściciel** ma pełny dostęp tooall zasobów, w tym hello toodelegate prawo dostępu tooothers.

- **Współautor** można tworzyć i zarządzania wszystkimi typami zasobów platformy Azure, ale nie może udzielić dostępu tooothers.

- **Czytnik** można wyświetlić istniejących zasobów platformy Azure.

![Kontrola dostępu oparta na rolach na platformie Azure](./media/azure-isolation/azure-isolation-fig3.png)

Zezwalaj na zarządzanie określonych zasobów platformy Azure Hello pozostałe role RBAC hello na platformie Azure. Na przykład hello roli współautora maszyny wirtualnej umożliwia hello toocreate użytkowników i zarządzania maszynami wirtualnymi. Nie daje im toohello dostępu do sieci wirtualnej platformy Azure lub łączy się z podsieci hello, która hello maszyny wirtualnej.

[Wbudowane role RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) listy ról hello dostępnej na platformie Azure. Określa operacje hello i że każdy wbudowana rola przyznaje toousers zakresu. Jeśli szukasz toodefine własne role, aby uzyskać większą kontrolę, zobacz temat jak toobuild [niestandardowych ról w Azure RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles).

Niektóre inne możliwości usługi Azure Active Directory obejmują:
- Usługi Azure AD umożliwia aplikacjom tooSaaS logowania jednokrotnego, niezależnie od tego, gdzie są obsługiwane. Niektóre aplikacje są sfederowane z usługą Azure AD, a inne korzystają z logowania jednokrotnego z użyciem hasła. Aplikacji federacyjnych można również obsługę użytkowników i [archiwizowanie haseł](https://www.techopedia.com/definition/31415/password-vault).

- Toodata dostępu w [usługi Azure Storage](https://azure.microsoft.com/services/storage/) jest kontrolowany przez uwierzytelniania. Każde konto magazynu ma klucza podstawowego ([klucz konta magazynu](https://docs.microsoft.com/azure/storage/storage-create-storage-account), lub SAK) i klucz tajny pomocniczy (sygnatury dostępu współdzielonego hello lub SAS).

- Usługa Azure AD zapewnia jako usługi przy użyciu federacji tożsamości za pomocą [Active Directory Federation Services](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-azure-adfs), synchronizacji i replikacji z lokalnymi katalogami.

- [Usługa Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) jest hello usługi Multi-Factor authentication, który wymaga logowania tooverify użytkowników przy użyciu aplikacji mobilnej, połączenia telefonicznego lub wiadomości SMS. Można go przy użyciu usługi Azure AD toohelp bezpieczną lokalną zasobów z serwera usługi Azure Multi-Factor Authentication hello, a także z niestandardowych aplikacji i katalogów przy użyciu hello zestawu SDK.

- [Usługi domenowe Azure AD](https://azure.microsoft.com/services/active-directory-ds/) umożliwia dołączenie bez wdrażania kontrolerów domeny w domenie usługi Active Directory tooan maszyn wirtualnych platformy Azure. Można zalogować toothese maszyn wirtualnych za pomocą firmowych poświadczeń usługi Active Directory i administrować przyłączonych do domeny maszyn wirtualnych przy użyciu plany bazowe zabezpieczeń tooenforce zasad grupy na wszystkich maszyn wirtualnych platformy Azure.

- [Usługa Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) zapewnia usługę wysokiej dostępności zarządzania globalne tożsamości dla aplikacji dla użytkowników, która może obsłużyć toohundreds milionów tożsamości. Można ją łatwo integrować z platformami mobilnymi i platformami sieci Web. Użytkownicy mogą rejestrować w tooall aplikacji za pomocą środowiska można dostosować przy użyciu istniejących kont społecznościowych lub przez tworzenie poświadczeń.

### <a name="isolation-from-microsoft-administrators--data-deletion"></a>Izolacja Administratorzy usługi Microsoft & usunięcia danych z
Microsoft przyjmuje tooprotect Silne środki danych z niewłaściwego dostępu lub używany przez osoby nieupoważnione. Te procesy operacyjne i formanty bazują na powitania [warunki dotyczące usług Online](http://aka.ms/Online-Services-Terms), które oferują umownymi kwota zobowiązania, które kontrolują dostęp do danych tooyour.

-   Pracownicy firmy Microsoft nie ma domyślnego dostępu tooyour danych w chmurze hello. Zamiast tego otrzyma dostęp, w obszarze zarządzania nadzoru, tylko wtedy, gdy jest to konieczne. Program access jest dokładnie kontrolowany i rejestrowane i odwoływane, gdy nie jest już potrzebne.

-   Microsoft może zatrudnienia innych firm usług tooprovide ograniczone w jej imieniu. Podwykonawców firmy Microsoft może uzyskać dostępu do klienta tylko toodeliver hello usług danych, które firma Microsoft wynajmuje je tooprovide i nie wolno im wykorzystywać ich w jakimkolwiek innym celu. Co więcej są one toomaintain na podstawie umowy powiązanej hello poufności informacji dotyczących klientów.

Usługi biznesowe z inspekcji Certyfikaty takie jak ISO/IEC 27001 regularnie są weryfikowane przez firmę Microsoft i akredytowane inspekcji przedsiębiorstw, które wykonaj przykładowe tooattest inspekcji tej dostęp tylko do celów biznesowych uzasadnione. Można zawsze dostęp do danych klienta w dowolnym momencie z dowolnej przyczyny.

Po usunięciu wszystkich danych Microsoft Azure usuwa dane hello, w tym wszystkie kopie pamięci podręcznej lub kopii zapasowej. W przypadku usług-scope usunięcia tego zostanie przeprowadzona w ciągu 90 dni, po zakończeniu okresu przechowywania hello hello. (W zakresie usług są zdefiniowane w sekcji warunków przetwarzania danych hello naszych [warunki dotyczące usług Online](http://aka.ms/Online-Services-Terms).)

Jeśli dysk używany do magazynowania wystąpi awaria sprzętu, jest bezpiecznie [usunięte lub zniszczone](https://www.microsoft.com/trustcenter/Privacy/You-own-your-data) przed Microsoft zwraca producenta toohello dla zastąpienia lub naprawy. Witaj danych na dysku hello jest zastępowany tooensure, który hello danych nie można odzyskać w jakikolwiek sposób.

## <a name="compute-isolation"></a>Obliczenia bazy danych izolacji
Microsoft Azure oferuje różne przetwarzania danych usług w chmurze zawierających szeroką gamę wystąpienia obliczeniowe i usług, które można skalować w górę i w dół automatycznie toomeet hello potrzeb aplikacji lub enterprise. Te wystąpienia obliczeniowe i usługi zapewniają izolację na wielu poziomach toosecure danych bez ograniczania hello elastyczność w konfiguracji tego zapotrzebowania klientów.

### <a name="hyper-v--root-os-isolation-between-root-vm--guest-vms"></a>Funkcji Hyper-V & głównego izolacji systemu operacyjnego między główny maszyn wirtualnych i maszyn wirtualnych gościa
Platforma obliczeniowa platformy Azure jest oparta na maszynie wirtualizacji, co oznacza, że cały kod klienta jest wykonywana na maszynie wirtualnej funkcji Hyper-V. Na każdym węźle Azure (lub punktu końcowego sieci) Brak funkcji Hypervisor, która uruchamia bezpośrednio przez hello sprzętu i dzieli węzła numer zmiennej o maszynach wirtualnych gościa (VM).


![Funkcji Hyper-V & głównego izolacji systemu operacyjnego między główny maszyn wirtualnych i maszyn wirtualnych gościa](./media/azure-isolation/azure-isolation-fig4.jpg)


Każdy węzeł ma również jedną specjalne głównego maszynę Wirtualną, uruchamianego hello systemu operacyjnego hosta. Krytyczne granic jest izolacji hello hello głównych maszyny Wirtualnej z gościa hello maszyn wirtualnych i hello gościa maszyn wirtualnych od siebie, zarządza hello funkcji hypervisor i hello katalog główny systemu operacyjnego. parowanie funkcji hypervisor/root systemu operacyjnego Hello wykorzystuje dekad firmy Microsoft środowisko zabezpieczeń systemu operacyjnego i uczenie nowsza od firmy Microsoft Hyper-V, silne izolacji tooprovide maszyn wirtualnych gościa.

Witaj platformy Azure używa środowisku wirtualnym. Wystąpienia użytkownika działać jako autonomiczne maszyny wirtualne, które nie mają dostępu tooa serwera fizycznego hosta i Izolacja jest wymuszana za pomocą procesora fizycznego poziomy uprawnień (pierścień-0/pierścień-3).

Pierścień 0 jest hello najbardziej uprzywilejowanych i 3 jest najmniej hello. system operacyjny gościa Hello działa w 1 pierścień mniejszym uprzywilejowanego, i aplikacje są uruchamiane w hello najniższych uprawnieniach 3 pierścień. Ta wirtualizacji zasoby fizyczne prowadzi tooa wyraźnej separacji między funkcji hypervisor, co spowoduje rozdzielenie dodatkowe zabezpieczenia hello dwa i system operacyjny gościa.

Hello Azure funkcji hypervisor działa jak jądra i przekazuje wszystkie żądania dostępu do sprzętu z hosta toohello maszyn wirtualnych gościa dla przetwarzania przy użyciu interfejsu pamięci współużytkowanej, nazywany magistralę maszyny wirtualnej. Uniemożliwia użytkownikom uzyskiwanie dostępu odczytu/zapisu/wykonania surowego toohello systemu i zmniejsza ryzyko hello udostępnianie zasobów systemowych.

### <a name="advanced-vm-placement-algorithm--protection-from-side-channel-attacks"></a>Zaawansowane algorytm umieszczania maszyny Wirtualnej i ochronę przed atakami kanału po stronie
Atakiem maszyny Wirtualnej między wymaga wykonania dwóch kroków: wprowadzania kontrolowane atakujący dokonuje maszyny Wirtualnej na powitania sam host wśród ofiara hello maszyn wirtualnych i mogą spowodować tooeither granic izolacji hello wykradać informacje poufne ofiara lub spowolnić Chciwość lub vandalism. Microsoft Azure zapewnia ochronę w obu czynności przy użyciu zaawansowanych algorytm umieszczania maszyny Wirtualnej i ochronę przed atakami wszystkie znane po stronie kanał tym zakłócenia sąsiada maszyn wirtualnych.

### <a name="hello-azure-fabric-controller"></a>Witaj Kontroler sieci szkieletowej Azure
Hello Kontroler sieci szkieletowej Azure jest odpowiedzialny za przydzielanie zasobów infrastruktury tootenant obciążeń i zarządza jednokierunkowe komunikacji z hello hosta toovirtual maszyn. Hello maszyny Wirtualnej wprowadzanie algorytmem kontrolera sieci szkieletowej Azure hello jest bardzo zaawansowane i prawie niemożliwe toopredict jako poziomie hosta fizycznego.

![Witaj Kontroler sieci szkieletowej Azure](./media/azure-isolation/azure-isolation-fig5.png)

Hello Azure funkcji hypervisor wymusza pamięci i oddzielenie procesu maszyny wirtualnej, a bezpiecznie kieruje dzierżaw tooguest OS ruchu sieciowego. Eliminuje to możliwość i po stronie kanał ataku na poziomie maszyny Wirtualnej.

Na platformie Azure hello głównej maszyny Wirtualnej jest szczególna: działa ze wzmocnionymi zabezpieczeniami systemu operacyjnego o nazwie hello głównego systemu operacyjnego obsługującego agenta sieci szkieletowej (FA). FAs są używane w Włącz toomanage agentów gości (GA) w ramach systemów operacyjnych gościa, na klienta maszyn wirtualnych. FAs również zarządzać węzłów magazynu.

Witaj kolekcji Azure funkcji hypervisor, główny systemu operacyjnego/FA, i klienta maszyn wirtualnych lub gazu obejmuje węźle obliczeń. FAs są zarządzane przez kontroler sieci szkieletowej (FC), która istnieje poza węzłów obliczeniowych i przestrzeni dyskowej (klastrów obliczeniowych i magazynów są zarządzane przez oddzielne FCs). Jeśli klient aktualizuje plik konfiguracji ich stosowania jest uruchomiona, hello FC komunikuje się z hello FA, skontaktuje się następnie gazu, który powiadamia aplikacji hello hello zmiany konfiguracji. W przypadku hello awarii sprzętu hello FC zostanie automatycznie znaleźć dostępnego sprzętu i uruchom ponownie hello maszyna wirtualna istnieje.

![Kontroler sieci szkieletowej Azure](./media/azure-isolation/azure-isolation-fig6.jpg)

Komunikacji z agentem tooan kontrolera sieci szkieletowej jest jednokierunkowa. Hello agent implementuje usługi zabezpieczonego protokołem SSL tylko odpowiadający toorequests od hello kontrolera. Go nie można zainicjować połączenia toohello kontrolera lub inne węzły wewnętrzny uprzywilejowanych. Hello FC traktuje wszystkie odpowiedzi, tak jakby były niezaufanych.


![Kontroler sieci szkieletowej](./media/azure-isolation/azure-isolation-fig7.png)

Izolacja rozciąga się od hello wirtualna głównego z maszyn wirtualnych gościa i hello gościa maszyn wirtualnych od siebie nawzajem. Obliczeń węzły również są odizolowane od węzłów magazynu w celu zwiększenia ochrony.


Hello funkcji hypervisor i systemu operacyjnego hosta hello zapewniają pakietów sieciowych — filtry toohelp mieć pewność, że niezaufane maszyn wirtualnych nie może generować fałszywych ruch lub odbierania ruchu kierowanego nie toothem, punkty końcowe infrastruktury tooprotected bezpośredniego ruchu lub wysyłania i odbierania niewłaściwe ruch emisji.


### <a name="additional-rules-configured-by-fabric-controller-agent-tooisolate-vm"></a>Dodatkowe zasady skonfigurowane przez tooIsolate agenta kontrolera sieci szkieletowej maszyny Wirtualnej
Domyślnie cały ruch jest zablokowany, po utworzeniu maszyny wirtualnej i skonfiguruje agenta kontrolera sieci szkieletowej hello hello pakietów filtru tooadd regułami i wyjątkami tooallow autoryzowany ruchu.

Istnieją dwie kategorie reguł zaprogramowane:

-   **Reguły konfiguracji lub infrastruktury maszyny:** domyślnie cała komunikacja jest zablokowany. Są wyjątki tooallow toosend maszyny wirtualnej i odbierać dane DHCP i DNS. Maszyny wirtualne można również wysyłać ruch toohello "public" internet i wysyłania ruchu tooother maszyn wirtualnych w ramach hello tej samej sieci wirtualnej platformy Azure i hello Serwer aktywacji systemu operacyjnego. maszyny wirtualne Hello listy dozwolonych wychodzących miejsc docelowych nie ma podsieci Azure routera, zarządzania platformy Azure i inne właściwości firmy Microsoft.

-   **Plik konfiguracji roli:** definiuje hello przychodzących dostępu kontroli zawiera listę (kontroli dostępu ACL) oparte na modelu usługi hello dzierżawy.

### <a name="vlan-isolation"></a>Izolacja sieci VLAN
W każdym klastrze istnieją trzy sieci VLAN:

![Izolacja sieci VLAN](./media/azure-isolation/azure-isolation-fig8.jpg)


-   Witaj głównego sieci VLAN — połączeń węzłach niezaufanych klienta

-   Witaj FC sieci VLAN — zawiera zaufanych FCs i systemów pomocniczych

-   Witaj urządzenia sieci VLAN — zawiera zaufanych sieci i innych urządzeniach infrastruktury

Komunikacja jest dozwolony z toohello FC VLAN hello VLAN głównego, ale nie można zainicjować z hello głównego sieci VLAN toohello FC w sieci VLAN. Komunikacja również jest zablokowana z hello głównego sieci VLAN toohello urządzenia sieci VLAN. Gwarantuje to, że nawet wtedy, gdy węzeł uruchamiania kodu klienta zostanie naruszony, go nie ataki węzłów na powitania FC lub urządzenie sieci VLAN.

## <a name="storage-isolation"></a>Izolacja magazynu
### <a name="logical-isolation-between-compute-and-storage"></a>Logiczne izolację między zasobów obliczeniowych i magazynu
W ramach podstawowych projekt Microsoft Azure oddziela obliczeń na podstawie maszyny Wirtualnej z magazynu. Ta separacja umożliwia obliczeń i magazynowania tooscale niezależnie, łatwiejsze wielodostępność tooprovide i izolacji, co.

W związku z tym magazynu Azure działa na oddzielnego sprzętu z nie tooAzure łączności sieciowej obliczania, z wyjątkiem logicznie. [To](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf) oznacza, że podczas tworzenia dysku wirtualnego przydzielenie miejsca na dysku nie dla całego pojemności. Zamiast tego utworzeniu tabeli, która mapuje adresy na powitania tooareas wirtualnego dysku na dysk fizyczny hello i ta tabela jest początkowo pusta. **powitania klienta zapisuje dane na wirtualnym dysku hello jest przydzielone miejsce na dysku fizycznym hello i tooit wskaźnik myszy znajduje się w tabeli powitania po raz pierwszy.**
### <a name="isolation-using-storage-access-control"></a>Kontrola dostępu do magazynu przy użyciu izolacji
**Kontrola dostępu w usłudze Azure Storage** ma model kontroli dostępu za pomocą prostego. Każda subskrypcja platformy Azure można utworzyć co najmniej jedno konto magazynu. Każde konto magazynu ma pojedynczy klucz tajny, który jest używany toocontrol dostępu tooall dane na tym koncie magazynu.

![Kontrola dostępu do magazynu przy użyciu izolacji](./media/azure-isolation/azure-isolation-fig9.png)

**Dostęp do tooAzure magazynu danych (łącznie z tabelami)** można sterować za pośrednictwem [SAS (Shared Access Signature)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) token, który przyznaje zakres dostępu. Hello SAS jest tworzony przy użyciu szablonu zapytania (URL), podpisany hello [SAK (klucz konta magazynu)](https://msdn.microsoft.com/library/azure/ee460785.aspx). Który [podpisany adresu URL](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) można przydzielić tooanother procesu (który delegowane), który może, a następnie wypełnij szczegóły hello hello zapytania i Utwórz Żądanie hello hello usługi magazynu. Sygnatury dostępu Współdzielonego umożliwia tooclients dostępu na podstawie czasu toogrant bez ujawniania konta magazynu hello klucz tajny.

Hello SAS oznacza, że możemy udzielić się, że klient ograniczonych uprawnieniach, tooobjects w nasze konto magazynu w określonym przedziale czasu i z określonym zestawem uprawnień. Udzielamy uprawnieniami ograniczonymi według powyższego bez konieczności tooshare klucze dostępu do Twojego konta.

### <a name="ip-level-storage-isolation"></a>IP magazynu poziomu izolacji
Można ustanowić zapory i zdefiniować zakres adresów IP dla zaufanych klientów. Z zakresu adresów IP tylko klientów, którzy mają adres IP zakresu hello zdefiniowane można połączyć za[usługi Azure Storage](https://docs.microsoft.com/azure/storage/storage-security-guide).

IP magazynu danych mogą być chronione przed nieautoryzowanymi użytkownikami za pomocą mechanizmu sieci używanych tooallocate dedykowanej lub dedykowanych tunelu ruchu tooIP magazynu.

### <a name="encryption"></a>Szyfrowanie
Platforma Azure oferuje następujące typy danych tooprotect szyfrowania:
-   Szyfrowanie podczas przesyłania

-   Szyfrowanie w spoczynku

#### <a name="encryption-in-transit"></a>Szyfrowanie podczas przesyłania
Szyfrowanie podczas przesyłania jest mechanizm ochrony danych podczas ich przesyłania w sieciach. Z usługą Azure Storage można zabezpieczyć dane przy użyciu:

-   [Szyfrowanie na poziomie transportu](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit), taki jak HTTPS podczas transferu danych do i z usługi Azure Storage.

-   [Połączenie szyfrowania](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), takimi jak szyfrowanie protokołu SMB 3.0 udziałów plików Azure.

-   [Szyfrowanie po stronie klienta](https://docs.microsoft.com/azure/storage/storage-security-guide#using-client-side-encryption-to-secure-data-that-you-send-to-storage), tooencrypt hello danych, zanim zostanie przekazany do magazynu i toodecrypt danych powitania po przeniesieniu poza magazynu.

#### <a name="encryption-at-rest"></a>Szyfrowanie magazynowanych
W przypadku wielu organizacji [szyfrowanie danych magazynowanych](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) jest obowiązkowy krok na drodze danych suwerenności prywatności, zgodności i danych. Istnieją trzy funkcje platformy Azure, które zapewniają szyfrowania danych, która jest "w stanie spoczynku":

-   [Szyfrowanie usługi Magazyn](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-at-rest) pozwala toorequest, że Usługa magazynu hello automatycznie szyfrowania danych podczas jej pisania tooAzure magazynu.

-   [Szyfrowanie po stronie klienta](https://docs.microsoft.com/azure/storage/storage-security-guide#client-side-encryption) oferuje także funkcję hello szyfrowania w stanie spoczynku.

-   [Szyfrowanie dysków Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) tooencrypt dysków hello systemu operacyjnego i dysków danych używanych przez maszyny wirtualne IaaS.

#### <a name="azure-disk-encryption"></a>Usługa Azure Disk Encryption
[Szyfrowanie dysków Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) na maszynach wirtualnych (VM) ułatwia adres zabezpieczeń organizacji i wymagania zgodności przez szyfrowanie dysków maszyny Wirtualnej (w tym rozruchu i dysków z danymi) przy użyciu kluczy i zasad kontroli w [klucza usługi Azure Magazyn](https://azure.microsoft.com/services/key-vault/).

Szyfrowanie dysków rozwiązania dla systemu Windows Hello jest oparta na [szyfrowania dysków funkcją BitLocker Microsoft](https://technet.microsoft.com/library/cc732774.aspx), i hello Linux rozwiązanie opiera się na [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt).

rozwiązanie Hello obsługuje następujące scenariusze dla maszyn wirtualnych IaaS, jeśli są włączone w systemie Microsoft Azure hello:
-   Integracja z usługi Azure Key Vault

-   Maszyny wirtualne warstwy standardowa: A, D DS, G, GS i tak dalej, maszyny wirtualne IaaS serii

-   Włączenie szyfrowania w systemach Windows i maszyn wirtualnych systemu Linux IaaS

-   Wyłączenie szyfrowania systemu operacyjnego i danych dyski dla maszyn wirtualnych IaaS systemu Windows

-   Wyłączenie szyfrowania dla dysków z danymi dla maszyn wirtualnych systemu Linux IaaS

-   Włączenie szyfrowania na maszynach wirtualnych IaaS, którego uruchomiono system operacyjny klienta systemu Windows

-   Włączenie szyfrowania na woluminach ze ścieżki instalacji

-   Włączenie szyfrowania na maszynach wirtualnych systemu Linux, które są skonfigurowane przy użyciu rozkładanie (RAID) przy użyciu [mdadm](https://en.wikipedia.org/wiki/Mdadm)

-   Włączenie szyfrowania na maszynach wirtualnych systemu Linux przy użyciu [LVM (Menedżer woluminów logicznych)](https://msdn.microsoft.com/library/windows/desktop/bb540532) dla dysków z danymi

-   Włączenie szyfrowania na maszynach wirtualnych systemu Windows, które są skonfigurowane przy użyciu funkcji miejsca do magazynowania

-   Wszystkie publiczne regiony platformy Azure są obsługiwane.

rozwiązanie Hello nie obsługuje następujące scenariusze, funkcje i technologie w wersji hello hello:

-   Maszyny wirtualne IaaS warstwa podstawowa

-   Wyłączenie szyfrowania na dysku systemu operacyjnego dla maszyn wirtualnych systemu Linux IaaS

-   Maszyny wirtualne IaaS, utworzony przy użyciu hello klasycznego metodę tworzenia maszyny Wirtualnej

-   Integracja z lokalnej usługi zarządzania kluczami

-   Usługa pliki Azure (udostępnionego systemu plików), sieciowego systemu plików (NFS), dynamiczne woluminy i maszyn wirtualnych systemu Windows, które są skonfigurowane przy użyciu systemów opartych na oprogramowaniu RAID

## <a name="sql-azure-database-isolation"></a>Izolacja Azure bazy danych SQL
Baza danych SQL jest usługą relacyjnych baz danych w chmurze firmy Microsoft hello oparte na aparacie Microsoft SQL Server wiodące rynku hello i nadaje się do obsługi obciążenia o znaczeniu krytycznym. Baza danych SQL oferuje przewidywalną danych izolacja na poziomie konta, geography / region, na podstawie i oparte na sieci — wszystko przy bliskich zeru nakładach administracji.

### <a name="sql-azure-application-model"></a>Model aplikacji usługi Azure SQL

[Microsoft SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-get-started) bazy danych jest oparta na chmurze usługa relacyjnej bazy danych oparty na technologii programu SQL Server. Zapewnia usługi wysokiej dostępności, skalowalności, wielodostępne bazy danych obsługiwane przez firmę Microsoft w chmurze.

Z perspektywy aplikacji usługi SQL Azure udostępnia powitania po hierarchii: każdy poziom ma zawierania jeden do wielu poziomów poniżej.

![Model aplikacji usługi Azure SQL](./media/azure-isolation/azure-isolation-fig10.png)

Witaj konto i Subskrypcja są rozliczeń tooassociate pojęcia platformy Microsoft Azure i zarządzania.

Logiczne serwerów i baz danych są pojęcia dotyczące usługi Azure SQL i są zarządzane za pomocą usług SQL Azure, pod warunkiem OData i TSQL interfejsy lub za pośrednictwem portalu SQL Azure, który zintegrowane w portalu Azure.

Serwery SQL Azure nie są fizycznej lub wystąpień maszyn wirtualnych, zamiast tego są one kolekcji baz danych, udostępnianie zasady zarządzania i zabezpieczeń, które są przechowywane w tak zwany "logicznych wzorca" bazy danych.

![Usługi SQL Azure](./media/azure-isolation/azure-isolation-fig11.png)

Logiczne baz danych master obejmują:

-   Toohello tooconnect używane logowania do programu SQL server

-   Reguły zapory

Toobe na powitania gwarantowane rozliczeń i dotyczące wykorzystania informacji dla baz danych SQL Azure z hello tym samym serwerze logicznym nie są tego samego wystąpienia fizycznego w klastrze usługi SQL Azure, zamiast tego aplikacje podać hello docelowej bazy danych nazwę podczas nawiązywania połączenia.

Z perspektywy klienta serwera logicznego jest tworzony w graficzny geograficznie regionu a hello tworzenia rzeczywistego powitania serwera odbywa się w jednym z klastrami hello w regionie hello.

### <a name="isolation-through-network-topology"></a>Izolację przez topologii sieci

Po utworzeniu serwera logicznego i zarejestrowaniu nazwy DNS, nazwy DNS hello punktów toohello tak zwane adres "VIP bramy" w centrum danych określonego hello rozmieszczenia powitania serwera.

Za hello VIP (wirtualny adres IP) zostały kolekcja usług bezstanowych bramy. Ogólnie rzecz biorąc bram uzyskać wykonywane po koordynacji potrzebne między wiele źródeł danych (bazy danych master, bazy danych użytkowników itp.). Brama usług zaimplementować hello poniżej:
-   **Pośredniczenie połączenia TDS.** W tym lokalizowanie bazy danych użytkowników w hello wewnętrznej bazy danych klastra, implementacja hello sekwencji logowania i następnie przekazywania hello TDS pakietów toohello wewnętrznej bazy danych i z powrotem.

-   **Zarządzanie bazą danych.** W tym wdrażanie to kolekcja operacji bazy danych CREATE/ALTER/DROP toodo przepływów pracy. Hello operacje bazy danych może być wywoływany przez wykrywania pakietów TDS lub jawne API OData.

-   Użytkownik logowania CREATE/ALTER/DROP operacji

-   Operacje zarządzania serwerem logicznym za pomocą interfejsu API OData

![Izolację przez topologii sieci](./media/azure-isolation/azure-isolation-fig12.png)

Warstwa Hello za bram hello jest nazywany "wewnętrzne". Jest to, gdy wszystkie dane hello są przechowywane w sposób wysokiej dostępności. Każdy element danych jest tooa wspomnianej toobelong "partycji" lub "jednostki trybu failover", każde z nich o co najmniej trzy repliki. Repliki są przechowywane i replikowane za pomocą aparatu programu SQL Server i zarządzane przez trybu failover systemu często określany tooas "sieci szkieletowej".

Ogólnie rzecz biorąc system zaplecza hello komunikują się wychodzących tooother systemy ze względów bezpieczeństwa. Jest to systemy toohello zarezerwowane w hello warstwy frontonu (bramy). maszyny warstwy Hello bramy ma ograniczone uprawnienia na powitania maszyny zaplecza toominimize hello ataku, jako mechanizm obrony zabezpieczeń.

### <a name="isolation-by-machine-function-and-access"></a>Izolacja według funkcji maszyny i dostępu
Usługi SQL Azure (składa się z usługi działające na innym komputerze funkcje. Usługi SQL Azure jest podzielony na "wewnętrzna" bazy danych w chmurze i "frontonu" środowiskach (bramy/Management), przy użyciu hello zasadniczo będzie tylko ruch do zaplecza, a nie wychodzących. środowisko frontonu Hello może komunikować się toohello poza world innych usług i ogólnie rzecz biorąc, tylko ma ograniczone uprawnienia w zaplecza hello (za mało toocall hello punkty wejścia go tooinvoke potrzeb).

## <a name="networking-isolation"></a>Izolacja sieci
Wdrożenia usługi Azure ma wiele warstw izolacji sieci. Witaj Poniższy diagram przedstawia izolacji sieci, które platforma Azure udostępnia toocustomers różnych warstw. Te warstwy są zarówno macierzystego w hello platformy Azure, sam, jak i funkcje zdefiniowane przez klientów. Przychodzące z Internetu hello, Azure DDoS zapewnia izolację na dużą skalę ataków na platformie Azure. Kolejna warstwa Hello izolacji jest zdefiniowany przez klienta publicznych adresów IP (punkty końcowe), które są używane toodetermine ruchu, które można przekazać za pośrednictwem sieci wirtualnej usługi toohello hello chmury. Azure macierzystego wirtualnego pełnej izolacji od innych sieci zapewnia izolację sieci i czy ruch przepływa tylko za pośrednictwem ścieżki użytkownika skonfigurowane i. Tych ścieżek i metody są hello kolejnej warstwy, których grup NSG, przez i wirtualnych urządzeń sieciowych mogą być używane toocreate izolacji granice tooprotect hello wdrożenia aplikacji w sieci hello chronione.

![Izolacja sieci](./media/azure-isolation/azure-isolation-fig13.png)

**Izolacja ruchu:** A [sieci wirtualnej](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) jest granica izolacji ruchu hello na powitania platformy Azure. Maszynach wirtualnych (VM) w jednej sieci wirtualnej nie może komunikować się bezpośrednio tooVMs w innej sieci wirtualnej, nawet jeśli obie sieci wirtualne są tworzone przez hello tego samego klienta. Izolacja jest krytyczne właściwość, która zapewnia klienta maszyn wirtualnych i komunikacja pozostanie prywatnej sieci wirtualnej.

[Podsieci](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#subnets) zapewnia dodatkową warstwę izolacji o w oparciu o zakres adresów IP sieci wirtualnej. Adresy IP w sieci wirtualnej hello, sieć wirtualną można podzielić na wiele podsieci w celu uporządkowania i zapewnienia bezpieczeństwa. Maszyny wirtualne i PaaS roli wdrożone toosubnets (tych samych lub różnych) w ramach sieci wirtualnej mogą komunikować się ze sobą bez dodatkowego konfigurowania. Można również skonfigurować [grupy zabezpieczeń sieci (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#network-security-groups-nsg) tooallow lub odmówić wystąpienia maszyny Wirtualnej tooa ruchu sieciowego na podstawie reguł skonfigurowanych w listy kontroli dostępu (ACL) NSG. Grupy NSG można kojarzyć z podsieciami lub poszczególnymi wystąpieniami maszyn wirtualnych w danej podsieci. Gdy grupa NSG jest skojarzona z podsiecią, reguły listy ACL hello zastosować wystąpień maszyn wirtualnych hello tooall w tej podsieci.

## <a name="next-steps"></a>Następne kroki

- [Izolacja sieci opcje dla komputerów w systemie Windows sieci wirtualnych platformy Azure](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/)

W tym hello klasycznego frontonu i zaplecza scenariusz której komputery w określonej sieci wewnętrznej lub podsieć może Zezwalaj tylko niektórych klientów lub inne komputery tooconnect tooa danego punktu końcowego oparte na listą dozwolonych adresów IP.

- [Obliczenia bazy danych izolacji](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure oferuje różne przetwarzania danych usług w chmurze zawierających szeroką gamę wystąpienia obliczeniowe i usług, które można skalować w górę i w dół automatycznie toomeet hello potrzeb aplikacji lub enterprise.

- [Izolacja magazynu](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure oddziela klienta obliczeń na podstawie maszyny Wirtualnej z magazynu. Ta separacja umożliwia obliczeń i magazynowania tooscale niezależnie, łatwiejsze wielodostępność tooprovide i izolacji, co. W związku z tym magazynu Azure działa na oddzielnego sprzętu z nie tooAzure łączności sieciowej obliczania, z wyjątkiem logicznie. Uruchom wszystkie żądania HTTP i HTTPS, na podstawie wyboru klienta.

