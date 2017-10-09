---
title: "we wdrożeniach typu PaaS aaaSecuring | Dokumentacja firmy Microsoft"
description: " Zrozumieć zalety zabezpieczeń hello PaaS i innych modeli usługi w chmurze i Dowiedz się zalecane wskazówki dotyczące zabezpieczania wdrożenia Azure PaaS. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: techlake
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: terrylan
ms.openlocfilehash: b94fe03b6f3a43d82e1e6e834f10a423e4c1db95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-deployments"></a>Zabezpieczanie wdrożenia PaaS

Ten artykuł zawiera informacje ułatwiające:

- Zrozumienie hello zabezpieczeń zalety obsługi aplikacji w chmurze hello
- Oceny hello zalety zabezpieczeń platformy jako usługa (PaaS) w porównaniu z innymi modelami usługi chmury
- Zmień fokus zabezpieczeń z podejście tooan skoncentrowane sieci obwodowej skoncentrowane na tożsamość zabezpieczeń
- Implementowanie ogólne PaaS zabezpieczeń poniżej rekomendowane najlepsze rozwiązania

## <a name="cloud-security-advantages"></a>Zalety zabezpieczeń w chmurze
W chmurze hello są toobeing zalety zabezpieczeń. W środowisku lokalnym, organizacje mogą mieć ograniczone zasoby dostępne tooinvest zabezpieczeń, który tworzy środowisko, w których osoby atakujące luk w zabezpieczeniach tooexploit stanie na wszystkich warstwach i unmet odpowiedzialności.

![Zalety zabezpieczeń ery chmury][1]

Organizacje są tooimprove stanie ich wykrywanie zagrożeń i czasy odpowiedzi przy użyciu funkcji zabezpieczeń oparte na chmurze i analizy chmury dostawcy.  Ustalając dostawcy chmury toohello obowiązki organizacji można uzyskać więcej pokrycia zabezpieczeń, która umożliwi im tooreallocate zabezpieczeń zasobów oraz priorytetów firmy tooother budżetu.

## <a name="division-of-responsibility"></a>Podział odpowiedzialności
Jest ważne toounderstand hello podział obowiązków między Tobą a firmą Microsoft. W infrastrukturze lokalnej, właścicielem hello cały stos, ale podczas przenoszenia chmury toohello pewne obowiązki transfer tooMicrosoft. Witaj następujące macierzy odpowiedzialność pokazuje obszarów hello hello stosu we wdrożeniu SaaS, PaaS i IaaS, który jest odpowiedzialny za i firmy Microsoft jest odpowiedzialny za.

![Odpowiedzialność stref][2]

Dla wszystkich typów wdrożeń chmury posiadanych danych i tożsamości. Jesteś wyłączną odpowiedzialność za ochronę hello bezpieczeństwa danych i tożsamości, zasobów lokalnych i hello składniki chmury, które kontrolujesz (która jest zależna od typu usługi).

Obowiązki, które są zawsze zachowywane przez administratora, niezależnie od tego typu wdrożenia, hello są:

- Dane
- Punkty końcowe
- Konto
- Zarządzanie dostępem

## <a name="security-advantages-of-a-paas-cloud-service-model"></a>Zalety zabezpieczeń PaaS modelu usługi w chmurze
Przy użyciu hello tej samej macierzy odpowiedzialność, umożliwia przyjrzeć się hello zabezpieczeń zalet wdrożenie Azure PaaS lub lokalnie.

![Zalety zabezpieczeń PaaS][3]

Zaczynając od dołu hello hello stosu, hello infrastruktury fizycznej, typowe zagrożenia i jego obowiązki firmy Microsoft zmniejsza. Ponieważ hello firmy Microsoft w chmurze jest stale monitorowane przez firmę Microsoft, jest tooattack twardym. Go nie ma sensu dla osoby atakującej toopursue hello firmy Microsoft w chmurze jako miejsce docelowe. O ile ma dużą oszczędność pieniędzy i zasobów, osoba atakująca hello hello jest prawdopodobnie toomove w celu tooanother.  

W środka hello hello stosu nie ma różnic między wdrożenie PaaS i lokalnej. Na warstwie aplikacji hello i warstwa zarządzania hello konta i dostępu masz podobne czynników ryzyka. W hello następnej sekcji kroki tego artykułu firma Microsoft przeprowadzi Cię toobest wskazówki dotyczące wyeliminowanie lub zmniejszenia ryzyka.

U góry hello hello stosu, zarządzanie danymi i usługi rights management możesz wykonać na jednym ryzyko, że można zminimalizować przez zarządzanie kluczami. (Zarządzanie kluczami jest objęte najlepszych rozwiązań.) Podczas zarządzania kluczami jest dodatkowe odpowiedzialność, masz obszarów w ramach wdrożenia PaaS już nie toomanage, można przesunąć zarządzania tookey zasobów.

