---
title: "aaaAzure Centrum zabezpieczeń — często zadawane pytania (FAQ) | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania odpowiedzi na pytania dotyczące Centrum zabezpieczeń Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: be2ab6d5-72a8-411f-878e-98dac21bc5cb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: cd0c0f8bdf15cdaf5889f2da5ac3cadf6017a9e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-frequently-asked-questions-faq"></a>Często zadawane pytania dotyczące usługi Azure Security Center
Często zadawane pytania odpowiedzi na pytania dotyczące Centrum zabezpieczeń Azure to usługa, która pomaga zapobiec, wykrywania i odpowie toothreats lepszy wgląd w i kontroli nad hello bezpieczeństwa zasobów na platformie Microsoft Azure.

> [!NOTE]
> Począwszy od początku czerwca 2017, Centrum zabezpieczeń użyj toocollect Microsoft Monitoring Agent hello i przechowywania danych. toolearn więcej, zobacz [migracji Platform Centrum zabezpieczeń Azure](security-center-platform-migration.md). Witaj informacje w tym artykule reprezentuje funkcji Centrum zabezpieczeń po toohello przejścia programu Microsoft Monitoring Agent.
>
>

## <a name="general-questions"></a>Pytania ogólne
### <a name="what-is-azure-security-center"></a>Co to jest Centrum zabezpieczeń Azure?
Centrum zabezpieczeń Azure ułatwia zapobieganie, wykrywania i odpowie toothreats lepszy wgląd w i kontroli nad hello zabezpieczeń zasobów platformy Azure. Umożliwia zintegrowane monitorowanie zabezpieczeń i zarządzanie zasadami dla wszystkich subskrypcji, pomaga wykrywać zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone, a także współpracuje z szerokim ekosystemem rozwiązań zabezpieczających.

