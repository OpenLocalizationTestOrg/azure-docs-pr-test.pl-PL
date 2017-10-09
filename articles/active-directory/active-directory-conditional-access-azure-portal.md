---
title: "aaaAzure dostępu warunkowego w usłudze Active Directory | Dokumentacja firmy Microsoft"
description: "Użyj kontroli dostępu warunkowego w usłudze Azure Active Directory toocheck dotyczące określonych warunków podczas uwierzytelniania dla tooapplications dostępu."
services: active-directory
keywords: "tooapps dostępu warunkowego, dostępu warunkowego z usługą Azure AD, bezpieczny dostęp do zasobów toocompany, zasady dostępu warunkowego"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 9fa8a5c3e514c032fbe3aa56f33d759485a018c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-azure-active-directory"></a>Dostęp warunkowy w usłudze Azure Active Directory

W świecie pierwszy mobile, najpierw chmury Azure Active Directory umożliwia toodevices rejestracji jednokrotnej, aplikacji i usług z dowolnego miejsca. Witaj mnożenie urządzeń (takich jak BYOD), pracować poza siedzibą i 3 stron aplikacji SaaS, specjalistów IT muszą stawiać czoła dwóch celów przeciwna:

- Zwiększenie możliwości dostępnych dla toobe użytkownicy końcowi hello produktywności wszędzie tam, gdzie i po każdej zmianie
- Ochrona zasobów firmowych hello w dowolnym momencie

tooimprove wydajności, Azure Active Directory zapewnia użytkownikom szeroki zakres opcji tooaccess zasobów firmowych. Z zarządzania dostępem do aplikacji, usługi Azure Active Directory umożliwia jedynie tooensure *hello odpowiednich osób* mogą uzyskiwać dostęp do aplikacji. Co zrobić, jeśli chcesz toohave większą kontrolę nad jak hello odpowiednich osób uzyskują dostęp do zasobów w niektórych warunkach? Co zrobić, jeśli jeszcze masz warunków, w których aplikacje toocertain dostępu tooblock nawet w przypadku hello *prawym przyciskiem myszy osób*? Na przykład może być OK dla Ciebie Jeżeli hello odpowiednich osób uzyskuje dostęp do niektórych aplikacji z sieci zaufanej. jednak nie można ich tooaccess tych aplikacji z sieci, której nie ufasz. Można rozwiązać te pytania, przy użyciu dostępu warunkowego.

Dostęp warunkowy jest możliwość usługi Azure Active Directory, umożliwiającą tooenforce formantów na powitania tooapps dostępu w danym środowisku, na podstawie określonych warunków. Z formantami albo może powiązać dodatkowe wymagania toohello dostęp lub go zablokować. Implementacja Hello dostępu warunkowego jest oparta na zasadach. Podejście oparte na zasadach upraszcza środowiska konfiguracji, ponieważ wynika sposób hello myślisz na temat wymagań dostępu.  

Zazwyczaj określa wymagań dostępu za pomocą instrukcji, które są oparte na powitania następującego wzorca:

![Formant](./media/active-directory-conditional-access-azure-portal/10.png)

Gdy Zastąp hello dwa wystąpienia "*to*" informacje rzeczywistych ma przykład deklaracji zasad, prawdopodobnie wyglądająca znanych tooyou:

*Gdy wykonawców próbujesz tooaccess nasze aplikacje w chmurze z sieci, które nie są zaufane, następnie zablokować dostęp.*

Deklaracja zasad Hello powyżej prezentuje zasilania hello dostępu warunkowego. Podczas gdy można włączyć toobasically wykonawców dostęp do aplikacji w chmurze (**kto**), przy użyciu dostępu warunkowego, można również zdefiniować warunki, w których hello dostęp jest możliwy (**jak**).

W kontekście hello dostępu warunkowego dla usługi Azure Active Directory,

- "**w takim przypadku**" jest wywoływana **warunku — instrukcja**
- "**To zrobić**" jest wywoływana **formantów**

![Formant](./media/active-directory-conditional-access-azure-portal/11.png)

Kombinacja Hello instrukcji warunku z formantów reprezentuje zasady dostępu warunkowego.

![Formant](./media/active-directory-conditional-access-azure-portal/12.png)


## <a name="controls"></a>Kontrolki

W zasadach dostępu warunkowego kontroli zdefiniować, co jest to, że powinno się zdarzyć, gdy instrukcja warunku zostały spełnione.  
Funkcje kontroli możesz zablokować dostęp lub zezwolić na dostęp z dodatkowymi wymaganiami.
Po skonfigurowaniu zasad, która zezwala na dostęp, należy tooselect co najmniej jedno wymaganie.   