Witaj platformy Azure również udostępnia silną ochronę przed atakami DDoS przy użyciu różnych technologii sieciowych. Wszystkie typy opartych na sieci metody ochrony przed atakami DDoS jednak limity ich na podstawie na jedno łącze i na centrum danych. toohelp uniknąć wpływu hello ataków DDoS, możesz można korzystać z możliwości chmury podstawowej platformy Azure umożliwienia tooquickly i automatycznie skalować toodefend przed atakami DDoS. Znajdują się bardziej szczegółowo na jak to zrobić w hello zalecane praktyki artykułów.

## <a name="modernizing-hello-defenders-mindset"></a>Mindset unowocześnienia defender hello
Z PaaS wdrożenia są shift w Twojej ogólną toosecurity podejście. Przesunięcie musi toocontrol wszystko siebie odpowiedzialność toosharing z firmą Microsoft.

Inny istotną różnicą między PaaS i wdrożeń tradycyjnych, lokalnie jest nowy widok co definiuje hello obwodowej głównej zabezpieczeń. W przeszłości granicznej zabezpieczeń lokalnych głównej hello został sieci i najbardziej lokalnymi zabezpieczeń wzorów użycia hello sieci, co jego pivot głównej zabezpieczeń. W przypadku wdrożeń typu PaaS są lepiej obsłużone przez uwzględnieniu obwodowej głównej zabezpieczeń hello toobe tożsamości.

## <a name="identity-as-hello-primary-security-perimeter"></a>Tożsamość jako hello obwodowej głównej zabezpieczeń
Mniej istotne myśląc co pięć istotnych cech hello chmury obliczeniowej jest szerokiego dostępu do sieci, dzięki czemu skoncentrowane sieci. cel Hello wielu chmury obliczeniowej jest użytkowników tooallow tooaccess zasobów, niezależnie od lokalizacji. Dla większości użytkowników ich lokalizacji będzie toobe gdzieś na powitania Internet.

Witaj poniższej ilustracji przedstawiono sposób granicznej zabezpieczeń hello powstał z sieci obwodowej tooan tożsamości obwodu. Zabezpieczenia staje się mniej o jednocześnie obrona dostępu do sieci i więcej informacji o jednocześnie obrona dostępu do danych, a także zarządzanie zabezpieczeniami hello aplikacji i użytkowników. Najważniejsza różnica Hello jest, które mają toopush zabezpieczeń bliżej toowhat na ważne tooyour firmy.

![Tożsamość jako nowe granicznej zabezpieczeń][4]

Początkowo usług Azure PaaS (na przykład ról sieć web i Azure SQL) podać niewielkiego lub żadnego z tradycyjną siecią obwodową zabezpieczenia. Został rozumie, że hello element celem było widoczne toobe toohello Internet (role sieci web) i uwierzytelniania oferuje granicznej nowe hello (na przykład obiekt BLOB lub Azure SQL).

Nowoczesne rozwiązania przyjęto założenie, że atakujący dokonuje tego hello naruszony hello sieci obwodowej. W związku z tym obrony nowoczesnych rozwiązań zostało przeniesione tooidentity. Organizacje należy ustanowić granicznej zabezpieczeń opartych na tożsamości z silnego uwierzytelniania i autoryzacji higieny (najlepsze rozwiązania).

## <a name="recommendations-for-managing-hello-identity-perimeter"></a>Zalecenia dotyczące zarządzania hello obwodowej tożsamości

Zasady i wzorce dla hello sieci obwodowej były dostępne dla dekad. Natomiast w branży hello ma stosunkowo mniej środowisko z przy użyciu tożsamości jako hello obwodowej głównej zabezpieczeń. Z tym powiedział możemy współdzielenia za mało tooprovide środowisko ogólne zalecenia dotyczące, które zostały sprawdzone w polu hello i stosować tooalmost wszystkie usługi PaaS.

następujące Hello zawiera podsumowanie toomanaging podejście ogólne najlepsze rozwiązania w zakresie sieci obwodowej tożsamości.