### <a name="how-do-i-get-azure-security-center"></a>Jak uzyskać Centrum zabezpieczeń Azure?
Centrum zabezpieczeń Azure jest włączone w ramach subskrypcji Microsoft Azure i są dostępne w hello [portalu Azure](https://azure.microsoft.com/features/azure-portal/). ([Zaloguj się w portalu toohello](https://portal.azure.com), wybierz pozycję **Przeglądaj**i przewiń zbyt**Centrum zabezpieczeń**).  

## <a name="billing"></a>Rozliczenia
### <a name="how-does-billing-work-for-azure-security-center"></a>Jak działa rozliczeń dla Centrum zabezpieczeń Azure?
Centrum zabezpieczeń jest oferowana w dwóch warstw:

Witaj **warstwę bezpłatna** zapewnia wgląd w hello stan zabezpieczeń zasobów platformy Azure, zasady zabezpieczeń podstawowych, zalecenia dotyczące zabezpieczeń i integracja z produktów i usług zabezpieczeń partnerów.

Witaj **warstwy standardowa** dodaje zagrożeń zaawansowane możliwości wykrywania, takie jak zagrożenia analizy, analizy behawioralnej, wykrywania anomalii, przypadki naruszenia zabezpieczeń i zagrożenia autorstwa raportów. Hello warstwy standardowa zwolnieniu dla hello pierwsze 60 dni. Możesz wybrać toocontinue toouse hello usługi ponad 60 dni automatycznie Rozpoczniemy toocharge hello usługi.  tooupgrade, wybierz opcję warstwy cenowej w hello [zasady zabezpieczeń](security-center-policies.md#set-security-policies). toolearn więcej, zobacz [cennik Centrum zabezpieczeń](security-center-pricing.md).

## <a name="permissions"></a>Uprawnienia
Centrum zabezpieczeń Azure używa [kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md), która zapewnia [wbudowane role](../active-directory/role-based-access-built-in-roles.md) mogą być przypisane toousers, grup i usług Azure.

Centrum zabezpieczeń ocenia konfiguracji hello problemy z zabezpieczeniami tooidentify zasobów i luk w zabezpieczeniach. W Centrum zabezpieczeń widoczne są tylko informacje dotyczące zasobów tooa po przypisaniu roli hello właściciela, współautora lub czytelnika dla grupy zasobów lub subskrypcji hello należącą do zasobu.

Zobacz [uprawnienia w Centrum zabezpieczeń Azure](security-center-permissions.md) toolearn więcej informacji na temat ról i akcji dozwolonych w Centrum zabezpieczeń.

## <a name="data-collection"></a>Zbieranie danych
Centrum zabezpieczeń zbiera dane z Twojego tooassess maszyn wirtualnych stanu zabezpieczeń, podaj zalecenia dotyczące zabezpieczeń i alertów toothreats. Jeśli najpierw przejść do Centrum zabezpieczeń zbieranie danych jest włączone na wszystkich maszynach wirtualnych w ramach subskrypcji. Można również włączyć zbieranie danych w hello zasadami Centrum zabezpieczeń.

### <a name="how-do-i-disable-data-collection"></a>Jak wyłączyć zbieranie danych?
Jeśli korzystasz z warstwy bezpłatna Centrum zabezpieczeń Azure hello, możesz wyłączyć zbieranie danych z maszyn wirtualnych w dowolnym momencie. Zbieranie danych jest wymagane dla subskrypcji w warstwie standardowa hello. Możesz wyłączyć zbieranie danych w ramach subskrypcji w hello zasady zabezpieczeń. ([Zaloguj się w portalu Azure toohello](https://portal.azure.com), wybierz pozycję **Przeglądaj**, wybierz pozycję **Centrum zabezpieczeń**i wybierz **zasad**.)  Po wybraniu subskrypcji nowy blok otwiera i udostępnia hello tooturn opcji poza **zbierania danych**.

### <a name="how-do-i-enable-data-collection"></a>Jak włączyć zbieranie danych?
Zbieranie danych można włączyć dla Twojej subskrypcji platformy Azure w hello zasady zabezpieczeń. zbieranie danych tooenable. [Zaloguj się w portalu Azure toohello](https://portal.azure.com), wybierz pozycję **Przeglądaj**, wybierz pozycję **Centrum zabezpieczeń**i wybierz **zasad**. Ustaw **zbierania danych** za**na**.

### <a name="what-happens-when-data-collection-is-enabled"></a>Co się stanie po włączeniu funkcji zbierania danych?
Po włączeniu funkcji zbierania danych hello Microsoft Monitoring Agent jest udostępniany automatycznie na wszystkich istniejących i nowych obsługiwanych maszyn wirtualnych, które są wdrażane w hello subskrypcji.

### <a name="does-hello-monitoring-agent-impact-hello-performance-of-my-servers"></a>Czy hello agenta monitorowania wpływ hello wydajności serwerów?
Hello agent zużywa nominalnego ilość zasobów systemowych i powinna mieć mały wpływ na wydajność hello. Aby uzyskać więcej informacji dotyczących wpływu na wydajność i hello agent i rozszerzenia, zobacz hello [przewodnik dotyczący planowania i operacje](security-center-planning-and-operations-guide.md#data-collection-and-storage).

### <a name="where-is-my-data-stored"></a>Gdzie są przechowywane moje dane?
Dane zbierane z tego agenta są przechowywane w istniejącym obszarem roboczym analizy dzienników skojarzonych z Twoją subskrypcją lub nowego obszaru roboczego. Aby uzyskać więcej informacji, zobacz [bezpieczeństwo danych](security-center-data-security.md).

## <a name="using-azure-security-center"></a>Korzystanie z Centrum zabezpieczeń Azure
### <a name="what-is-a-security-policy"></a>Co to jest zasady zabezpieczeń?
Zasady zabezpieczeń definiuje zestaw hello formantów, które są zalecane dla zasobów w ramach hello określonej subskrypcji. W Centrum zabezpieczeń Azure można zdefiniować zasady dla subskrypcji platformy Azure zgodnie z wymagań dotyczących zabezpieczeń tooyour firmy i typem aplikacji hello lub czułości hello danych w każdej subskrypcji.

Witaj zasady zabezpieczeń włączone w Centrum zabezpieczeń Azure dysku — zalecenia dotyczące zabezpieczeń i monitorowania. toolearn więcej informacji na temat zasad zabezpieczeń, zobacz [monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md).

### <a name="who-can-modify-a-security-policy"></a>Kto może modyfikować zasady zabezpieczeń?
toomodify zasady zabezpieczeń, musi być administratorem zabezpieczeń lub właścicielem lub współautorem subskrypcji.

toolearn tooconfigure zasady zabezpieczeń, zobacz temat [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md).

### <a name="what-is-a-security-recommendation"></a>Jaka jest zalecana ze względów bezpieczeństwa?
Centrum zabezpieczeń Azure analizuje hello stan zabezpieczeń zasobów platformy Azure. Po potencjalnych luk w zabezpieczeniach, tworzone są zalecenia. Przewodnik zalecenia Hello użytkownika przez proces konfigurowania hello hello potrzebne formantu. Przykłady to:

* Inicjowanie obsługi administracyjnej ochrony przed złośliwym kodem toohelp identyfikacji i usuwania złośliwego oprogramowania
* Konfigurowanie [grup zabezpieczeń sieci](../virtual-network/virtual-networks-nsg.md) i reguł toocontrol ruchu toovirtual maszyny
* Inicjowanie obsługi administracyjnej toohelp zapory aplikacji sieci web chronić przed atakami przeznaczonych dla aplikacji sieci web
* Wdrażanie brakujących aktualizacji systemu
* Modyfikowanie konfiguracji systemu operacyjnego, które nie odpowiadają hello zalecanych planów bazowych

Tylko te zalecenia, które są włączone w zasadach zabezpieczeń są wyświetlane tutaj.

### <a name="how-can-i-see-hello-current-security-state-of-my-azure-resources"></a>Jak wyświetlić bieżący stan zabezpieczeń hello Moje zasobów platformy Azure?
Witaj **Omówienie Centrum zabezpieczeń** bloku pokazuje hello ogólny stan zabezpieczeń środowiska według obliczeniowych, sieci, magazynu i danych i aplikacji. Każdy typ zasobu ma przedstawiający wskaźnika, jeśli zidentyfikowano wszelkich potencjalnych luk w zabezpieczeniach. Kliknięcie każdego kafelka powoduje wyświetlenie listy problemów dotyczących zabezpieczeń, zidentyfikowane przez Centrum zabezpieczeń, razem ze spisem hello zasobów w ramach subskrypcji.

### <a name="what-triggers-a-security-alert"></a>Co to jest wyzwalane alert zabezpieczeń?
Centrum zabezpieczeń Azure automatycznie gromadzi, analizuje i fuses dane dzienników z zasobów platformy Azure, hello sieci i rozwiązań partnerskich, takich jak ochrony przed złośliwym oprogramowaniem i zapory. Po wykryciu zagrożenia tworzony jest alert zabezpieczeń. Przykłady obejmują wykrywanie:

* Zagrożonych maszyn wirtualnych komunikujących się ze znanymi złośliwymi adresami IP
* Zaawansowanego złośliwego oprogramowania wykrytego za pomocą raportowanie błędów systemu Windows
* Ataków siłowych wobec maszyn wirtualnych
* Alerty zabezpieczeń ze zintegrowanych zabezpieczeń rozwiązań partnerskich, takich jak przed złośliwym oprogramowaniem i zapór aplikacji sieci Web

### <a name="whats-hello-difference-between-threats-detected-and-alerted-on-by-microsoft-security-response-center-versus-azure-security-center"></a>Co to jest hello różnica między zagrożenia wykryte i alerty o przez Microsoft Security Response Center lub Centrum zabezpieczeń Azure?
Hello Microsoft Security odpowiedzi Center (MSRC) wykonuje monitorowanie zabezpieczeń wybierz hello sieć platformy Azure i infrastruktury i odbiera zagrożeń analizy i nadużycia utrudnień od osób trzecich. Gdy MSRC świadomość, czy dane klienta uzyskano dostęp przez stronę bezprawnego lub nieautoryzowane lub użycie tego klienta hello Azure nie jest zgodne z hello warunków do użycia dopuszczalne, Menedżer zdarzenia zabezpieczeń powiadamia powitania klienta. Powiadomienia zwykle występuje, wysyłając zabezpieczeń toohello e-mail kontaktów określone w Centrum zabezpieczeń Azure lub hello właściciela subskrypcji platformy Azure, jeśli nie określono kontaktu zabezpieczeń.

Centrum zabezpieczeń jest usługą platformy Azure, która stale monitoruje powitania klienta środowiska platformy Azure i stosuje analytics tooautomatically wykryć szeroką gamę potencjalnie złośliwych działań. Wykrywane odmiany są udostępniane jako alerty zabezpieczeń na pulpicie nawigacyjnym Centrum zabezpieczeń hello.

### <a name="which-azure-resources-are-monitored-by-azure-security-center"></a>Zasoby platformy Azure są monitorowane przez Centrum zabezpieczeń Azure?
Centrum zabezpieczeń Azure monitoruje hello następujących zasobów platformy Azure:

* Maszynach wirtualnych (VM) (w tym [usługi w chmurze](../cloud-services/cloud-services-choose-me.md))
* Sieci wirtualne platformy Azure
* Usługi SQL Azure
* Konto usługi Azure Storage
* Aplikacje sieci Web Azure (w [środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md))
* Partnerskich rozwiązań zintegrowanych z subskrypcją platformy Azure, takich jak Zapora aplikacji sieci web na maszynach wirtualnych i na [środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md)

## <a name="virtual-machines"></a>Maszyny wirtualne
### <a name="what-types-of-virtual-machines-are-supported"></a>Jakie typy maszyn wirtualnych są obsługiwane?
Monitorowanie i zalecenia są dostępne dla maszyn wirtualnych (VM) utworzone za pomocą obu hello [klasycznego i modeli wdrażania usługi Resource Manager](../azure-classic-rm.md).

Zobacz [obsługiwanych platform w Centrum zabezpieczeń Azure](security-center-os-coverage.md) listę obsługiwanych platform.

### <a name="why-doesnt-azure-security-center-recognize-hello-antimalware-solution-running-on-my-azure-vm"></a>Dlaczego nie rozpoznaje hello ochrony przed złośliwym kodem działającej na maszynie Wirtualnej platformy Azure w Centrum zabezpieczeń Azure?
Centrum zabezpieczeń Azure ma wgląd w ochrony przed złośliwym oprogramowaniem, zainstalowanych przy użyciu rozszerzeń Azure. Na przykład Centrum zabezpieczeń nie jest możliwe toodetect przed złośliwym kodem, który został wstępnie zainstalowany na podane obrazu lub jeśli ochrony przed złośliwym kodem jest zainstalowany na maszynach wirtualnych przy użyciu własnych procesów (takich jak systemy zarządzania konfiguracją).

### <a name="why-do-i-get-hello-message-missing-scan-data-for-my-vm"></a>Dlaczego otrzymuję błąd wiadomości powitania "Brakujących danych skanowania" Moje maszyny wirtualnej?
Ten komunikat jest wyświetlany, gdy nie ma żadnych danych skanowania dla maszyny Wirtualnej. Po włączeniu funkcji zbierania danych w Centrum zabezpieczeń Azure może upłynąć trochę czasu (mniej niż godzinę), zanim toopopulate danych skanowania. Po początkowej populacji hello danych skanowania ponieważ nie ma żadnych danych skanowania w ogóle lub nie ma żadnych ostatnich danych skanowania może zostać wyświetlony ten komunikat. Skanowanie nie należy wypełniać dla maszyny Wirtualnej w stanie zatrzymania. Ten komunikat może również zostać wyświetlony, jeśli dane skanowania nie został wypełniony ostatnio (zgodnie z zasadami przechowywania powitania dla agenta systemu Windows hello, który ma wartość domyślną w ciągu 30 dni).

### <a name="why-do-i-get-hello-message-vm-agent-is-missing"></a>Dlaczego otrzymuję błąd wiadomości powitania "Agent maszyny Wirtualnej jest Brak?"
Witaj agenta maszyny Wirtualnej musi być zainstalowany na maszynach wirtualnych tooenable zbierania danych. Witaj agenta maszyny Wirtualnej jest instalowany domyślnie dla maszyn wirtualnych, które zostały wdrożone z hello Azure Marketplace. Uzyskać informacji o sposobie tooinstall hello agenta maszyny Wirtualnej na innych maszynach wirtualnych, zobacz hello blogu [agenta maszyny Wirtualnej i rozszerzenia](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/).
