---
title: "Application Insights, aby rozwiązać zasady niestandardowe — usługi Azure AD B2C | Dokumentacja firmy Microsoft"
description: "sposób instalacji usługi Application Insights do śledzenia realizacji zasad niestandardowych"
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
ms.openlocfilehash: 8c79df33cd5f04f490e2cc6372f7e8ac1c4d9bbe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a>Azure Active Directory B2C: Zbierania dzienników

Ten artykuł zawiera kroki do zbierania dzienników z usługi Azure AD B2C, dzięki czemu można diagnozować problemy z zasadami dotyczącymi zasobów niestandardowych.

>[!NOTE]
>Obecnie dzienniki szczegółowe działania opisane w tym miejscu są zaprojektowane **tylko** ułatwiających tworzenie niestandardowych zasad. Nie należy używać trybu tworzenia w środowisku produkcyjnym.  Dzienniki zbierać wszystkie oświadczenia wysyłane do i z dostawców tożsamości w czasie projektowania.  Jeśli używane w środowisku produkcyjnym, deweloper przyjmuje na siebie odpowiedzialność dla wrażliwych danych osobowych (prywatnie informacje umożliwiające identyfikację) zebrane w dzienniku Insights aplikacji, w której jest właścicielem.  Te szczegółowe dzienniki są zbierane tylko, gdy zasady jest umieszczona na **tryb programowania**.


## <a name="use-application-insights"></a>Użyj usługi Application Insights

Usługa Azure AD B2C obsługuje funkcję wysyłania danych do usługi Application Insights.  Usługa Application Insights umożliwia diagnozowanie wyjątków i wizualizację problemy z wydajnością aplikacji.

### <a name="setup-application-insights"></a>Konfiguracja usługi Application Insights

1. Przejdź do witryny [Azure Portal](https://portal.azure.com). Upewnij się, że jesteś w dzierżawcy z subskrypcją platformy Azure (nie dzierżawy usługi Azure AD B2C).
1. Kliknij przycisk **+ nowy** w menu nawigacji po lewej stronie.
1. Wyszukaj i wybierz **usługi Application Insights**, następnie kliknij przycisk **Utwórz**.
1. Wypełnij formularz, a następnie kliknij przycisk **Utwórz**. Wybierz **ogólne** dla **typu aplikacji**.
1. Po utworzeniu zasobu, należy otworzyć zasobu usługi Application Insights.
1. Znajdź **właściwości** w menu po lewej i kliknij go.
1. Kopiuj **klucza Instrumentacji** i zapisz go w następnej sekcji.

### <a name="set-up-the-custom-policy"></a>Ustawienia zasad niestandardowych

1. Otwórz plik RP (na przykład SignUpOrSignin.xml).
1. Dodaj następujące atrybuty `<TrustFrameworkPolicy>` elementu:

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. Jeśli nie istnieje już, Dodaj węzeł podrzędny `<UserJourneyBehaviors>` do `<RelyingParty>` węzła. Znajdować się natychmiast po`<DefaultUserJourney ReferenceId="YourPolicyName" />`
2. Dodaj następujący węzeł jako element podrzędny `<UserJourneyBehaviors>` elementu. Upewnij się zastąpić `{Your Application Insights Key}` z **klucza Instrumentacji** uzyskane z usługi Application Insights w poprzedniej sekcji.

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * `DeveloperMode="true"`Określa, że ApplicationInsights w celu przyspieszenia telemetrii za pośrednictwem potoku przetwarzania dobry do tworzenia aplikacji, ale ograniczonego w dużej ilości.
  * `ClientEnabled="true"`wysyła ApplicationInsights skryptu po stronie klienta do śledzenia błędy po stronie klienta i widoku strony (nie wymagane).
  * `ServerEnabled="true"`wysyła istniejących JSON UserJourneyRecorder jako zdarzenie niestandardowe do usługi Application Insights.
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

3. Przekaż zasad.

### <a name="see-the-logs-in-application-insights"></a>Można znaleźć w dziennikach w usłudze Application Insights

>[!NOTE]
> Brak krótki opóźnienie (mniej niż pięć minut), aby zobaczyć nowe dzienniki w usłudze Application Insights.

1. Otwórz zasobu usługi Application Insights, który został utworzony w [portalu Azure](https://portal.azure.com).
1. W **omówienie** menu, kliknij polecenie **Analytics**.
1. Otwórz nową kartę w usłudze Application Insights.
1. Poniżej przedstawiono listę zapytania używanego do znajduje się w dziennikach

| Zapytanie | Opis |
|---------------------|--------------------|
Dane śledzenia | Wyświetl wszystkie dzienniki generowane przez usługę Azure AD B2C |
ślady \| gdzie sygnatury czasowej > ago(1d) | Wyświetl wszystkie dzienniki generowane przez usługę Azure AD B2C w ciągu ostatniego dnia

Wpisy może trwać długo.  Eksportuj do pliku CSV dla bliższe spojrzenie.

Dowiedz się więcej o narzędziu Analytics [tutaj](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).

>[!NOTE]
>Społeczność opracowała podglądu przebieg użytkownika, aby pomóc deweloperom w tożsamości.  Nie jest obsługiwane przez firmę Microsoft i staje się dostępna wyłącznie jako — jest.  Odczytuje z wystąpieniem usługi Application Insights i udostępnia widok struktury także użytkownika przebieg zdarzenia.  Uzyskanie kodu źródłowego i wdrożyć ją w własne rozwiązania.

>[!NOTE]
>Obecnie dzienniki szczegółowe działania opisane w tym miejscu są zaprojektowane **tylko** ułatwiających tworzenie niestandardowych zasad. Nie należy używać trybu tworzenia w środowisku produkcyjnym.  Dzienniki zbierać wszystkie oświadczenia wysyłane do i z dostawców tożsamości w czasie projektowania.  Jeśli używane w środowisku produkcyjnym, deweloper przyjmuje na siebie odpowiedzialność dla wrażliwych danych osobowych (prywatnie informacje umożliwiające identyfikację) zebrane w dzienniku Insights aplikacji, w której jest właścicielem.  Te szczegółowe dzienniki są zbierane tylko, gdy zasady jest umieszczona na **tryb programowania**.

[Repozytorium Github dla nieobsługiwany Przykłady zasad niestandardowych oraz narzędzia pokrewne](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a>Następne kroki

Eksplorowanie danych w usłudze Application Insights, aby ułatwić zrozumienie sposobu wykonywania Framework obsługi tożsamości podstawowej B2C działa, aby dostarczyć własny tożsamości.
