---
title: "aaaSettings i dane mobilne — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Udostępnia toosome odpowiedzi na pytania Administratorzy IT mogą mieć o ustawieniach i synchronizacji danych aplikacji."
services: active-directory
keywords: "Enterprise mobilnego ustawienia stanu, chmury systemu windows, często zadawane pytania na roamingu stanu przedsiębiorstwa"
documentationcenter: 
author: tanning
manager: swadhwa
editor: curtand
ms.assetid: c0824f5c-129b-4240-969f-921f6a64eae7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4d6d6619b3a5fbd1d274603808d89b73ed942cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="settings-and-data-roaming-faq"></a>Roaming ustawień i danych — często zadawane pytania
W tym temacie odpowiedzi na pytania Administratorzy IT mogą mieć o ustawieniach i synchronizacji danych aplikacji.

## <a name="what-data-roams"></a>Jakie dane uzyskuje mobilny dostęp?
**Ustawienia systemu Windows**: hello ustawienia komputera, które są wbudowane w system operacyjny Windows hello. Ogólnie rzecz biorąc ustawienia, które personalizowanie komputera i zawierają hello następujące kategorie:

* *Motyw*, która obejmuje funkcje, takie jak ustawienia motywu i paska zadań pulpitu.
* *Ustawienia programu Internet Explorer*, w tym ostatnio otwartą kart i Ulubione.
* *Ustawienia przeglądarki krawędzi*, na przykład Ulubione i odczytu listy.
* *Hasła*, w tym hasła internetowe, profile sieci Wi-Fi i inne.
* *Preferencje językowe*, w tym ustawienia układów klawiatury, język systemu, Data i czas i więcej.
* *Łatwość dostępu do funkcji*, na przykład motywu dużego kontrastu, Narrator i Lupa.
* *Inne ustawienia systemu Windows*, takie jak ustawienia wiersza polecenia i listy aplikacji.

