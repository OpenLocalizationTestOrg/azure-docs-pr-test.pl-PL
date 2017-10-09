---
title: "aaaSecurity najlepszych rozwiązań IaaS obciążeń na platformie Azure | Dokumentacja firmy Microsoft"
description: " Witaj migracji obciążeń tooAzure IaaS oferuje możliwości tooreevaluate nasze projekty "
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 02c5b7d2-a77f-4e7f-9a1e-40247c57e7e2
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: barclayn
ms.openlocfilehash: 9cee1ca6effe9561e51dc8b945e7388ffea169b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-iaas-workloads-in-azure"></a>Najlepsze rozwiązania dotyczące IaaS obciążeń na platformie Azure

Rozpocznie się zastanawiać przenoszenie obciążeń tooAzure infrastruktura jako usługa (IaaS), możesz prawdopodobnie zrealizowane zapoznali pewne zagadnienia. Środowisko zabezpieczanie środowisk wirtualnych mogą już istnieć. Po przeniesieniu tooAzure IaaS można się swoją wiedzą w zabezpieczanie środowisk wirtualnych i używać nowego zestawu opcji toohelp bezpiecznego zasobów.

Zacznijmy od informujący o tym, że powinien nie oczekujemy toobring zasobów lokalnych jako tooAzure jeden do jednego. wyzwania Hello i nowe opcje hello przełączyć istniejącą możliwości tooreevaluate deigns, narzędzi i procesów.

Twoje odpowiedzialność za bezpieczeństwo jest oparty na typie hello usługi w chmurze. Hello poniższej tabeli przedstawiono saldo hello odpowiedzialność firmy Microsoft i można:


![Zakres odpowiedzialności](./media/azure-security-iaas/sec-cloudstack-new.png)


Omówiono niektóre opcje hello dostępnej na platformie Azure, które pomaga spełnić wymagania dotyczące zabezpieczeń w organizacji. Należy pamiętać, że wymagania dotyczące zabezpieczeń mogą być różne w różnych rodzajów obciążeń. Nie jest elementem następujące najlepsze rozwiązania samodzielnie zabezpieczyć systemy. Podobnie jak żadnych innych elementów zabezpieczeń toochoose hello odpowiednie opcje i dowiedzieć się, jak hello rozwiązania można uzupełniają przez wypełniania luk.

## <a name="use-privileged-access-workstations"></a>Użyj stacje robocze uprzywilejowanego dostępu

Organizacje często wchodzą żerują toocyberattacks ponieważ administratorom wykonywać akcji przy użyciu konta z podwyższonym poziomem uprawnień. Zazwyczaj nie jest to złośliwy, ale ponieważ zezwala na to istniejącej konfiguracji i procesów. Większość tych użytkowników świadomość ryzyka hello tych działań z punktu widzenia koncepcyjnej, ale nadal wybierz toodo je.

Wykonywanie czynności, takie jak sprawdzanie poczty e-mail i przeglądania Internetu hello wydaje się wystarczająco nieszkodliwie. Ale one może narazić toocompromise z podwyższonym poziomem uprawnień konta przez złośliwych osób, używający działań przeglądania, specjalnie przygotowany wiadomości e-mail lub innych technik toogain dostępu tooyour przedsiębiorstwa. Zdecydowanie zaleca się użycie hello stacjami roboczymi do zarządzania bezpiecznego przeprowadzania wszystkich zadań administracyjnych usługi Azure, jako sposób zmniejszenie zagrożeń tooaccidental naruszenia.

Uprzywilejowany dostęp do stacji roboczych (łapy) zawierają dedykowanego systemu operacyjnego poufnych zadań —, który jest chroniony z Internetu ataków i zagrożeń wektory. Oddzielanie tych ważnych zadań i konta z hello stacji roboczych używanych codziennie i urządzenia udostępnia silną ochronę wyłudzania, aplikacji i systemu operacyjnego luk w zabezpieczeniach, różnych personifikacji przed atakami oraz ataki kradzieży poświadczeń, takie jak naciśnięcie klawisza Rejestrowanie i Pass--Hash, Pass--Ticket.

Hello ŁAPY podejście jest rozszerzeniem hello ustalonym i zalecane praktyki toouse konto administracyjne indywidualnie przypisane różni się od standardowego konta użytkownika. ŁAPY udostępnia zaufanego stacji roboczej dla tych kont poufnych.