### <a name="grant-controls"></a>Udziel formantów
Bieżąca implementacja Hello Azure Active Directory umożliwia hello tooconfigure następujące wymagania dotyczące sterowania grant:

![Formant](./media/active-directory-conditional-access-azure-portal/05.png)

- **Uwierzytelnianie wieloskładnikowe** — można wymaga silnego uwierzytelniania za pośrednictwem usługi Multi-Factor authentication. Jako dostawcy możesz użyć wieloskładnikowe Azure lub lokalnego dostawcy uwierzytelniania wieloskładnikowego, w połączeniu z usługi Active Directory Federation Services (AD FS). Przy użyciu usługi Multi-Factor authentication pomaga chronić zasoby z uzyskiwany przez nieautoryzowanego użytkownika, który może mieć uzyskał dostęp toohello poświadczenia prawidłowego użytkownika.

- **Urządzenie zgodne z** — na poziomie urządzeń hello można ustawić zasady dostępu warunkowego. Można skonfigurować komputery Włącz tooonly zasad, które są zgodne lub urządzeń przenośnych, które są zarejestrowane w tooaccess zarządzania urządzeniami przenośnymi zasobów organizacji. Na przykład można użyć zgodności urządzeń toocheck usługi Intune i raportować ją tooAzure AD do wymuszania hello użytkownik próbujący tooaccess aplikacji. Szczegółowe wskazówki dotyczące sposobu toouse Intune tooprotect aplikacji i danych, zobacz [ochrona aplikacji i danych w usłudze Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune). Można też użyć do ochrony danych tooenforce usługi Intune w przypadku utraty lub kradzieży urządzeń. Aby uzyskać więcej informacji, zobacz [pomocy lepszej ochrony danych dzięki pełnemu lub selektywnemu czyszczeniu przy użyciu programu Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

- **Urządzenia przyłączone do domeny** — może wymagać hello urządzenia użyto tooyour tooconnect tooAzure usługi Active Directory toobe przyłączonych do domeny lokalnej usługi Active Directory (AD). Ta zasada dotyczy tooWindows komputerów stacjonarnych, laptopów i tabletów przedsiębiorstwa. 

Jeśli masz wiele formantów zaznaczone, można również skonfigurować, czy wszystkie z nich są wymagane podczas przetwarzania zasad.

![Formant](./media/active-directory-conditional-access-azure-portal/06.png)

### <a name="session-controls"></a>Formanty sesji
Formanty sesji Włącz ograniczanie doświadczenie w aplikacji w chmurze. Formanty sesji Hello są wymuszane przez aplikacje w chmurze i polegać na dodatkowe informacje o aplikacji usługi Azure AD toohello o hello sesji.

![Formant](./media/active-directory-conditional-access-azure-portal/session-control-pic.png)

#### <a name="use-app-enforced-restrictions"></a>Użyj aplikacji wymuszane ograniczeń
Możesz użyć tej kontrolki toorequire usługi Azure AD toopass hello urządzenia informacji toohello chmury aplikacji. Dzięki temu można sprawdzić, czy użytkownik hello pochodzi z zgodne urządzenie lub urządzenia przyłączone do domeny aplikacji w chmurze hello. Ten formant jest obecnie obsługiwana tylko z programem SharePoint jako hello aplikacji w chmurze. SharePoint używa hello urządzenia informacje tooprovide użytkownicy środowisko ograniczony lub pełną w zależności od stanu urządzenia hello.
toolearn więcej informacji na temat sposobu toorequire ograniczony dostęp z programem SharePoint, przejdź [tutaj](https://aka.ms/spolimitedaccessdocs).

## <a name="condition-statement"></a>Instrukcja warunku

Hello poprzedniej sekcji wprowadziła tooblock opcje toosupported lub ograniczyć dostęp do zasobów tooyour w postaci formantów. Zasady dostępu warunkowego służy do definiowania kryteria hello, które muszą spełnić toobe dla Twojego toobe formantów stosowany w postaci instrukcja warunku.  

Może zawierać powitania po przypisań do instrukcji warunku:

![Formant](./media/active-directory-conditional-access-azure-portal/07.png)


- **Kto** — w wielu przypadkach ma Twojej formantów stosowany toobe tooa określonych użytkowników. W instrukcji warunku można zdefiniować tego zestawu, wybierając hello użytkowników i grup, które dotyczą zasady. W razie potrzeby można również jawnie wykluczyć zbiór użytkowników z zasad, zwalniając je.  
Po wybraniu użytkowników i grup, należy zdefiniować zakres hello użytkowników, których dotyczą zasady.    

    ![Formant](./media/active-directory-conditional-access-azure-portal/08.png)



- **Co** — zwykle istnieją pewne aplikacje, które są uruchomione w środowisku wymagające z punktu widzenia ochrony uwagi więcej niż inne. Wpływa to na przykład aplikacje, które mają dostęp do danych toosensitive.
Po wybraniu aplikacji w chmurze, możesz określić zakres hello zasady stosowane do aplikacji w chmurze. W razie potrzeby można również jawnie wykluczyć zestawu aplikacji z zasad.

    ![Formant](./media/active-directory-conditional-access-azure-portal/09.png)


- **Jak** — tak długo, jak aplikacje tooyour dostęp odbywa się w warunkach można kontrolować, może nie musi nakładające dodatkowych funkcji kontroli w sposób aplikacji w chmurze są dostępne przez użytkowników. Jednak czynności mogą wyglądać inaczej, jeśli dostęp do aplikacji w chmurze tooyour jest wykonywana, na przykład z sieci, które nie są zaufane lub urządzeń, które nie są zgodne. W instrukcji warunku można zdefiniować niektórych warunki dostępu, które mają dodatkowe wymagania dotyczące realizację dostępu tooyour aplikacji.

    ![Warunki](./media/active-directory-conditional-access-azure-portal/21.png)


## <a name="conditions"></a>Warunki

W hello bieżąca implementacja usługi Azure Active Directory można określić warunki hello następujące obszary:

- Ryzyko logowania
- Platformy urządzeń
- Lokalizacje
- Aplikacje klienta

![Warunki](./media/active-directory-conditional-access-azure-portal/21.png)

### <a name="sign-in-risk"></a>Ryzyko logowania

Ryzyko logowania jest obiekt, który jest używany przez usługi Azure Active Directory tootrack hello prawdopodobieństwo próba logowania nie została wykonana przez właściciela uzasadnionych hello konta użytkownika. W tym obiekcie prawdopodobieństwo hello (wysoki, średni lub niski) są przechowywane w postaci atrybutu o nazwie [poziom ryzyka logowania](active-directory-reporting-risk-events.md#risk-level). Ten obiekt jest generowany podczas logowania użytkownika, jeśli logowanie ryzyka zostały wykryte przez usługę Azure Active Directory. Aby uzyskać więcej informacji, zobacz [Ryzykowne logowania](active-directory-identityprotection.md#risky-sign-ins).  
Poziom rejestrowania ryzyka hello obliczana służy jako warunek w zasadach dostępu warunkowego. 

![Warunki](./media/active-directory-conditional-access-azure-portal/22.png)

### <a name="device-platforms"></a>Platformy urządzeń

platformy urządzeń Hello charakteryzuje się hello systemu operacyjnego, który działa na twoim urządzeniu:

- Android
- iOS
- Windows Phone
- Windows
- System macOS (wersja zapoznawcza). 

![Warunki](./media/active-directory-conditional-access-azure-portal/02.png)

Można zdefiniować hello platformy urządzeń, które są dołączone oraz platformy urządzeń, które są wykluczone z zasad.  
toouse platformy urządzeń w zasadach hello, pierwszy hello zmiany Konfigurowanie przełączników zbyt**tak**, a następnie zaznacz wszystkie lub urządzenie poszczególnych platform hello zasady dotyczą. Wybranie platformy poszczególnych urządzeń, hello zasad ma wpływ tylko na tych platformach. W takim przypadku logowania tooother obsługiwanych platform nie dotyczy hello zasad.


### <a name="locations"></a>Lokalizacje

Witaj lokalizacji jest identyfikowane za pomocą adresu IP hello powitania klienta zostały użyte tooAzure tooconnect usługi Active Directory. Ten warunek wymaga, należy zapoznać się z toobe **o nazwie lokalizacje** i **MFA zaufanych adresów IP**.  

**O nazwie lokalizacje** to funkcja usługi Azure Active Directory, dzięki czemu zakresów adresów IP toolabel zaufane w Twojej organizacji. W danym środowisku, można użyć nazwane lokalizacje w kontekście hello wykrywanie hello [ryzyka zdarzenia](active-directory-reporting-risk-events.md) oraz dostępu warunkowego. Aby uzyskać więcej informacji o konfigurowaniu o nazwie lokalizacjach w usłudze Azure Active Directory, zobacz [o nazwie lokalizacjach w usłudze Azure Active Directory](active-directory-named-locations.md).

Hello liczba lokalizacji, które można skonfigurować jest ograniczane przez rozmiar hello hello powiązanego obiektu w usłudze Azure AD. Można skonfigurować:
 
 - Jedną lokalizację o nazwie o się too500 zakresów adresów IP
 - Maksymalnie 60 lokalizacji o nazwie (wersja zapoznawcza) jeden zakres adresów IP przypisanych tooeach z nich 


**Uwierzytelnianie wieloskładnikowe zaufanych adresów IP** to funkcja usługi Multi-Factor Authentication, umożliwiającą zakresów adresów IP toodefine zaufane reprezentujący lokalny intranet firmy. Po skonfigurowaniu warunków lokalizacji zaufanych adresów IP umożliwia toodistinguish między połączenia z siecią organizacji i innych lokalizacjach. Aby uzyskać więcej informacji, zobacz [zaufanych adresów IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).  



Można dołączyć wszystkie lokalizacje lub wszystkich zaufanych adresów IP i można wykluczyć wszystkie zaufane adresów IP.

![Warunki](./media/active-directory-conditional-access-azure-portal/03.png)


### <a name="client-app"></a>Aplikacja kliencka

powitania klienta aplikacji może być to aplikacja ogólnego poziomu hello (przeglądarki sieci web, aplikacji mobilnej, klient usług pulpitu) zostały użyte tooAzure tooconnect usługi Active Directory lub musisz wybrać programu Exchange Active Sync.  
Starsze uwierzytelnianie odwołuje się tooclients przy użyciu uwierzytelniania podstawowego, takich jak starszych klientów pakietu Office, które nie używają nowoczesnego uwierzytelniania. Dostęp warunkowy nie jest obecnie obsługiwane przy użyciu starszej wersji uwierzytelniania.

![Warunki](./media/active-directory-conditional-access-azure-portal/04.png)


## <a name="common-scenarios"></a>Typowe scenariusze

### <a name="requiring-multi-factor-authentication-for-apps"></a>Wymagania uwierzytelniania wieloskładnikowego dla aplikacji

Wiele środowisk ma aplikacje wymagające wyższego poziomu ochrony niż hello innych użytkowników.
Jest to, na przykład w przypadku aplikacji, które mają dostęp do danych toosensitive hello.
Jeśli chcesz tooadd kolejną warstwę ochrony toothese aplikacji, można skonfigurować zasady dostępu warunkowego, która wymaga usługi Multi-Factor authentication, gdy użytkownicy uzyskują dostęp do tych aplikacji.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>Wymagania uwierzytelniania wieloskładnikowego dla dostępu z sieci, które nie są zaufane

Ten scenariusz jest podobne toohello poprzednim scenariuszu, ponieważ powoduje ona dodanie wymaganie uwierzytelniania wieloskładnikowego.
Główna różnica hello jest jednak warunek hello tego wymagania.  
Podczas hello fokus poprzednim scenariuszu hello na aplikacje z danymi toosensitve dostępu hello w tym scenariuszu koncentruje się na zaufanych lokalizacji.  
Innymi słowy może być wymagane uwierzytelnianie wieloskładnikowe, jeśli aplikacja jest dostępna przez użytkownika z sieci, której nie ufasz.


### <a name="only-trusted-devices-can-access-office-365-services"></a>Tylko zaufane urządzenia mają dostęp do usług Office 365

Jeśli używasz usługi Intune w danym środowisku, mogą natychmiast rozpocząć korzystanie hello interfejs zasad dostępu warunkowego w hello konsoli platformy Azure.

Wielu klientów usługi Intune korzystają z dostępu warunkowego tooensure, że tylko zaufane urządzenia mają dostęp do usług Office 365. Oznacza to, że urządzenia przenośne zarejestrowane w usłudze Intune i spełnić wymagania zasad zgodności oraz czy komputery z systemem Windows są tooan przyłączone do domeny lokalnej. Poprawy klucza jest, że nie masz tooset hello te same zasady dla każdej z usług hello usługi Office 365.  Podczas tworzenia nowych zasad konfigurowania hello chmury aplikacji tooinclude każdej aplikacji hello usługi Office 365, które mają tooprotect z przy użyciu dostępu warunkowego.

## <a name="next-steps"></a>Następne kroki

Jeśli chcesz, aby tooknow tooconfigure zasady dostępu warunkowego, zobacz temat [wprowadzenie dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).

Jeśli zasady dostępu warunkowego tooconfigure gotowy dla danego środowiska, zobacz hello [najlepszych rozwiązań dotyczących dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-best-practices.md). 
