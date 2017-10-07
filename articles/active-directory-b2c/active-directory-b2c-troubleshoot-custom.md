---
title: "Application Insights tootroubleshoot zasady niestandardowe — usługi Azure AD B2C | Dokumentacja firmy Microsoft"
description: "jak tootrace usługi Application Insights toosetup hello wykonywania zasad niestandardowych"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: saeda
ms.openlocfilehash: c02d7178512c7f9e022385371c3effd4f8cb7726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a>Azure Active Directory B2C: Zbierania dzienników

Ten artykuł zawiera kroki do zbierania dzienników z usługi Azure AD B2C, dzięki czemu można diagnozować problemy z zasadami dotyczącymi zasobów niestandardowych.

>[!NOTE]
>Obecnie hello dzienniki szczegółowe działania opisane w tym miejscu są zaprojektowane **tylko** tooaid w tworzenie zasad niestandardowych. Nie należy używać trybu tworzenia w środowisku produkcyjnym.  Dzienniki zbierać wszystkie oświadczenia wysyłane tooand od dostawców tożsamości hello podczas programowania.  Jeśli używane w środowisku produkcyjnym, deweloperów hello przyjmuje na siebie odpowiedzialność dla wrażliwych danych osobowych (prywatnie informacje umożliwiające identyfikację) zebrane w dzienniku Insights aplikacji hello, w której jest właścicielem.  Te szczegółowe dzienniki są zbierane tylko, gdy zasady hello jest umieszczona na **tryb programowania**.


## <a name="use-application-insights"></a>Użyj usługi Application Insights

Usługa Azure AD B2C obsługuje funkcję wysyłania danych tooApplication szczegółowych informacji.  Usługi Application Insights udostępnia toodiagnose sposób wyjątków i wizualizację problemy z wydajnością aplikacji.

### <a name="setup-application-insights"></a>Konfiguracja usługi Application Insights

1. Przejdź toohello [portalu Azure](https://portal.azure.com). Upewnij się, że jesteś w dzierżawie powitalnych z subskrypcją platformy Azure (nie dzierżawy usługi Azure AD B2C).
1. Kliknij przycisk **+ nowy** w menu nawigacji po lewej stronie powitania.
1. Wyszukaj i wybierz **usługi Application Insights**, następnie kliknij przycisk **Utwórz**.
1. Wypełnij formularz hello i kliknij przycisk **Utwórz**. Wybierz **ogólne** dla hello **typu aplikacji**.
1. Po utworzeniu zasobu hello Otwórz hello zasobu usługi Application Insights.
1. Znajdź **właściwości** w hello menu po lewej i kliknij go.
1. Kopiuj hello **klucza Instrumentacji** i zapisać go do następnej sekcji hello.

### <a name="set-up-hello-custom-policy"></a>Ustawienia zasad niestandardowych hello

1. Otwórz plik RP hello (na przykład SignUpOrSignin.xml).
1. Dodaj następujące atrybuty toohello hello `<TrustFrameworkPolicy>` elementu:

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. Jeśli nie istnieje już, Dodaj węzeł podrzędny `<UserJourneyBehaviors>` toohello `<RelyingParty>` węzła. Należy zlokalizować natychmiast po hello`<DefaultUserJourney ReferenceId="YourPolicyName" />`
2. Dodaj następujące węźle jako element podrzędny hello hello `<UserJourneyBehaviors>` elementu. Upewnij się, że tooreplace `{Your Application Insights Key}` z hello **klucza Instrumentacji** uzyskane z usługi Application Insights w poprzedniej sekcji hello.

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * `DeveloperMode="true"`Określa, że ApplicationInsights tooexpedite hello telemetrii za pośrednictwem potoku przetwarzania hello, dobry do tworzenia aplikacji, ale ograniczonego w dużej ilości.
  * `ClientEnabled="true"`wysyła skryptu po stronie klienta ApplicationInsights hello śledzenia błędy po stronie klienta i widoku strony (nie wymagane).
  * `ServerEnabled="true"`wysyła hello istniejących JSON UserJourneyRecorder jako zdarzenie niestandardowe tooApplication szczegółowych informacji.
Przykład:

  ```XML
  <TrustFrameworkPolicy
    ...
    TenantId="fabrikamb2c.onmicrosoft.com"
    PolicyId="SignUpOrSignInWithAAD"
    DeploymentMode="Development"
    UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  >
    ...
    <RelyingParty>
      <DefaultUserJourney ReferenceId="YourPolicyName" />
      <UserJourneyBehaviors>
        <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      </UserJourneyBehaviors>
      ...
  </TrustFrameworkPolicy>
  ```

3. Przekaż hello zasad.

### <a name="see-hello-logs-in-application-insights"></a>Zobacz dzienniki hello w usłudze Application Insights

>[!NOTE]
> Brak krótki opóźnienie (mniej niż pięć minut), aby zobaczyć nowe dzienniki w usłudze Application Insights.

1. Otwórz hello zasobu usługi Application Insights, który został utworzony w hello [portalu Azure](https://portal.azure.com).
1. W hello **omówienie** menu, kliknij polecenie **Analytics**.
1. Otwórz nową kartę w usłudze Application Insights.
1. Poniżej przedstawiono listę zapytań, których można użyć toosee hello dzienników

| Zapytanie | Opis |
|---------------------|--------------------|
Dane śledzenia | Wyświetl wszystkie dzienniki hello generowane przez usługę Azure AD B2C |
ślady \| gdzie sygnatury czasowej > ago(1d) | Zobacz wszystkie dzienniki hello generowane przez usługę Azure AD B2C dla hello ostatni dzień

wpisy Hello może trwać długo.  Wyeksportuj tooCSV dla bliższe spojrzenie.

Dowiedz się więcej o narzędzie analityczne hello [tutaj](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).

>[!NOTE]
>Społeczność Hello opracowała deweloperzy tożsamości użytkownika toohelp podglądu podróży.  Nie jest obsługiwane przez firmę Microsoft i staje się dostępna wyłącznie jako — jest.  Odczytuje z wystąpieniem usługi Application Insights i udostępnia widok struktury także hello użytkownika przebieg zdarzeń.  Uzyskaj hello kodu źródłowego i wdrożyć ją w własne rozwiązania.

>[!NOTE]
>Obecnie hello dzienniki szczegółowe działania opisane w tym miejscu są zaprojektowane **tylko** tooaid w tworzenie zasad niestandardowych. Nie należy używać trybu tworzenia w środowisku produkcyjnym.  Dzienniki zbierać wszystkie oświadczenia wysyłane tooand od dostawców tożsamości hello podczas programowania.  Jeśli używane w środowisku produkcyjnym, deweloperów hello przyjmuje na siebie odpowiedzialność dla wrażliwych danych osobowych (prywatnie informacje umożliwiające identyfikację) zebrane w dzienniku Insights aplikacji hello, w której jest właścicielem.  Te szczegółowe dzienniki są zbierane tylko, gdy zasady hello jest umieszczona na **tryb programowania**.

[Repozytorium Github dla nieobsługiwany Przykłady zasad niestandardowych oraz narzędzia pokrewne](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a>Następne kroki

Eksplorowanie danych hello toohelp usługi Application Insights rozumiesz sposób hello Framework obsługi tożsamości podstawowej B2C działa toodeliver napotyka własną tożsamości.