Aby uzyskać więcej informacji i implementacji pomocy, zobacz [uprzywilejowanego dostępu stacje robocze](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/privileged-access-workstations).

## <a name="use-multi-factor-authentication"></a>Uwierzytelnianie wieloskładnikowe

W ciągu ostatnich hello Twojej sieci obwodowej był używany toocontrol dostępu toocorporate danych. W środowisku chmury — pierwszy, najpierw mobile tożsamość jest płaszczyzny kontroli hello: Użyj toocontrol usługi tooIaaS dostęp z dowolnego urządzenia. Można również stosować widoczność tooget i wgląd w jak i gdzie danych jest używany. Ochrona hello tożsamości cyfrowe użytkowników platformy Azure jest podstawą hello ochrony subskrypcji przed kradzieżą tożsamości i innych cybercrimes.

Jeden z kroków najbardziej przydatne hello, czy użytkownik może uwzględniać toosecure jest tooenable uwierzytelniania dwuskładnikowego. Uwierzytelnianie dwuskładnikowe jest sposób uwierzytelniania przy użyciu elementu dodanie tooa hasło. Pomaga ograniczyć ryzyko hello dostępu przez osobę, która zarządza tooget hasła do kogoś innego.

[Usługa Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) pomaga w zabezpieczaniu dostępu toodata i aplikacje, jednocześnie spełniając zapotrzebowanie na prosty proces logowania. Zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe — połączenie telefoniczne, wiadomość tekstowa lub powiadomienie aplikacji mobilnej. Użytkownicy wybierają metody hello preferowany.

Witaj najprostszy sposób toouse uwierzytelnianie wieloskładnikowe jest hello Microsoft Authenticator aplikacją mobilną, które można używać na urządzeniach przenośnych z systemem Windows, iOS i Android. Z hello najnowszej wersji systemu Windows 10 i hello integracji lokalnej usługi Active Directory z usługą Azure Active Directory (Azure AD) [Windows Hello dla firm](../active-directory/active-directory-azureadjoin-passport-deployment.md) może służyć do łatwego pojedynczego logowania jednokrotnego tooAzure zasobów. W takim przypadku urządzenie hello systemu Windows 10 jest używane jako hello drugiego etapu uwierzytelniania.

Dla konta, które zarządzają subskrypcją platformy Azure i kont, które można zarejestrować się w toovirtual maszyn przy użyciu usługi Multi-Factor Authentication zapewnia znacznie wyższy poziom zabezpieczeń niż używanie tylko hasła. Inne formy uwierzytelniania dwuskładnikowego może działać równie dobrze, ale ich wdrożeniem może być skomplikowane, jeśli tak nie jest już w środowisku produkcyjnym.

Witaj Poniższy zrzut ekranu przedstawia niektóre z dostępnych opcji hello uwierzytelnianie wieloskładnikowe Azure:

![Opcje uwierzytelniania wieloskładnikowego](./media/azure-security-iaas/mfa-options.png)

## <a name="limit-and-constrain-administrative-access"></a>Ograniczenia i ograniczenie dostępu administracyjnego