- **Nie utrać Twoje klucze lub poświadczenia** zabezpieczania kluczy i poświadczeń jest istotne toosecure we wdrożeniach typu PaaS. Utraty kluczy i poświadczeń jest to powszechny problem. Jeden dobrym rozwiązaniem jest toouse scentralizowanego rozwiązania, w których kluczy i kluczy tajnych są przechowywane w sprzętowych modułach zabezpieczeń (HSM). Platforma Azure udostępnia modułu HSM w chmurze hello z [usługi Azure Key Vault](../key-vault/key-vault-whatis.md).
- **Nie umieszczaj poświadczeń i innych informacji poufnych do kodu źródłowego lub GitHub** hello co element gorsza niż utraty Twoje klucze i poświadczeń o nieautoryzowana osoba uzyskują dostęp toothem tylko. Osoby atakujące są tootake mogli korzystać z bot technologii toofind kluczy i kluczy tajnych przechowywane w repozytoriach kodów, takich jak GitHub. Nie należy umieszczać kluczy i kluczy tajnych w tych publicznych repozytoriach kodów źródłowych.
- **Ochrona interfejsów zarządzania maszyny Wirtualnej na hybrydowego usługi PaaS i IaaS** IaaS i PaaS usługi są uruchomione na maszynach wirtualnych (VM). W zależności od typu hello usługi, są dostępne kilka interfejsów zarządzania pozwalające tooremote bezpośrednie zarządzanie tych maszyn wirtualnych. Zdalne zarządzanie protokołów, takich jak [protokołu Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell), [protokołu RDP (Remote Desktop)](https://support.microsoft.com/kb/186607), i [zdalnego programu PowerShell](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enable-psremoting) mogą być używane. Ogólnie rzecz biorąc zaleca się, nie należy włączać tooVMs bezpośredniego dostępu zdalnego z hello Internet. Jeśli to możliwe, należy użyć alternatywnych metod takich jak przy użyciu wirtualnej sieci prywatnej w sieci wirtualnej platformy Azure. Jeśli alternatywnych metod nie są dostępne, a następnie upewnij się, że używasz złożone hasła, a jeśli jest dostępna, uwierzytelnianie dwuskładnikowe (takich jak [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)).
- **Użyj silnego uwierzytelniania i autoryzacji platformy**

  - Użyj tożsamości federacyjnych w usłudze Azure AD zamiast magazynów użytkownika niestandardowego. Korzystając z tożsamości federacyjnej, możesz korzystać z platformy opartego i delegować hello Zarządzanie tożsamościami autoryzowanych partnerów tooyour. Podejście tożsamości federacyjnych jest szczególnie ważne w przypadkach, gdy kończą pracowników i że informacji wymaga toobe uwzględniane w wielu tożsamości i autoryzacji systemów.
  - Użyj platformy dostarczona mechanizmy uwierzytelniania i autoryzacji, zamiast kodu niestandardowego. Hello przyczyną jest to, że opracowywanie uwierzytelniania niestandardowego kodu może być błąd podatnych na błędy. Większość deweloperów nie są ekspertów zabezpieczeń i prawdopodobne toobe o precyzyjnie hello i hello najnowszych rozwiązań w uwierzytelniania i autoryzacji. Komercyjnych kodu (na przykład od firmy Microsoft) jest często często przeglądu zabezpieczeń.
  - Uwierzytelnianie wieloskładnikowe. Uwierzytelnianie wieloskładnikowe jest hello bieżącego standardowa do uwierzytelniania i autoryzacji, ponieważ pozwala ona na uniknięcie hello słabych zabezpieczeń jest związane z nazwy użytkownika i hasła typy uwierzytelniania. Należy tak zaprojektować i skonfigurowania toouse interfejsów zarządzania platformy Azure (portal/zdalne programu PowerShell) hello tooboth dostępu i toocustomer ukierunkowane usług [Azure Multi-Factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md).
  - Użyj standardowych protokołów uwierzytelniania, takich jak OAuth2 i protokołu Kerberos. Te protokoły zostały często dokładnie przeglądane i prawdopodobnie są zaimplementowane jako część bibliotek platformy do uwierzytelniania i autoryzacji.

## <a name="next-steps"></a>Następne kroki
W tym artykule firma Microsoft skupia się na zalet zabezpieczeń wdrożenie Azure PaaS. Następnie Dowiedz się, najważniejsze wskazówki dotyczące zabezpieczania PaaS w sieci web i rozwiązań mobilnych. Zaczniemy usłudze Azure App Service, baza danych SQL Azure i usługi Azure SQL Data Warehouse. Jako artykułów na zaleceń dla innych usług platformy Azure są dostępne, łącza zostanie podany w hello następującej listy:

- [Azure App Service](security-paas-applications-using-app-services.md)
- [Baza danych Azure SQL i magazyn danych Azure SQL](security-paas-applications-using-sql.md)
- Azure Storage
- Pamięć podręczna Azure REDIS
- Azure Service Bus
- Zapory aplikacji sieci Web

<!--Image references-->
[1]: ./media/security-paas-deployments/advantages-of-cloud.png
[2]: ./media/security-paas-deployments/responsibility-zones.png
[3]: ./media/security-paas-deployments/advantages-of-paas.png
[4]: ./media/security-paas-deployments/identity-perimeter.png