**Dane aplikacji**: aplikacji uniwersalnych systemu Windows można zapisać ustawień tooa danych mobilnych folder i wszystkie dane zapisane w folderze toothis zostaną automatycznie zsynchronizowane. Działa toohello poszczególnych aplikacji developer toodesign aplikacji tootake z zalet tej możliwości. Aby uzyskać więcej informacji o toodevelop aplikacji uniwersalnej systemu Windows, który korzysta z roamingu, zobacz temat hello [magazynu appdata interfejsu API](https://msdn.microsoft.com/library/windows/apps/mt299098.aspx) i hello [appdata systemu Windows 8 roamingu blog deweloperów](http://blogs.msdn.com/b/windowsappdev/archive/2012/07/17/roaming-your-app-data.aspx).

## <a name="what-account-is-used-for-settings-sync"></a>Jakie konto jest używane do synchronizacji ustawień?
W systemie Windows 8 i Windows 8.1 ustawienia synchronizacji zawsze używany kont Microsoft konsumenta. Użytkownicy w organizacji mają tooconnect możliwości hello tootheir konta Microsoft synchronizacja toosettings dostępu toogain z kontem domeny usługi Active Directory. W systemie Windows 10 to połączone konto Microsoft, że funkcja jest zastępowany framework podstawowego i pomocniczego konta.

kontem podstawowym Hello jest zdefiniowany jako konto hello używane toosign w tooWindows. Może to być konto Microsoft, konto usługi Azure Active Directory (Azure AD), konta lokalne usługi Active Directory lub konta lokalnego. W dodanie toohello kontem podstawowym użytkownicy systemu Windows 10 można dodać jeden lub więcej urządzeń tootheir kont dodatkowej chmury. Drugie konto jest zazwyczaj kontem Microsoft, konta usługi Azure AD lub niektóre inne konto, takie jak Gmail lub Facebook. Te konta dodatkowej tooadditional usług, takich jak logowanie jednokrotne i Sklepu Windows hello zapewnić dostęp, ale nie są one w stanie synchronizacji ustawień zasilania.

W systemie Windows 10, tylko hello kontem podstawowym hello urządzenia może służyć do synchronizacji ustawień (zobacz [jak uaktualnić synchronizację ustawień konta Microsoft w systemie Windows 8 tooAzure AD ustawienia synchronizacji w systemie Windows 10?](active-directory-windows-enterprise-state-roaming-faqs.md#how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-to-azure-ad-settings-sync-in-windows-10)).

Dane nigdy nie jest mieszana między hello różne konta użytkownika na urządzeniu hello. Istnieją dwie reguły synchronizacji ustawień:

* Ustawienia systemu Windows będzie zawsze są przekazywane z kontem podstawowym hello.
* Dane aplikacji zostaną oznaczone hello konto używane tooacquire hello aplikacji. Tylko aplikacje z kontem podstawowym hello zostanie zsynchronizowany. Znakowanie własność aplikacji jest określana, gdy aplikacja jest ładowana za pośrednictwem Sklepu Windows hello lub zarządzania urządzeniami przenośnymi (MDM).

Jeśli nie można zidentyfikować właściciela aplikacji, będą są przekazywane z kontem podstawowym hello. Jeśli urządzenie jest uaktualniony z systemu Windows 8 lub Windows 8.1 tooWindows 10, wszystkie aplikacje hello zostanie oznaczone jako uzyskaną przez hello konta Microsoft. Jest tak, ponieważ większość użytkowników uzyskać aplikacje do Sklepu Windows hello, a nie było Sklepu Windows nie obsługuje wcześniejsze tooWindows kont usługi Azure AD 10. Jeśli aplikacja zostanie zainstalowana przy użyciu licencję w trybie offline, aplikacja hello zostanie oznaczone za pomocą konta podstawowego hello na urządzeniu hello.

> [!NOTE]
> Urządzeń z systemem Windows 10, które są należących do przedsiębiorstwa i połączone tooAzure AD już nie mogą łączyć swoje konta domeny tooa konta Microsoft. Witaj tooconnect możliwości konta domeny tooa konta Microsoft i mają wszystkie użytkownika hello synchronizacji danych toohello konta Microsoft (to znaczy hello konta Microsoft mobilnych za pomocą konta Microsoft hello podłączone i funkcjonalności usługi Active Directory) zostanie usunięty z Urządzeń z systemem Windows 10, które są przyłączone do tooa połączone usługi Active Directory lub środowiska usługi Azure AD.
>
>

## <a name="how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-tooazure-ad-settings-sync-in-windows-10"></a>Jak uaktualnić z synchronizację ustawień konta Microsoft w systemie Windows 8 tooAzure AD ustawienia synchronizacji w systemie Windows 10?
Jeśli jesteś toohello przyłączone do domeny usługi Active Directory systemem Windows 8 lub Windows 8.1 z kontem Microsoft połączonych zsynchronizuje ustawienia za pomocą konta Microsoft. Po uaktualnieniu tooWindows 10, będzie nadal toosync ustawienia użytkownika za pomocą konta Microsoft, jak długo użytkownik jest użytkownikiem domeny i domeny usługi Active Directory hello nie łączy się z usługą Azure AD.

Jeśli hello lokalnej domeny usługi Active Directory połączenia z usługą Azure AD, urządzenie będzie podejmować toosync ustawień za pomocą hello połączone konta usługi Azure AD. Jeśli administrator hello Azure AD nie obsługuje roamingu stanu przedsiębiorstwa, z połączonych konto usługi Azure AD przestanie Synchronizowanie ustawień. Jeśli użytkownik jest użytkownikiem systemu Windows 10, a następnie zaloguj się przy użyciu tożsamości usługi Azure AD, rozpocznie synchronizację ustawień systemu windows, jak administrator włącza ustawienia synchronizacji za pomocą usługi Azure AD.

Jeśli wszystkie dane osobowe są przechowywane na urządzeniu firmowych, należy pamiętać, że systemu operacyjnego i danych aplikacji rozpocznie się synchronizowanie tooAzure AD. To ustawienie hello następujące konsekwencje:

* Ustawienia osobiste konto Microsoft będzie rozchodzenia oprócz ustawienia hello w pracy lub szkołą konta usługi Azure AD. Jest to spowodowane konta Microsoft hello i ustawień usługi Azure AD synchronizowane są teraz przy użyciu osobnych kont.
* Dane osobowe, takie jak hasła sieci Wi-Fi, sieci web, poświadczeń i Ulubione programu Internet Explorer, które wcześniej zostały zsynchronizowane przez połączone konto Microsoft zostaną zsynchronizowane za pomocą usługi Azure AD.

## <a name="how-do-microsoft-account-and-azure-ad-enterprise-state-roaming-interoperability-work"></a>Jak konta Microsoft i pracy współdziałanie Roaming stanu przedsiębiorstwa usług Azure AD?
W hello listopad 2015 lub nowszymi wersjami systemu Windows 10 roamingu stanu przedsiębiorstwa jest obsługiwana tylko dla jednego konta w czasie. Jeśli tooWindows Zaloguj się przy użyciu służbowe konto usługi Azure AD, wszystkie dane zostaną zsynchronizowane za pomocą usługi Azure AD. Jeśli tooWindows Zaloguj się za pomocą osobistego konta Microsoft, wszystkie dane zostaną zsynchronizowane za pomocą konta Microsoft hello. Uniwersalny appdata będzie są przekazywane za pomocą tylko hello głównej konto logowania na urządzeniu hello i będzie są przekazywane tylko wtedy, gdy licencji aplikacji hello jest własnością podstawowego konta hello. Uniwersalny appdata dla aplikacji hello właścicielem żadnych kont nie będą synchronizowane.

## <a name="do-settings-sync-for-azure-ad-accounts-from-multiple-tenants"></a>Czy ustawienia synchronizacji dla konta usługi Azure AD z wieloma dzierżawcami?
Kiedy usługi Azure AD wielu kont z różnych dzierżaw usługi Azure AD znajdują się na powitania jednym urządzeniu, należy zaktualizować toocommunicate rejestru hello urządzenia za pomocą usługi Azure Rights Management (Azure RMS) dla każdego dzierżawcy usługi Azure AD.  

1. Znajdź hello identyfikatora GUID dla każdego dzierżawcy usługi Azure AD. Otwórz hello klasycznego portalu Azure i wybierz dzierżawa usługi Azure AD. Hello identyfikatora GUID dla dzierżawcy hello jest w adresie URL hello hello pasku adresu przeglądarki. Na przykład: `https://manage.windowsazure.com/YourAccount.onmicrosoft.com#Workspaces/ActiveDirectoryExtension/Directory/Tenant GUID/directoryQuickStart`
2. Po umieszczeniu hello identyfikatora GUID, konieczne będzie klucza rejestru hello tooadd **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\SettingSync\WinMSIPC\<dzierżawy Identyfikatora GUID >**.
   Z hello **dzierżawy Identyfikatora GUID** kluczy, Utwórz nową wartość ciągu wielokrotnego (REG-MULTI-SZ) o nazwie **AllowedRMSServerUrls**. W przypadku jego danych określ hello licencjonowania adresy URL punktu dystrybucji hello innych dzierżawców Azure hello uzyskuje dostęp do urządzenia.
3. Można znaleźć hello licencjonowania adresy URL punktu dystrybucji przez uruchomienie hello **Get-AadrmConfiguration** polecenia cmdlet. Jeśli wartości hello hello **LicensingIntranetDistributionPointUrl** i **LicensingExtranetDistributionPointUrl** są różne, określ obie wartości. Jeśli hello wartości są takie same Witaj, należy określić wartość hello tylko raz.

## <a name="what-are-hello-roaming-settings-options-for-existing-windows-desktop-applications"></a>Jakie są opcje mobilnego ustawienia hello istniejących aplikacji klasycznych systemu Windows?
Roaming działa tylko dla aplikacji uniwersalnych systemu Windows. Dostępne są dwie opcje do włączania mobilnego na istniejącą aplikację pulpitu systemu Windows:

* Witaj [Mostek pulpitu](http://aka.ms/desktopbridge) pomaga Przełącz z istniejącej aplikacji klasycznych systemu Windows toohello platformy uniwersalnej systemu Windows. W tym miejscu minimalnego kodu, który będzie zmiany wymagane zaletą tootake mobilne dane aplikacji Azure AD. Hello Mostek pulpitu udostępnia aplikacje przy użyciu tożsamości aplikacji, co jest potrzebne tooenable dane aplikacji mobilnych dla istniejącej aplikacji klasycznych.
* [Wirtualizacji środowiska użytkownika (UE-V)](https://technet.microsoft.com/library/dn458947.aspx) pomaga utworzyć ustawienia niestandardowe szablon dla istniejącej aplikacji klasycznych systemu Windows i włączyć mobilnych dla aplikacji Win32. Ta opcja nie wymaga kodu toochange Deweloper aplikacji hello aplikacji hello. Wirtualizacji środowiska użytkownika jest ograniczona lokalnych tooon Active Directory mobilnego dla klientów, którzy kupili hello pakietu Microsoft Desktop Optimization Pack.

Administratorzy mogą skonfigurować danych aplikacji klasycznej systemu Windows tooroam wirtualizacji środowiska użytkownika, zmieniając roaming ustawień systemu operacyjnego i danych aplikacji uniwersalnej za pośrednictwem [wirtualizacji środowiska użytkownika, zasady grupy](https://technet.microsoft.com/itpro/mdop/uev-v2/configuring-ue-v-2x-with-group-policy-objects-both-uevv2), takie jak:

* Są przekazywane zasad grupy ustawienia systemu Windows
* Nie Synchronizuj zasad grupy aplikacji systemu Windows
* Roaming w sekcji aplikacji hello w programie Internet Explorer

W przyszłości hello firma Microsoft może zbadać toomake sposoby, które wirtualizacji środowiska użytkownika głęboko zintegrowana z systemem Windows i rozszerzyć ustawienia tooroam UE-V za pośrednictwem hello Azure AD cloud.

## <a name="can-i-store-synced-settings-and-data-on-premises"></a>Lokalnie może przechowywać zsynchronizowane ustawienia i dane?
Roamingu stanu przedsiębiorstwa są przechowywane wszystkie zsynchronizowane dane hello chmury Azure. UE-V oferuje lokalnego roamingu rozwiązania.

## <a name="who-owns-hello-data-thats-being-roamed"></a>Kto jest właścicielem danych hello jest są przekazywane?
Witaj przedsiębiorstw hello własne dane przekazywane za pośrednictwem roamingu stanu przedsiębiorstwa. Dane są przechowywane w centrum danych Azure. Wszystkie dane użytkownika są szyfrowane, zarówno przesyłanych i przechowywanych w chmurze hello przy użyciu usługi Azure RMS. Jest to ulepszenia w porównaniu tooMicrosoft konta na podstawie ustawienia synchronizacji, który szyfruje tylko niektórych poufnych danych, takich jak poświadczeń użytkownika przed opuszczeniem hello urządzenia.

Firma Microsoft dokłada danych klienta toosafeguarding zatwierdzone. Dane ustawienia użytkownika w organizacji jest automatycznie szyfrowane przez usługę Azure RMS przed opuszczeniem urządzenia z systemem Windows 10, więc żaden inny użytkownik może odczytywać te dane. Jeśli Twoja organizacja ma płatną subskrypcję usługi Azure RMS, można korzystanie z innych funkcji usługi Azure RMS, takie jak śledzenie i odwoływanie dokumentów, automatycznie chronić wiadomości e-mail zawierające poufne informacje i zarządzanie własnych kluczy (Witaj "bring your own key" rozwiązania również znana jako BYOK). Aby uzyskać więcej informacji o tych funkcjach i jak działa usługa Azure RMS, zobacz [co to jest usługa Azure Rights Management](https://technet.microsoft.com/jj585026.aspx).

## <a name="can-i-manage-sync-for-a-specific-app-or-setting"></a>Można zarządzać synchronizacji dla określonej aplikacji lub ustawienie?
W systemie Windows 10 nie ma żadnych toodisable ustawienie zarządzania urządzeniami Przenośnymi lub zasad grupy, mobilnych dla poszczególnych aplikacji. Administratorzy dzierżawy mogą wyłączyć appdata synchronizacji dla wszystkich aplikacji na urządzeniach zarządzanych, ale nie nie bardziej precyzyjną kontrolę na poziomie aplikacji lub w aplikacji.

## <a name="how-can-i-enable-or-disable-roaming"></a>Jak włączyć lub wyłączyć mobilnych?
W hello **ustawienia** aplikacji, przejdź do zbyt**kont** > **Synchronizuj swoje ustawienia**. Na tej stronie mogą zobaczyć konto, które są używane tooroam ustawienia, a można włączyć lub wyłączyć poszczególne grupy ustawień toobe przekazywane.

## <a name="what-is-microsofts-recommendation-for-enabling-roaming-in-windows-10"></a>Co to jest zalecenia firmy Microsoft umożliwiających roaming w systemie Windows 10?
Firma Microsoft udostępnia kilka różnych ustawień roamingu rozwiązań, łącznie z profilów użytkowników mobilnych, UE-V i roamingu stanu przedsiębiorstwa.  Firma Microsoft dokłada zatwierdzone toomaking inwestycji w stanie Enterprise Roaming w przyszłych wersjach systemu Windows. Jeśli Twoja organizacja nie jest gotowy lub doświadczenia z toohello przenoszenie danych w chmurze, następnie firma Microsoft zaleca użycie wirtualizacji środowiska użytkownika jako podstawowy technologii mobilnych. Jeśli Twoja organizacja wymaga roaming obsługę istniejących aplikacji pulpitu systemu Windows, ale jest wczesny toomove toohello chmury, firma Microsoft zaleca korzystanie z roamingu stanu przedsiębiorstwa i wirtualizacji środowiska użytkownika. Mimo że UE-V i roamingu stanu przedsiębiorstwa są bardzo podobne technologie, nie są one wykluczają się wzajemnie. One uzupełniają toohelp zagwarantować, że Twoja organizacja zapewnia hello usługi, które wymagają użytkowników mobilnych.  

Korzystając z roamingu stanu przedsiębiorstwa i wirtualizacji środowiska użytkownika, zastosuj hello następujące reguły:

* Roamingu stanu przedsiębiorstwa jest hello głównej agenta roamingu na urządzeniu hello. UE V są używane toosupplement hello "Przerwa Win32".
* Powinno zostać wyłączone wirtualizacji środowiska użytkownika mobilnego dla ustawienia systemu Windows i nowoczesne danych aplikacji platformy uniwersalnej systemu Windows, gdy zasady grupy hello wirtualizacji środowiska użytkownika. Te są już objęte roamingu stanu przedsiębiorstwa.

## <a name="how-does-enterprise-state-roaming-support-virtual-desktop-infrastructure-vdi"></a>W jaki sposób roamingu stanu przedsiębiorstwa obsługuje infrastrukturę pulpitu wirtualnego (VDI)?
Roamingu stanu przedsiębiorstwa jest obsługiwana na kliencie systemu Windows 10 jednostki SKU, ale nie na serwerze jednostki SKU. Jeśli klient maszyna wirtualna znajduje się na komputerze funkcji hypervisor i zdalnie Zaloguj toohello maszyny wirtualnej, dane będą są przekazywane. Jeśli wielu użytkowników udziału powitalne tego samego systemu operacyjnego i użytkowników zdalnie Zaloguj tooa serwera do obsługi całego pulpitu, roamingu może nie działać. Scenariusz Hello ostatnie opartymi na sesji nie jest oficjalnie obsługiwana.

## <a name="what-happens-when-my-organization-purchases-azure-rms-after-using-roaming"></a>Co się stanie, jeśli Moja organizacja zakupi usługi Azure RMS, po zakończeniu korzystania z roamingu?
Jeśli Twoja organizacja korzysta już roaming w systemie Windows 10 z hello Azure RMS ograniczonej bezpłatnej subskrypcji zakupu płatnej subskrypcji usługi Azure RMS nie będą miały wpływu na działanie hello funkcji mobilnych hello i będzie bez zmian konfiguracji wymagane przez administratora IT.

## <a name="known-issues"></a>Znane problemy
Zobacz dokumentację hello w hello [Rozwiązywanie problemów z](active-directory-windows-enterprise-state-roaming-troubleshooting.md) sekcja zawiera listę znanych problemów. 

## <a name="related-topics"></a>Powiązane tematy
* [Przegląd roamingu stanu przedsiębiorstwa](active-directory-windows-enterprise-state-roaming-overview.md)
* [Włącz roaming stanu przedsiębiorstwa w usłudze Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md)
* [Zasady grupy i ustawienia zarządzania urządzeniami Przenośnymi dla ustawień synchronizacji](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Informacje dotyczące ustawień roamingu systemu Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Rozwiązywanie problemów](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