Zabezpieczanie kont hello, którymi może zarządzać subskrypcją platformy Azure jest bardzo ważne. naruszenie Hello któregokolwiek z tych kont Negacja wartości hello hello wszystkie inne czynności, że może potrwać tooensure hello poufność i integralność danych. Ostatnio zilustrowane hello [Edward Snowden](https://en.wikipedia.org/wiki/Edward_Snowden) wycieku informacji niejawnych atakami wewnętrznymi stanowić toohello dużych zagrożeń ogólne bezpieczeństwo każdej organizacji.

Następujące toothese podobnych kryteriów w celu oceny osoby do prawa administracyjne:

- Są one wykonywanie zadań, które wymagają uprawnień administratora?
- Jak często wykonywane zadania hello
- Czy istnieje powód, dlaczego nie można wykonać zadania hello przez innego administratora w ich imieniu?

Wszystkie inne uprawnienia hello toogranting znane alternatywnych metod i każdego Dlaczego dopuszczalne dokumentów.

Użyj Hello administracji just in time zapobiega hello niepotrzebnych istnieją konta z podwyższonym poziomem uprawnień w okresach, gdy nie są wymagane te prawa. Konta podniesionymi uprawnieniami przez ograniczony czas, aby administratorzy można wykonać swoje zadania. Następnie te prawa są usuwane na końcu hello shift lub zadanie zostało ukończone.

Można użyć [Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md) toomanage, monitorowania i kontroli dostępu w organizacji. Pomaga pamiętać o akcje hello, wykonywane przez osoby w Twojej organizacji. Stwarza również tooAzure administracji just in time AD dzięki zastosowaniu koncepcji hello kwalifikujących się Administratorzy. Są to osoby, która kont z toobe potencjalnych hello udzielono uprawnień administratora. Te typy użytkowników, należy udzielić uprawnień administratora przez ograniczony czas i można przejść za pośrednictwem procesu aktywacji.


## <a name="use-devtest-labs"></a>Użyj DevTest Labs

Laboratoria i środowisk deweloperskich przy użyciu usługi Azure umożliwia organizacjom toogain elastycznie badań i rozwoju przez wykonywania zadań hello opóźnienia, które wprowadza nabywania sprzętu. Niestety, brak znajomość Azure lub desire toohelp przyspieszenia przyjęciu może prowadzić toobe administratora hello zbyt ograniczająca z Przypisywanie praw. To zagrożenie przypadkowo może narazić hello organizacji toointernal ataków. Niektórzy użytkownicy mogą otrzymać znacznie szerszy dostęp niż powinny mieć.

Witaj [Azure DevTest Labs](../devtest-lab/devtest-lab-overview.md) usługi używa [kontroli dostępu](../active-directory/role-based-access-control-what-is.md) (RBAC). Za pomocą RBAC, można rozdzielenie obowiązków w obrębie organizacji do ról, które udzielić tylko hello poziom dostępu wymaganych przez użytkowników toodo swoich zadań. RBAC zawiera wstępnie zdefiniowane role (właściciel, użytkownik laboratorium i współautor). Można również użyć tych ról tooassign prawa tooexternal partnerów i znacznie upraszcza współpracy.

Ponieważ DevTest Labs używa RBAC, jest możliwe toocreate dodatkowe, [role niestandardowe](../devtest-lab/devtest-lab-grant-user-permissions-to-specific-lab-policies.md). DevTest Labs nie tylko ułatwia zarządzanie hello uprawnienia, takie rozwiązanie upraszcza proces konfigurowania środowisk elastycznie hello. Pomaga również postępowania w przypadku innych typowych wyzwań związanych z zespołów, które pracują na środowisk projektowania i testowania. Wymaga on pewne przygotowania, ale w długoterminowej hello go będzie ułatwienia dla zespołu.

Azure DevTest Labs funkcje:

- Kontrolę administracyjną nad toousers dostępne opcje hello. Hello administrator centralnie zarządzać dozwolone rozmiary maszyn wirtualnych, maksymalna liczba maszyn wirtualnych i rozpoczęcie maszyn wirtualnych i zamykania.
- Automatyzacja tworzenia środowiska laboratorium.
- Śledzenie kosztów.
- Uproszczony dystrybucji maszyn wirtualnych do tymczasowej pracy współpracy.
- Samoobsługi, który umożliwia ich labs tooprovision użytkowników przy użyciu szablonów.
- Ograniczanie zużycia i zarządzanie.

![Przy użyciu toocreate DevTest Labs laboratorium](./media/azure-security-iaas/devtestlabs.png)

Bez dodatkowych kosztów jest skojarzona z hello użycie DevTest Labs. Tworzenie Hello labs, zasady, szablonów i artefakty jest bezpłatna. Płacisz za tylko hello Azure zasoby używane w laboratorium, na przykład maszyny wirtualne, konta magazynu i sieci wirtualnych.



## <a name="control-and-limit-endpoint-access"></a>Limit i kontroli dostępu do punktu końcowego

Hosting labs lub systemów produkcyjnych na platformie Azure oznacza, że systemy muszą toobe dostępny z Internetu hello. Domyślnie nowej maszyny wirtualnej systemu Windows ma portem RDP hello jest dostępny z Internetu hello, a maszyny wirtualnej systemu Linux ma hello portu SSH. Podejmowanie działań toolimit widoczne punkty końcowe jest konieczne toominimize hello ryzyka nieautoryzowanego dostępu.

Technologie na platformie Azure może pomóc ograniczyć hello dostępu toothose administracyjne punktów końcowych. Na platformie Azure, można użyć [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md) (NSG). Gdy używasz usługi Azure Resource Manager do wdrożenia grup NSG zajmującym hello z wszystkich sieci toojust hello zarządzania punktów końcowych (RDP lub SSH). Jeśli uważasz, że grupy NSG, wziąć pod uwagę router listy kontroli dostępu. Można używać ich tootightly kontroli hello sieci komunikacji między różnych segmentów sieci platformy Azure. Jest to podobne sieci toocreating w sieci obwodowej lub innych sieci izolowanej. Nie kontrolują ruch hello, ale pomagają segmentacji sieci.


Na platformie Azure, można skonfigurować [sieci VPN typu lokacja lokacja](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) z sieci lokalnej. Sieć VPN lokacja lokacja rozszerza lokalnej sieci toohello chmury. Umożliwia innym toouse możliwości grup NSG, ponieważ można również zmodyfikować hello toonot grup NSG zezwolić na dostęp z dowolnego miejsca innych niż hello sieci lokalnej. Następnie można wymagać, aby zarządzanie odbywa się przez pierwszy toohello łączenia sieci platformy Azure za pośrednictwem sieci VPN.

Opcja VPN lokacja lokacja Hello może być najbardziej atrakcyjne w przypadku których prowadzą hosting systemów produkcyjnych, które są ściśle zintegrowane z lokalnymi zasobami na platformie Azure.

Alternatywnie można użyć hello [punkt lokacja](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md) opcji w sytuacji, gdy toomanage systemów, które nie muszą uzyskać dostęp do zasobów lokalnych tooon. Te systemy można samodzielnie w ich własnych sieci wirtualnych platformy Azure. Administratorzy mogą sieci VPN do hello Azure hostowane środowisko z ich administracyjnej stacji roboczej.

>[!NOTE]
>Możesz użyć albo powitalne tooreconfigure opcji VPN listy ACL na powitania grup NSG toonot umożliwiają punkty końcowe toomanagement dostępu z hello Internet.

Inną opcją warto rozważane jest [bramy usług pulpitu zdalnego](../multi-factor-authentication/multi-factor-authentication-get-started-server-rdg.md) wdrożenia. Można użyć tego wdrożenia toosecurely łączenia tooRemote serwerów usług pulpitu za pośrednictwem protokołu HTTPS, podczas gdy zastosowanie bardziej szczegółowe steruje toothose połączenia.

Funkcje, które będą miały dostępu tooinclude:

- Administrator opcje toolimit toorequests połączenia z określonym systemów.
- Uwierzytelnianie karty inteligentnej lub uwierzytelnianie wieloskładnikowe Azure.
- Kontrolowanie w systemach, w których ktoś połączyć toovia hello bramy.
- Kontrolę nad urządzeniami i dysk przekierowania.

## <a name="use-a-key-management-solution"></a>Za pomocą rozwiązania zarządzania kluczami

Bezpiecznego zarządzania kluczami jest tooprotecting istotnych danych w chmurze hello. Z [usługi Azure Key Vault](../key-vault/key-vault-whatis.md), można bezpiecznie przechowywać kluczy szyfrowania i kluczy tajnych w małych, takich jak hasła w sprzętowych modułach zabezpieczeń (HSM). W celu zapewnienia dodatkowego bezpieczeństwa możesz zaimportować lub wygenerować klucze w modułach HSM.

Procesy Microsoft klucze w trybie FIPS 140-2 poziom 2 HSM zweryfikowanych (sprzęt i oprogramowanie układowe). Monitor i inspekcji użycie kluczy z rejestrowaniem Azure: potoku dzienniki systemu Azure lub Security Information and Event Management (SIEM) dla dodatkowych analizy i wykrywania zagrożeń.

Każdy użytkownik z subskrypcją platformy Azure można tworzyć i używać magazynów kluczy. Mimo że Key Vault przynosi korzyści deweloperom i administratorom zabezpieczeń, można wdrożone i zarządzane przez administratora, który jest odpowiedzialny za zarządzanie usługami Azure w organizacji.


## <a name="encrypt-virtual-disks-and-disk-storage"></a>Szyfrowanie dysków wirtualnych i magazynu danych na dysku

[Szyfrowanie dysków Azure](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0) adresy hello zagrożenia kradzieżą lub ujawnieniem przed nieautoryzowanym dostępem, że jest to osiągane przez przeniesienie dysku danych. Witaj dysk może być dołączone tooanother systemu sposób pomijanie inne kontrole dotyczące zabezpieczenia. Dysk używa szyfrowania [funkcji BitLocker](https://technet.microsoft.com/library/hh831713) w systemach Windows i DM-Crypt w systemie operacyjnym Linux tooencrypt i dysków z danymi. Szyfrowanie dysków Azure integruje się z toocontrol magazyn kluczy i zarządzać kluczami szyfrowania hello. Jest ona dostępna dla standardowych maszyn wirtualnych i maszyn wirtualnych z magazyn w warstwie premium.

Aby uzyskać więcej informacji, zobacz [szyfrowania dysków Azure w systemie Windows i maszyn wirtualnych systemu Linux IaaS](azure-security-disk-encryption.md).

[Szyfrowanie usługi Magazyn Azure](../storage/common/storage-service-encryption.md) pomaga chronić dane przechowywane. Jest on włączony na poziomie konta magazynu hello. Ponieważ jest ona zapisywana w naszych centrach danych, które są automatycznie odszyfrowywane, tylko uzyskujesz dostęp do, szyfruje dane. Obsługuje ona hello następujące scenariusze:

- Dołącz szyfrowania blokowych obiektów blob, obiekty BLOB i stronicowe obiekty BLOB
- Szyfrowanie zarchiwizowane wirtualne dyski twarde i szablony przełączony w tryb tooAzure z lokalnymi
- Szyfrowanie podstawowego systemu operacyjnego i dysków z danymi dla maszyn wirtualnych IaaS, utworzony za pomocą sieci wirtualne dyski twarde

Przed przystąpieniem do szyfrowania magazynu Azure, należy pamiętać o dwa ograniczenia:

- Nie jest dostępny na klasycznych kont magazynu.
- Koduje tylko danych zapisane po włączeniu szyfrowania.

## <a name="use-a-centralized-security-management-system"></a>Używany system zarządzania scentralizowanych zabezpieczeń

Serwery muszą toobe monitorowane w celu stosowania poprawek, konfiguracji, zdarzeń i działania, które może zostać uznane za bezpieczeństwo. te dotyczy tooaddress, można użyć [Centrum zabezpieczeń](https://azure.microsoft.com/services/security-center/) i [Operations Management Suite zabezpieczeń i zgodności](https://azure.microsoft.com/services/security-center/). Obie te opcje wykracza poza hello konfiguracji w systemie operacyjnym hello. Zapewniają także monitorowanie konfiguracji hello hello podstawowej infrastruktury, takich jak konfiguracji sieci i używania urządzenia wirtualnego.

## <a name="manage-operating-systems"></a>Zarządzanie systemami operacyjnymi

W przypadku wdrożenia IaaS można nadal są odpowiedzialne za zarządzanie hello hello systemów, które można wdrożyć, podobnie jak inne serwery lub stacji roboczej w środowisku. Stosowanie poprawek, ograniczenie funkcjonalności, przypisywania praw i innych działań związanych z toohello konserwacji systemu nadal są z odpowiedzialności. Dla systemów, które są ściśle powiązane z zasobami lokalnymi, może zaistnieć toouse hello tego samego narzędzia i procedury, że używasz lokalnych elementów, jak oprogramowanie antywirusowe, ochrony przed złośliwym kodem, poprawki i kopii zapasowej.

### <a name="harden-systems"></a>Ograniczenia funkcjonalności systemów
Wszystkie maszyny wirtualne Azure IaaS powinien wzmocnione zabezpieczenia, dzięki czemu udostępniają tylko usługi punktów końcowych, które są wymagane dla aplikacji hello, które są zainstalowane. Dla maszyn wirtualnych systemu Windows, należy wykonać hello zaleceń, które firma Microsoft opublikuje jako podstawy dla hello [Security Compliance Manager](https://technet.microsoft.com/solutionaccelerators/cc835245.aspx) rozwiązania.

Menedżer zgodności zabezpieczeń to bezpłatne narzędzie. Można użyć tooquickly Konfigurowanie i zarządzanie nimi z komputerów stacjonarnych, tradycyjnych centrów danych i chmury prywatnej i publicznej za pomocą zasad grupy i System Center Configuration Manager.

Menedżer zgodności zabezpieczeń zawiera gotowe do wdrożenia zasad i zarządzania żądaną konfiguracją pakiety konfiguracyjne, które są sprawdzane pod. Te plany bazowe są oparte na [wskazówki dotyczące zabezpieczeń Microsoft](https://technet.microsoft.com/en-us/library/cc184906.aspx) zaleceń oraz z branży najlepsze rozwiązania. Pomagają odejście konfiguracji, adres wymagania dotyczące zgodności i zmniejsza zagrożenia bezpieczeństwa.

Za pomocą dwóch różnych metod, można użyć Menedżera zgodności zabezpieczeń tooimport hello bieżącej konfiguracji komputerów. Po pierwsze można zaimportować zasad grupy opartych na usłudze Active Directory. Po drugie, można zaimportować konfigurację "wzorcowe" hello komputera odniesienia przy użyciu hello [narzędzie LocalGPO](https://blogs.technet.microsoft.com/secguide/2016/01/21/lgpo-exe-local-group-policy-object-utility-v1-0/) tooback się hello lokalne zasady grupy. Następnie można zaimportować zasad grupy lokalne powitania do Menedżera zgodności zabezpieczeń.

Porównaj z normami tooindustry najlepszych rozwiązań, dostosuj je i Utwórz nowe zasady i pakiety konfiguracji zarządzania żądaną konfiguracją. Linie bazowe zostały opublikowane dla wszystkich obsługiwanych systemów operacyjnych, w tym Windows 10 Anniversary Update i Windows Server 2016.


### <a name="install-and-manage-antimalware"></a>Zainstaluj i Zarządzaj ochrony przed złośliwym oprogramowaniem

W środowiskach hostowanych oddzielnie od środowiska produkcyjnego, można użyć ochrony przed złośliwym kodem toohelp rozszerzenia ochrony maszyn wirtualnych i usług w chmurze. Integruje się z [Centrum zabezpieczeń Azure](../security-center/security-center-intro.md).


[Microsoft Antimalware](azure-security-antimalware.md) obejmuje funkcje, takie jak ochrona w czasie rzeczywistym, zaplanowane skanowanie, korygowaniem złośliwego oprogramowania, aktualizacji podpisu, aktualizacji aparatu i przykłady raportowania zbierania zdarzeń wykluczeń, i [ObsługaprogramuPowerShell](https://msdn.microsoft.com/library/dn771715.aspx).

![Azure ochrony przed złośliwym oprogramowaniem](./media/azure-security-iaas/azantimalware.png)

### <a name="install-hello-latest-security-updates"></a>Zainstaluj najnowsze aktualizacje zabezpieczeń hello
Pierwszy obciążeń hello, że klienci przenieść tooAzure należą labs i systemy dołączonej do Internetu. W przypadku maszyn wirtualnych hostowanych w usłudze Azure obsługuje aplikacje lub usługi, które wymagają toohello dostępny toobe Internet, można czujność o stosowanie poprawek. Poprawka poza hello systemu operacyjnego. Które luk w zabezpieczeniach w aplikacjach innych firm może również spowodować tooproblems, który można uniknąć, jeśli zarządzanie poprawkami dobrej znajduje się w miejscu.

### <a name="deploy-and-test-a-backup-solution"></a>Wdrażanie i testowanie kopii zapasowej rozwiązania

Podobnie jak aktualizacje zabezpieczeń, kopii zapasowej musi hello toobe obsługiwane taki sam sposób obsługi przez inną operację. Dotyczy to systemów, które są częścią środowiska produkcyjnego, rozszerzanie toohello chmury. Test i deweloperów systemy, należy wykonać strategii tworzenia kopii zapasowych, które zapewniają możliwości przywracania, które są podobne użytkowników toowhat znaczne przyzwyczajony do, na podstawie ich doświadczeń w środowiskach lokalnych.

Obciążeń produkcyjnych przeniesiony tooAzure należy zintegrować z istniejącymi rozwiązaniami tworzenia kopii zapasowej, jeśli to możliwe. Można użyć [kopia zapasowa Azure](../backup/backup-azure-arm-vms.md) toohelp adresów wymagania dotyczące tworzenia kopii zapasowej.


## <a name="monitor"></a>Monitorowanie

[Centrum zabezpieczeń](../security-center/security-center-intro.md) zapewnia ciągłej oceny hello stan zabezpieczeń zasobów platformy Azure tooidentify potencjalnych luk w zabezpieczeniach. Lista zaleceń prowadzi użytkownika przez proces konfigurowania wymaganych elementów sterujących hello.

Przykłady:

- Inicjowanie obsługi ochrony przed złośliwym kodem toohelp identyfikacji i usuwania złośliwego oprogramowania.
- Konfigurowanie sieci zabezpieczeń grup i reguł toocontrol ruchu toovirtual maszyn.
- Inicjowanie obsługi zapory aplikacji sieci web toohelp chronić przed atakami, które odnoszą się do aplikacji sieci web.
- Wdrażanie brakujących aktualizacji systemu.
- Modyfikowanie konfiguracji systemu operacyjnego, które nie odpowiadają hello zalecanych linii bazowych.

Witaj poniższej ilustracji przedstawiono niektóre opcje hello, które można włączyć w Centrum zabezpieczeń.

![Zasadami Centrum zabezpieczeń Azure](./media/azure-security-iaas/security-center-policies.png)

[Operations Management Suite](../operations-management-suite/operations-management-suite-overview.md) Microsoft oparte na chmurze IT rozwiązanie do zarządzania ułatwiające zarządzanie i ochrona lokalnej infrastruktury w chmurze. Ponieważ Operations Management Suite jest zaimplementowany jako usługa w chmurze, można wdrożyć, szybko i z minimalnym inwestycji w zasoby infrastruktury.

Nowe funkcje są przeprowadzane automatycznie, eliminuje konieczność rutynowej konserwacji i uaktualnić kosztów. Operations Management Suite integruje się również z programu System Center Operations Manager. Składa się z różnych składników toohelp lepiej zarządzać Azure obciążeń, w tym [zabezpieczeń i zgodności](../operations-management-suite/oms-security-getting-started.md) modułu.

Można hello funkcje zabezpieczeń i zgodności w programie Operations Management Suite tooview informacje o zasobach. informacje o Hello jest podzielony na cztery główne kategorie:

- **Domen zabezpieczeń**: dalszą analizę rekordy zabezpieczeń w czasie. Dostęp do oceny złośliwego oprogramowania, aktualizacji oceny, informacje o zabezpieczeniach sieci, tożsamości i dostępu do informacji i komputery ze zdarzeniami zabezpieczeń. Korzystać z pulpitu nawigacyjnego Centrum zabezpieczeń Azure toohello szybki dostęp.
- **Godne uwagi problemy**: szybko zidentyfikować hello liczba aktywnych problemów i hello ważności tych problemów.
- **Wykryć (wersja zapoznawcza)**: wykrycie ataku wzorce przez wizualizacja alerty zabezpieczeń po ich wprowadzeniu względem zasobów.
- **Analizy zagrożeń**: wykrycie ataku hello wzorce przez wizualizacja hello łącznej liczby serwerów z wychodzącym ruchem złośliwego oprogramowania IP, typ złośliwe oprogramowanie i mapowanie pokazujący, gdzie pochodzą z tych adresów IP.
- **Typowe zapytania zabezpieczeń**: Zobacz listę najczęściej zabezpieczeń hello zapytania, których można używać toomonitor środowiska. Po kliknięciu jednego z tych kwerend hello **wyszukiwania** bloku otwiera i wyświetla wyniki hello tej kwerendy.

Witaj Poniższy zrzut ekranu przedstawia przykład hello informacje, które można wyświetlić Operations Management Suite.

![Plany bazowe zabezpieczeń programu Operations Management Suite](./media/azure-security-iaas/oms-security-baseline.png)



## <a name="next-steps"></a>Następne kroki


* [Blog zespołu ds. zabezpieczeń platformy Azure](https://blogs.msdn.microsoft.com/azuresecurity/)
* [Centrum zabezpieczeń firmy Microsoft](https://technet.microsoft.com/library/dn440717.aspx)
* [Wskazówki dotyczące zabezpieczeń platformy Azure i wzorce](security-best-practices-and-patterns.md)
