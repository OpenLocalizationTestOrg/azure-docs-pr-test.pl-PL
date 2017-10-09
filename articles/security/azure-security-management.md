---
title: "aaaEnhance zabezpieczeń zdalnego zarządzania na platformie Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano kroki związane z poprawianiem zabezpieczeń zdalnego zarządzania podczas administrowania środowiskami Microsoft Azure, w tym usługami w chmurze, usługą Virtual Machines i aplikacjami niestandardowymi."
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 2431feba-3364-4a63-8e66-858926061dd3
ms.service: security
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 9262cfb98bfe51d15fbad8f18997c4573668d9ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-management-in-azure"></a>Zarządzanie zabezpieczeniami na platformie Azure
Subskrybenci platformy Azure mogą zarządzać środowiskami chmury przy użyciu wielu urządzeń, łącznie ze stacjami roboczymi do zarządzania, komputerami deweloperów, a nawet urządzeniami uprzywilejowanych użytkowników końcowych, którzy mają uprawnienia specyficzne dla zadania. W niektórych przypadkach funkcje administracyjne są wykonywane za pośrednictwem konsoli opartych na sieci web, takich jak hello [portalu Azure](https://azure.microsoft.com/features/azure-portal/). W innych przypadkach mogą istnieć tooAzure bezpośrednich połączeń z systemów lokalnych za pośrednictwem wirtualnej sieci prywatnej (VPN), usług terminalowych, protokołów aplikacji klienckich lub (programowo) hello Azure Service Management API (SMAPI). Ponadto punkty końcowe klienta mogą być przyłączone do domeny lub odizolowane i niezarządzane (np. tablety lub smartfony).

Mimo że wiele możliwości dostępu i zarządzania zapewniają bogaty zestaw opcji, jednak można dodać znaczące zagrożenie tooa chmury wdrażania. Może być trudne toomanage, śledzenie i inspekcję czynności administracyjnych. To zróżnicowanie może również wprowadzać zagrożenia bezpieczeństwa związane z nieuregulowanym dostępem punkty końcowe tooclient, które są używane do zarządzania usługami w chmurze. Użycie ogólnych lub osobistych stacji roboczych do opracowywania infrastruktury i zarządzania nią powoduje, że zagrożenia mogą nadchodzić z nieprzewidywalnych kierunków, na przykład podczas przeglądania sieci Web (na przykład ataki za pośrednictwem używanych witryn) lub korzystania z poczty e-mail (na przykład techniki socjotechniczne i wyłudzanie informacji).

![][1]

Hello potencjalnymi atakami zwiększa się w środowisku tego typu, ponieważ jest trudne tooconstruct zabezpieczeń zasad i mechanizmów tooappropriately Zarządzanie interfejsów tooAzure dostępu (na przykład SMAPI) z bardzo różnorodnych punktów końcowych.

### <a name="remote-management-threats"></a>Zagrożenia związane ze zdalnym zarządzaniem
Osoby atakujące często usiłują toogain uprzywilejowany dostęp przez uzyskanie poświadczeń konta (na przykład za pomocą hasła ukierunkowany wymuszania wyłudzaniem informacji i przechwycenia poświadczeń) lub podstępne uruchomienia szkodliwego kodu (na przykład ze szkodliwych witryn sieci Web dysku przez pliki do pobrania lub ze szkodliwych załączników wiadomości e-mail). W zdalnie zarządzanym środowisku chmury, konto naruszeń może prowadzić tooan zwiększone ryzyko tooanywhere termin, dostęp w dowolnym momencie.

Nawet w przypadku ścisłej kontroli kont głównych administratorów kont użytkowników niższego poziomu mogą być używane tooexploit słabe strony algorytmu w strategii zabezpieczeń. Brak szkolenia odpowiednich ustawień zabezpieczeń również może prowadzić toobreaches skutek przypadkowego ujawnienia lub eksponowania informacji o koncie.

Jeśli stacja robocza użytkownika jest używana również do wykonywania zadań administracyjnych, zabezpieczenia mogą zostać naruszone w wielu różnych punktach. Czy użytkownik jest przeglądanie sieci web hello, przy użyciu narzędzia innej firmy 3rd i open source lub otwieranie pliku szkodliwe dokumentu zawierającego konia trojańskiego.

Ogólnie rzecz biorąc większość ataków ukierunkowanych, które doprowadzi do naruszeń danych mogą być śledzone toobrowser luki w zabezpieczeniach, wtyczek (takich jak Flash, PDF i Java) i ukierunkowanego wyłudzania informacji (poczta e-mail) na komputerach stacjonarnych. Te komputery mogą mieć na poziomie administracyjnym lub tooaccess uprawnień na poziomie usługi live serwerów lub urządzeń operacji, gdy używane do tworzenia i zarządzania innych zasobów sieciowych.

### <a name="operational-security-fundamentals"></a>Podstawy bezpieczeństwa operacyjnego
Dla lepiej zabezpieczyć zarządzanie i operacje można zminimalizować możliwości ataku na klienta, zmniejszając hello liczbę możliwych punktów wejścia. Można to zrobić za pomocą zasad zabezpieczeń „podział obowiązków” i „podział środowisk”.

Izolowanie ważnych funkcji ze sobą toodecrease hello prawdopodobieństwo że błąd na jednym poziomie prowadzi naruszenia tooa w innym. Przykłady:

* Zadania administracyjne nie powinny być łączone z działaniami, które mogą prowadzić do naruszenia tooa (na przykład przed złośliwym oprogramowaniem w wiadomości e-mail administratora zainfekowanie serwera infrastruktury).
* Stacja robocza używana do ważnych operacji nie powinna być hello, w tym samym systemie używany do celów o wysokim ryzyku, takich jak hello przeglądania Internetu.

Zmniejsza możliwości ataku na hello system przez usunięcie niepotrzebnego oprogramowania. Przykład:

* Standard administracyjne, pomocy technicznej lub deweloperskiej stacji roboczej nie powinny wymagać instalacji klienta poczty e-mail lub innych aplikacji biurowych, jeśli urządzenie hello głównym celem jest toomanage usługi w chmurze.

Systemy klienckie, które mają tooinfrastructure dostępu administratora, które składniki mają zostać poddane toohello najbardziej rygorystyczne zasady tooreduce zagrożeń. Przykłady:

* Zasady zabezpieczeń mogą zawierać ustawienia zasad grupy, które odmawiają otwartego dostępu do Internetu z urządzeń hello i stosowanie restrykcyjnej konfiguracji zapory.
* Korzystanie z sieci VPN z zabezpieczeniami protokołu internetowego (IPSec), jeśli wymagany jest bezpośredni dostęp.
* Skonfigurowanie oddzielnych domen usługi Active Directory na potrzeby zarządzania i programowania.
* Izolowanie i filtrowanie ruchu sieciowego stacji roboczej używanej do zarządzania.
* Korzystanie z oprogramowania chroniącego przed złośliwym kodem.
* Implementowanie uwierzytelniania wieloskładnikowego tooreduce hello ryzyka kradzieży poświadczeń.

Konsolidacja zasobów umożliwiających dostęp i eliminacja niezarządzanych punktów końcowych dodatkowo upraszcza zadania związane z zarządzaniem.

### <a name="providing-security-for-azure-remote-management"></a>Zapewnianie bezpieczeństwa zdalnego zarządzania na platformie Azure
Platforma Azure udostępnia zabezpieczeń mechanizmów tooaid administratorów, którzy zarządzają usług w chmurze Azure i maszyn wirtualnych. Te mechanizmy to m.in.:

* Uwierzytelnianie i [kontrola dostępu oparta na rolach](../active-directory/role-based-access-control-configure.md).
* Monitorowanie, rejestrowanie i inspekcje.
* Certyfikaty i szyfrowanie komunikacji.
* Portal zarządzania w sieci Web.
* Filtrowanie pakietów sieciowych.

Z konfiguracją zabezpieczeń po stronie klienta i wdrożeniem centrum danych bramy zarządzania jest możliwe toorestrict i monitor administratora dostępu toocloud aplikacji i danych.

> [!NOTE]
> Zastosowanie niektórych zaleceń zamieszczonych w tym artykule może spowodować zwiększenie użycia danych, sieci lub zasobów obliczeniowych i podwyższenie kosztów licencji lub subskrypcji.
>
>

## <a name="hardened-workstation-for-management"></a>Stacja robocza do zarządzania ze wzmocnionymi zabezpieczeniami
celem wzmocnienia zabezpieczeń stacji roboczej Hello jest tooeliminate wszystkie, ale hello najważniejsze funkcje wymagane dla niego toooperate wprowadzania możliwie najmniejsze hello potencjalny obszar ataków. Wzmocnienie zabezpieczeń systemu obejmuje, minimalizując liczbę hello zainstalowanych usług i aplikacji, ograniczenie uruchamiania aplikacji i tooonly dostępu do sieci, co jest potrzebne, i nie należy instalować zawsze hello system toodate. Ponadto wzmocnienie zabezpieczeń stacji roboczej do zarządzania powoduje oddzielenie działań i narzędzi administracyjnych od innych zadań użytkowników końcowych.

W środowisku przedsiębiorstwa lokalnie można ograniczyć hello ataku infrastruktury fizycznej za pomocą dedykowanych sieci do zarządzania, serwerowni karty dostępu i stacji roboczych działających w chronionych obszarach sieci hello. W chmurowym lub hybrydowym modelu IT większego dotyczące bezpieczeństwa usług zarządzania może być bardziej złożone z powodu braku hello zasobów tooIT fizyczny dostęp. W przypadku implementowania rozwiązań w zakresie ochrony wymagane jest rozważne konfigurowanie oprogramowania oraz stosowanie procesów zorientowanych na bezpieczeństwo i kompleksowych zasad.

Przy użyciu rozmiaru oprogramowania zminimalizowane uprawnień w trybie blokady stacji roboczej do zarządzania chmurą — i tworzenie aplikacji — można zmniejszyć ryzyko hello naruszenia zabezpieczeń dzięki standaryzacji hello zdalnego zarządzania i środowisk deweloperskich. Stacji roboczej ze wzmocnionymi zabezpieczeniami konfiguracji mogą pomagać w zapobieganiu hello naruszeniu zabezpieczeń kont, które są używane toomanage najważniejszymi zasobami chmury przez zamknięcie wielu typowych możliwości ataku z wykorzystaniem złośliwego oprogramowania i luk w zabezpieczeniach. W szczególności mogą używać [systemu Windows AppLocker](http://technet.microsoft.com/library/dd759117.aspx) i toocontrol technologii Hyper-V i izolowania zachowania systemu klienta oraz ograniczenia zagrożeń związanych z tym wiadomości e-mail lub przeglądaniem Internetu.

Na stacji roboczej ze wzmocnionymi zabezpieczeniami hello administrator uruchamia konta użytkownika standardowego (które blokuje wykonywanie na poziomie administratora) i skojarzone aplikacje są kontrolowane przez listę dozwolonych. podstawowe elementy Hello wzmocnienie zabezpieczeń stacji roboczej są następujące:

* Aktywne skanowanie i stosowanie poprawek. Wdrażania oprogramowania chroniącego przed złośliwym kodem, regularne luki w zabezpieczeniach skanowania i aktualizowanie wszystkich stacji roboczych przy użyciu najnowszych aktualizacji zabezpieczeń hello w odpowiednim czasie.
* Ograniczenie funkcjonalności. Odinstalowanie zbędnych aplikacji i wyłączenie zbędnych usług (startowych).
* Wzmocnienie zabezpieczeń sieci. Użyj zapory systemu Windows reguły tooallow tylko prawidłowych adresów IP, porty i adresy URL powiązane tooAzure zarządzania. Upewnij się, że stacji roboczej toohello zdalne połączenia przychodzące są również blokowane.
* Ograniczenie wykonywania. Zezwalaj tylko zestaw wstępnie zdefiniowanych plików wykonywalnych, które są wymagane do zarządzania toorun (określony tooas "odmową domyślną"). Domyślnie użytkownicy należy odmówić uprawnień toorun żadnego programu, jeśli nie jest jawnie zdefiniowany w hello lista dozwolonych.
* Stosowanie najniższych uprawnień. Użytkownicy stacji roboczej zarządzania nie powinna mieć żadnych uprawnień administracyjnych na komputerze lokalnym hello samej siebie. Dzięki temu nie mogą zmienić hello konfiguracji systemu ani hello plików systemowych, celowo lub przypadkowo.

Można wymusić wszystko to przy użyciu [obiektów zasad grupy](https://www.microsoft.com/download/details.aspx?id=2612) (GPO) w usługach domenowych w usłudze Active Directory (AD DS), stosując je za pomocą kont zarządzania tooall domeny zarządzania (lokalny).

### <a name="managing-services-applications-and-data"></a>Zarządzanie usługami, aplikacjami i danymi
Konfiguracji usługi w chmurze Azure realizuje hello portalu Azure lub interfejsu SMAPI, za pomocą interfejsu wiersza polecenia programu Windows PowerShell hello lub aplikacji niestandardowej, która korzysta z tych interfejsów RESTful. Z tych mechanizmów korzystają usługi takie jak Azure Active Directory (Azure AD), Azure Storage, Azure Websites, Azure Virtual Network i inne.

Aplikacje wdrożone na maszynie wirtualnej zapewniają własne narzędzia klienta i interfejsów, zgodnie z potrzebami, takie jak hello Microsoft Management Console (MMC), konsolę zarządzania przedsiębiorstwem (na przykład program Microsoft System Center lub Windows Intune) lub innego zarządzania Aplikacja — Microsoft SQL Server Management Studio, na przykład. Te narzędzia zazwyczaj znajdują się w środowisku przedsiębiorstwa lub sieci klienta. Mogą być one zależne od określonych protokołów sieciowych, takich jak protokół Remote Desktop Protocol (RDP), wymagających stanowych połączeń bezpośrednich. Niektóre mogą mieć interfejsy sieci web, które nie powinny być jawnie publikowane ani dostępne za pośrednictwem hello Internet.

Można ograniczyć dostęp tooinfrastructure i platformy zarządzania usługami Azure za pomocą [uwierzytelnianie wieloskładnikowe](../multi-factor-authentication/multi-factor-authentication.md), [certyfikatów zarządzania X.509](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/), a reguły zapory. Witaj portalu Azure i interfejs SMAPI wymagają zabezpieczeń TLS (Transport Layer). Jednak usługi i aplikacje, które można wdrożyć na platformie Azure wymagają tootake środki ochrony, które są odpowiednie dla aplikacji. Te mechanizmy często można zapewnić łatwiej przy użyciu standardowej konfiguracji stacji roboczej ze wzmocnionymi zabezpieczeniami.

### <a name="management-gateway"></a>Brama zarządzania
wszystkie administracyjne toocentralize dostępu i uprościć monitorowanie i rejestrowanie, można wdrożyć dedykowany [bramy usług pulpitu zdalnego](https://technet.microsoft.com/library/dd560672) serwera (bramy usług pulpitu zdalnego) w lokalnej sieci połączonych tooyour środowiska platformy Azure.

Brama usług pulpitu zdalnego jest opartą na zasadach usługą serwera proxy RDP wymuszającą wymagania dotyczące zabezpieczeń. Zaimplementowanie bramy usług pulpitu zdalnego wraz z ochroną dostępu do sieci (NAP, Network Access Protection) systemu Windows Server gwarantuje, że połączenia mogą ustanawiać tylko klienci spełniający określone kryteria kondycji zabezpieczeń określone przez obiekty zasad grupy w usłudze Active Directory Domain Services. Ponadto:

* Zainicjuj obsługę [certyfikat zarządzania platformy Azure](http://msdn.microsoft.com/library/azure/gg551722.aspx) na powitania bramy usług pulpitu zdalnego, aby była hello hosta tylko dozwolone tooaccess hello portalu Azure.
* Dołącz toohello bramy usług pulpitu zdalnego hello tego samego [domeny zarządzania](http://technet.microsoft.com/library/bb727085.aspx) jako hello stacji roboczych administratorów używanych. Jest to konieczne, gdy używasz protokołu IPsec sieci VPN lokacja lokacja lub ExpressRoute w domenie, która ma tooAzure jednokierunkowe zaufanie AD lub w przypadku Federacji poświadczeń między lokalnym wystąpieniem usług AD DS i Azure AD.
* Skonfiguruj [zasady autoryzacji połączeń klientów](http://technet.microsoft.com/library/cc753324.aspx) toolet hello bramy usług pulpitu zdalnego sprawdź, czy nazwa komputera klienta hello jest nieprawidłowa (przyłączony do domeny) i dozwolonych tooaccess hello portalu Azure.
* Używaj zabezpieczeń IPsec dla [sieci VPN platformy Azure](https://azure.microsoft.com/documentation/services/vpn-gateway/) toofurther chronić ruch związany z zarządzaniem przed podsłuchem i kradzieżą tokenów, lub rozważ izolowanego łącza internetowego za pośrednictwem [Azure ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).
* Zapewnij uwierzytelnianie wieloskładnikowe (za pomocą usługi [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)) lub uwierzytelnianie przy użyciu kart inteligentnych dla administratorów logujących się przy użyciu bramy usług pulpitu zdalnego.
* Konfigurowanie źródła [ograniczenia adresu IP](http://azure.microsoft.com/blog/2013/08/27/confirming-dynamic-ip-address-restrictions-in-windows-azure-web-sites/) lub [grup zabezpieczeń sieci](../virtual-network/virtual-networks-nsg.md) hello Azure toominimize liczbę punktów końcowych uprawnionych do zarządzania.

## <a name="security-guidelines"></a>Zalecenia dotyczące zabezpieczeń
Ogólnie rzecz biorąc, pomaga stacje robocze administratora toosecure podobne praktyki toohello używany do dowolnej stacji roboczej w sieci lokalnej jest używany z chmurą hello — na przykład minimalizacja funkcjonalności i bardziej restrykcyjnymi uprawnieniami. Niektóre unikatowe aspekty zarządzania chmurą są bardziej akin tooremote lub zarządzania poza pasmem. Obejmują one hello użycie i inspekcja poświadczeń, rozszerzone zabezpieczenia dostępu zdalnego oraz wykrywanie zagrożeń i odpowiedzi.

### <a name="authentication"></a>Authentication
Można użyć tooconstrain ograniczeń logowania platformy Azure źródłowych adresów IP do uzyskiwania dostępu do narzędzi administracyjnych i prowadzić inspekcję żądań dostępu. toohelp Azure identyfikowania klientów (stacji roboczych i/lub aplikacji), możesz skonfigurować zarówno interfejs SMAPI (przy użyciu narzędzi opracowanych przez klienta, takich jak polecenia cmdlet programu Windows PowerShell), jak i hello toorequire portalu Azure po stronie klienta zarządzania certyfikatami toobe zainstalowanych dodatkowo tooSSL certyfikatów. Zalecamy również stosowanie uwierzytelniania wieloskładnikowego w przypadku dostępu administratorów.

Niektóre aplikacje lub usługi wdrażane na platformie Azure mogą mieć własne mechanizmy uwierzytelniania zarówno użytkowników końcowych, jak i administratorów, podczas gdy inne wykorzystują w pełnym zakresie usługę Azure AD. W zależności od tego, czy Federacji poświadczeń za pomocą usługi Active Directory Federation Services (AD FS), używana synchronizacja katalogów lub obsługa kont użytkowników jedynie w hello chmury, za pomocą [Microsoft Identity Manager](https://technet.microsoft.com/library/mt218776.aspx) (część Azure AD Premium) ułatwia zarządzanie cyklami życia tożsamości między zasobami hello.

### <a name="connectivity"></a>Łączność
Kilka mechanizmów są dostępne toohelp klienta bezpiecznego połączenia tooyour sieci wirtualnych platformy Azure. Dwa z tych mechanizmów [sieci VPN typu lokacja lokacja](https://channel9.msdn.com/series/Azure-Site-to-Site-VPN) (S2S) i [sieci VPN typu punkt lokacja](../vpn-gateway/vpn-gateway-point-to-site-create.md) (P2S), Zezwalaj na używanie hello branży standardowego protokołu IPsec (S2S) lub hello [Secure Socket Tunneling Protocol](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx)(SSTP) (P2S) do szyfrowania i tunelowania. W przypadku takich jak hello portalu Azure do zarządzania usługami Azure uwzględniającym toopublic jest połączenie platformy Azure, Azure wymaga Hypertext Transfer Protocol Secure (HTTPS).

Autonomiczny robocza ze wzmocnionymi zabezpieczeniami tooAzure nie połączenie za pośrednictwem bramy usług pulpitu zdalnego należy użyć hello protokołu SSTP punkt lokacja sieci VPN toocreate hello połączenia początkowego toohello sieci wirtualnej platformy Azure, a następnie utwórz tooindividual połączenia RDP wirtualnego maszyny z z hello tunel VPN.

### <a name="management-auditing-vs-policy-enforcement"></a>Inspekcja zarządzania a wymuszanie zasad
Zazwyczaj istnieją dwa podejścia procesów zarządzania toosecure: inspekcja i wymuszanie zasad. Zastosowanie obu podejść zapewnia kompleksową kontrolę, ale nie zawsze jest możliwe. Ponadto każde podejście jest różnych poziomów ryzyka, kosztem i działania związane z zarządzaniem zabezpieczeń, szczególnie, co wiąże toohello poziomu zaufania w osób i architektur systemów.

Monitorowanie, rejestrowanie i inspekcja stanowią podstawę dla śledzenia i zrozumienia czynności administracyjnych, ale może nie zawsze być możliwe tooaudit wszystkich akcji w ukończyć szczegółów powodu toohello ilość generowanych danych. Inspekcja skuteczności zasad zarządzania hello hello jest jednak najlepszym rozwiązaniem.

Wymuszanie zasad, które obejmuje ścisłą kontrolę dostępu, polega na stosowaniu programowych mechanizmów zarządzających akcjami wykonywanymi przez administratorów i ułatwia zapewnienie stosowania wszystkich możliwych środków ochrony. Rejestrowanie umożliwia potwierdzenie wymuszenia w rekordzie tooa dodanie wprowadzonych, z którym i. Rejestrowanie również włącza tooaudit i porównuje informacje o tym, jak Administratorzy kolejne zasady i zapewnia potwierdzenie wykonania czynności.

## <a name="client-configuration"></a>Konfiguracja klientów
Zalecamy trzy podstawowe konfiguracje stacji roboczych ze wzmocnionymi zabezpieczeniami. Witaj najważniejsze różnice są kosztem, użytecznością i dostępnością, przy zachowaniu podobnego profilu zabezpieczeń dla wszystkich opcji. Witaj w poniższej tabeli zawiera zwięzłe informacje umożliwiające analizę hello tooeach korzyści i zagrożeń. (Należy pamiętać, że "komputer firmowy" oznacza tooa standardową konfigurację komputera stacjonarnego wdrażaną dla wszystkich użytkowników domeny, niezależnie od roli).

| Konfiguracja | Korzyści | Wady |
| --- | --- | --- |
| Autonomiczna stacja robocza ze wzmocnionymi zabezpieczeniami |Ściśle kontrolowana stacja robocza |Wyższy koszt dla dedykowanych komputerów stacjonarnych |
| - | Mniejsze ryzyko wykorzystania luk w zabezpieczeniach aplikacji |Większa ilość zasobów wymaganych do zarządzania |
| - | Przejrzysty podział obowiązków | - |
| Komputer firmowy jako maszyna wirtualna |Niższe koszty sprzętu | - |
| - | Podział ról i aplikacji | - |
| Toogo systemu Windows z szyfrowania dysków funkcją BitLocker |Zgodność z większością komputerów |Śledzenie zasobów |
| - | Efektywność kosztowa i przenośność | - |
| - | Izolowane środowisko zarządzania |- |

Koniecznie hello stacji roboczej ze wzmocnionymi zabezpieczeniami jest hello hosta, a nie hello gościem, bez żadnych składników między hello hostem operacyjnej sprzętu systemu i hello. Witaj "zasadą czystego źródła" (nazywane również "bezpiecznym pochodzeniem") oznacza hostujących hello powinny być hello najbardziej wzmocnione zabezpieczenia. W przeciwnym razie hello stacji roboczej ze wzmocnionymi zabezpieczeniami (Gość) jest tooattacks podmiotu w systemie hello, na którym jest obsługiwany.

Dodatkowo można oddzielić funkcje administracyjne za pomocą dedykowanych obrazów systemu dla każdej wzmocnienie zabezpieczeń stacji roboczej zawierających tylko hello narzędzia i uprawnienia wymagane do zarządzania wybierz pozycję Azure i aplikacji z określonych lokalnej usługi AD DS obiektów zasad grupy dla hello w chmurze niezbędnych zadań.

Dla środowisk IT bez infrastruktury lokalnej (na przykład nie dostępu tooa wystąpienia lokalnych usług AD DS dla obiektów zasad grupy, ponieważ wszystkie serwery są w chmurze hello) usługi, takie jak [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx) można uprościć wdrażanie i konserwację konfiguracje stacji roboczej.

### <a name="stand-alone-hardened-workstation-for-management"></a>Autonomiczna stacja robocza do zarządzania ze wzmocnionymi zabezpieczeniami
W przypadku autonomicznej stacji roboczej ze wzmocnionymi zabezpieczeniami administratorzy mają komputer lub laptop, używany do wykonywania zadań administracyjnych, i oddzielny komputer lub laptop do wykonywania innych zadań. Toomanaging stacji roboczej dedykowanej usługami Azure nie trzeba instalować innych aplikacji. Ponadto korzystanie ze stacji roboczych obsługujących moduł [Trusted Platform Module](https://technet.microsoft.com/library/cc766159) (TPM) lub podobną sprzętową technologię kryptograficzną ułatwia uwierzytelnianie urządzeń i zapobieganie niektórym atakom. Za pomocą modułu TPM może również obsługiwać ochronę całego woluminu dysku systemowego hello [szyfrowania dysków funkcją BitLocker](https://technet.microsoft.com/library/cc732774.aspx).

W scenariuszu autonomicznej stacji roboczej ze wzmocnionymi zabezpieczeniami hello (pokazana poniżej), hello lokalne wystąpienie zapory systemu Windows (lub zapory klienta firmy Microsoft) jest skonfigurowany tooblock przychodzących połączeń, takie jak protokół RDP. Witaj, administrator może zalogować się przy toohello stacji roboczej ze wzmocnionymi zabezpieczeniami i rozpocząć jako sesji protokołu RDP, który łączy tooAzure po ustanowieniu sieci VPN łączyć się z sieci wirtualnej platformy Azure, ale nie można zalogować się tooa firmowym Komputerem i użycie protokołu RDP tooconnect toohello wzmocnione zabezpieczenia stacji roboczej samego siebie.

![][2]

### <a name="corporate-pc-as-virtual-machine"></a>Komputer firmowy jako maszyna wirtualna
W przypadkach, gdy oddzielne autonomicznej stacji roboczej ze wzmocnionymi zabezpieczeniami jest koszt hello zaporowe i niewygodne, stacja robocza może hostować zadań innych niż administracyjne tooperform maszyny wirtualnej.

![][3]

tooavoid kilku zagrożeń wynikających z użycia pojedynczej stacji roboczej do zarządzania systemami i wykonywania innych codziennych zadań, można wdrożyć stacji roboczej wzmocnione zabezpieczenia toohello maszyny wirtualnej funkcji Hyper-V systemu Windows. Ta maszyna wirtualna może służyć jako hello komputer firmowy. Witaj środowisko komputera firmowego może pozostać odizolowane od hello hosta, co pozwoli ograniczyć jej podatność na ataki i usuwa codzienne działania hello użytkownika (np. wiadomości e-mail) od ważnych z zadań administracyjnych.

Maszyna wirtualna komputera firmowego Hello działa w obszarze chronionym i udostępnia aplikacje użytkownika. Witaj host pozostaje "czystym źródłem" i wymusza ścisłe zasady sieci w głównym systemie operacyjnym hello (na przykład blokowanie dostępu RDP z maszyny wirtualnej hello).

### <a name="windows-toogo"></a>TooGo systemu Windows
Inny alternatywny toorequiring autonomicznej stacji roboczej ze wzmocnionymi zabezpieczeniami jest toouse [Windows tooGo](https://technet.microsoft.com/library/hh831833.aspx) dysków funkcją, która obsługuje możliwość rozruchu USB po stronie klienta. TooGo systemu Windows umożliwia użytkownikom tooboot zgodny komputer tooan izolowanego obrazu systemu z zaszyfrowanego dysku flash USB. Zapewnia dodatkowe funkcje kontroli dla punktów końcowych zdalnej administracji, ponieważ obraz powitania mogą być w pełni zarządzane przez firmowa grupa IT ze ścisłych zasad zabezpieczeń, minimalnej kompilacji systemu operacyjnego, i obsługi modułu TPM.

Hello rysunku poniżej przenośny obraz powitania jest systemu przyłączonych do domeny, w którym jest tylko tooAzure tooconnect wstępnie skonfigurowane, wymagającym uwierzytelniania wieloskładnikowego i blokuje cały ruch-management. Jeśli uruchamianie użytkownika hello tego samego komputera toohello standardowego obrazu firmowego i prób dostępu do bramy usług pulpitu zdalnego dla narzędzi do zarządzania platformy Azure, sesja hello jest zablokowana. System operacyjny na poziomie głównym hello staje się tooGo systemu Windows i żadne dodatkowe warstwy są wymagane (host działania systemu, funkcji hypervisor, maszyna wirtualna) może to być bardziej narażony toooutside ataków.

![][4]

Jest ważne toonote czy dyski flash USB są łatwiejsze utracone niż przeciętnego komputera stacjonarnego. Korzystanie z funkcji BitLocker tooencrypt hello całego woluminu, silnego hasła, powoduje, że mniej prawdopodobne, osoba atakująca może wykorzystać hello obrazu dysku do szkodliwych celów. Ponadto jeśli dysk flash USB hello zostaną utracone, odwoływanie i [wystawienie nowego certyfikatu zarządzania](https://technet.microsoft.com/library/hh831574.aspx) wraz z szybkiego hasła resetowania można zmniejszyć prawdopodobieństwo ujawnienia danych. Dzienniki inspekcji administracyjnej znajdują się w obrębie platformy Azure, nie na powitania klienta, co dodatkowo zwiększa ryzyko utraty danych.

## <a name="best-practices"></a>Najlepsze praktyki
Należy wziąć pod uwagę hello następujące dodatkowe zalecenia podczas zarządzania aplikacji i danych na platformie Azure.

### <a name="dos-and-donts"></a>Zalecenia i zakazy
Nie wolno zakładać, że ponieważ stacji roboczej został zablokowany który innych wymagań dotyczących bezpieczeństwa nie są spełnione toobe. Witaj potencjalne ryzyko jest wyższe ze względu na podwyższony poziom kont administratorów. W poniższej tabeli hello przedstawiono przykładowe zagrożenia i alternatywne, bezpieczne praktyki.

| Zakazy | Zalecenia |
| --- | --- |
| Nie wysyłaj pocztą e-mail poświadczeń umożliwiających dostęp z uprawnieniami administratora ani innych informacji poufnych (na przykład certyfikatów SSL lub certyfikatów zarządzania) |Zachowaj poufność, przekazując nazwy kont i hasła werbalnie (ale nie nagrywaj ich na poczcie głosowej), wykonując zdalną instalację certyfikatów klienta/serwera (za pośrednictwem sesji zaszyfrowanej), pobierając je z chronionego udziału sieciowego lub przekazując osobiście na nośniku wymiennym. |
| - | Aktywnie zarządzaj cyklami życia certyfikatów zarządzania. |
| Nie przechowuj haseł nieszyfrowanych lub nieprzetworzonych za pomocą funkcji skrótu w magazynie aplikacji (takim jak arkusze kalkulacyjne, witryny programu SharePoint lub udziały plików). |Ustanowienia zasad zarządzania bezpieczeństwa i zwiększania bezpieczeństwa systemu oraz stosuj je tooyour Środowisko deweloperskie. |
| - | Użyj [Enhanced Mitigation Experience Toolkit 5.5](https://technet.microsoft.com/security/jj653751) przypinania certyfikatu zasady tooensure właściwy dostęp tooAzure SSL/TLS witryny. |
| Nie udostępniaj kont i haseł innym administratorom ani nie używaj ponownie tych samych haseł dla wielu kont użytkowników lub usług, zwłaszcza związanych z mediami społecznościowymi lub innymi działaniami niezwiązanymi z administrowaniem. |Utwórz dedykowane toomanage konta Microsoft subskrypcji platformy Azure — konto, które nie jest używany na potrzeby osobistej poczty e-mail. |
| Nie przesyłaj plików konfiguracji pocztą e-mail. |Profile i pliki konfiguracji należy instalować z zaufanego źródła (na przykład zaszyfrowanego dysku flash USB), a nie przy użyciu mechanizmu, którego zabezpieczenia można łatwo złamać, takiego jak poczta e-mail. |
| Nie używaj słabych lub prostych haseł do logowania. |Wymuszaj zasady silnych haseł, cykle wygaśnięcia (zmiana po pierwszym użyciu), limity czasu konsoli i automatyczne blokowanie kont. Używaj systemu zarządzania hasłami klientów z uwierzytelnianiem wieloskładnikowym do uzyskiwania dostępu do magazynu haseł. |
| Nie uwidacznia toohello porty zarządzania internetowego. |Blokowanie Azure portów i dostęp administracyjny toorestrict adresów IP. Aby uzyskać więcej informacji, zobacz hello [zabezpieczenia sieci Azure](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) oficjalny dokument. |
| - | Używaj zapór, sieci VPN i ochrony dostępu do sieci dla wszystkich połączeń związanych z zarządzaniem. |

## <a name="azure-operations"></a>Operacje platformy Azure
W związku z obsługą platformy Azure przez firmę Microsoft inżynierowie operacyjni i personel pomocy technicznej, uzyskujący dostęp do systemów produkcyjnych Azure, używają [stacji roboczych ze wzmocnionymi zabezpieczeniami z maszynami wirtualnymi](#stand-alone-hardened-workstation-for-management) aprowizowanymi na nich na potrzeby dostępu do wewnętrznej sieci firmy i aplikacji (takich jak poczta e-mail, intranet itp.). Moduły TPM mają wszystkie stacje robocze zarządzania, dysk rozruchowy hosta hello są szyfrowane za pomocą funkcji BitLocker i są one tooa przyłączone do specjalnej jednostki organizacyjnej (OU) w podstawowej domenie firmy Microsoft.

Wzmacnianie zabezpieczeń systemu jest wymuszane za pośrednictwem zasad grupy ze scentralizowanymi aktualizacjami oprogramowania. Dla inspekcją i analizą dzienniki zdarzeń (np. zabezpieczeń i funkcji AppLocker) są zbierane ze stacjami roboczymi do zarządzania i zapisywane tooa centralnej lokalizacji.

Ponadto dedykowane serwery przeskoku w sieci firmy Microsoft wymagające uwierzytelniania dwuskładnikowego są używane tooconnect tooAzure produkcyjnego środowiska sieciowego.

## <a name="azure-security-checklist"></a>Lista kontrolna zabezpieczeń platformy Azure
Minimalizowanie hello liczba zadań, które Administratorzy mogą wykonywać na stacji roboczej ze wzmocnionymi zabezpieczeniami minimalizuje hello ataku w środowisk zarządzania i programowania. Użyj hello następujące technologie toohelp ochronę stacji roboczej ze wzmocnionymi zabezpieczeniami:

* Wzmacnianie zabezpieczeń programu Internet Explorer. Witaj przeglądarki Internet Explorer (lub dowolnej przeglądarki sieci web istotnego dla badania) jest głównym punktem wejścia dla szkodliwego kodu z powodu tooits rozległych interakcji z serwerami zewnętrznymi. Przejrzyj zasady klienta i wymuś uruchamianie w trybie chronionym, co powoduje wyłączenie dodatków i pobierania plików oraz korzystanie z filtrowania [Microsoft SmartScreen](https://technet.microsoft.com/library/jj618329.aspx). Upewnij się, że ostrzeżenia dotyczące zabezpieczeń są wyświetlane. Korzystaj ze stref internetowych i utwórz listę zaufanych witryn, dla których skonfigurowano odpowiednie zabezpieczenia. Zablokuj wszystkie pozostałe witryny i kod w przeglądarce, np. ActiveX i Java.
* Użytkownik standardowy. Uruchomiona jako użytkownik standardowy jest związane z kilkoma korzyściami, których największą hello jest, że kradzieży poświadczeń administratora przy użyciu złośliwego oprogramowania staje się coraz trudniejsze. Ponadto konto użytkownika standardowego nie ma podwyższonych uprawnień w głównym systemie operacyjnym hello, a wiele opcji konfiguracji i interfejsów API są zablokowane domyślnie.
* Funkcja AppLocker. Można użyć [zasad ograniczeń oprogramowania](http://technet.microsoft.com/library/ee619725.aspx) toorestrict hello programy i skrypty, które użytkownicy mogą uruchamiać. Funkcję AppLocker można uruchomić w trybie inspekcji lub wymuszania. Domyślnie funkcja AppLocker ma regułę zezwalającą umożliwia użytkowników, którzy mają toorun token administratora całego kodu na powitania klienta. Ta reguła istnieje blokowaniu własnych kont administratorów tooprevent i są one stosowane tylko tokeny tooelevated. Zobacz też integralność kodu w ramach [podstawowych zabezpieczeń](http://technet.microsoft.com/library/dd348705.aspx) systemu Windows Server.
* Podpisywanie kodu. Podpisywanie kodu wszystkich narzędzi i skryptów używanych przez administratorów zapewnia mechanizm wdrażania zasad blokowania aplikacji, którym można zarządzać. Skróty nie skalują się przy szybkich zmianach kodu toohello i ścieżki plików nie zapewniają wysokiego poziomu zabezpieczeń. Połącz reguły funkcji AppLocker przy użyciu programu PowerShell [zasady wykonywania](http://technet.microsoft.com/library/ee176961.aspx) czy tylko umożliwia określonego podpisanego kodu i skrypty toobe [wykonywane](http://technet.microsoft.com/library/hh849812.aspx).
* Zasady grupy. Utwórz globalne zasady administracyjne, które jest stosowane tooany stacji roboczej w domenie, używanej do zarządzania (i Zablokuj dostęp ze wszystkich pozostałych), a toouser konta uwierzytelnione na tych stacjach roboczych.
* Bezpieczna aprowizacja. Zabezpieczenia obraz stacji roboczej ze wzmocnionymi zabezpieczeniami linii bazowej toohelp chronić je przed naruszeniem. Stosuj środki ochrony, takie jak szyfrowanie i izolacja toostore obrazów, maszyn wirtualnych i skryptów i ograniczenie dostępu (możliwe, że proces Użyj podlegającą inspekcji wyboru w/wyewidencjonowywanie).
* Stosowanie poprawek. Obsługa kompilację spójności (lub oddzielne obrazy dla rozwoju, operacje i innych zadań administracyjnych), skanowanie w poszukiwaniu zmian i złośliwego oprogramowania regularnie, Zachowaj hello stworzenie toodate i Uaktywniaj komputery tylko wtedy, gdy są potrzebne.
* Szyfrowanie. Upewnij się, że stacjami roboczymi do zarządzania toomore modułu TPM, bezpieczne korzystanie [systemu szyfrowania plików](https://technet.microsoft.com/library/cc700811.aspx) (EFS) i funkcji BitLocker. Jeśli używasz tooGo systemu Windows, należy użyć tylko zaszyfrowanych dysków USB wraz z funkcją BitLocker.
* Zarządzanie. Użyj toocontrol obiektów zasad grupy usługi AD DS systemu Windows w przypadku wszystkich administratorów hello interfejsy, takich jak udostępnianie plików. Uwzględnij stacje robocze używane do zarządzania w procesach inspekcji, monitorowania i rejestrowania. Śledź dostęp i używanie przez wszystkich administratorów i deweloperów.

## <a name="summary"></a>Podsumowanie
Użycie konfiguracji stacji roboczej ze wzmocnionymi zabezpieczeniami do administrowania usługami w chmurze, usługą Virtual Machines i aplikacjami platformy Azure może pomóc w uniknięciu licznych zagrożeń związanych ze zdalnym zarządzaniem newralgiczną infrastrukturą informatyczną. Zarówno Azure i Windows zapewniają mechanizmy, że zostanie zastosowana toohelp ochrony i kontrolowania komunikacji, uwierzytelniania i zachowania klientów.

## <a name="next-steps"></a>Następne kroki
Hello są następujące zasoby dostępne tooprovide więcej ogólnych informacji na temat platformy Azure i powiązanych usług firmy Microsoft, w elementach toospecific dodanie omówionych w tym dokumencie:

* [Zabezpieczanie uprzywilejowanego dostępu](https://technet.microsoft.com/library/mt631194.aspx) — Pobierz hello szczegółowe informacje techniczne dotyczące projektowania i konfigurowania bezpiecznej administracyjnej stacji roboczej do zarządzania platformą Azure
* [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Security/AzureSecurity) — informacje na temat funkcji platformy Azure, których ochrona powitalnych sieci szkieletowej Azure i hello obciążeń tego uruchamiane na platformie Azure
* [Microsoft Security Response Center](http://www.microsoft.com/security/msrc/default.aspx) — w przypadku, gdy mogą być zgłaszane luk w zabezpieczeniach firmy Microsoft, w tym problemów z platformą Azure, lub za pośrednictwem poczty e-mail zbyt[secure@microsoft.com](mailto:secure@microsoft.com)
* [Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/) — śledzenie toodate na powitania najnowszych zabezpieczeń platformy Azure

<!--Image references-->
[1]: ./media/azure-security-management/typical-management-network-topology.png
[2]: ./media/azure-security-management/stand-alone-hardened-workstation-topology.png
[3]: ./media/azure-security-management/hardened-workstation-enabled-with-hyper-v.png
[4]: ./media/azure-security-management/hardened-workstation-using-windows-to-go-on-a-usb-flash-drive.png
