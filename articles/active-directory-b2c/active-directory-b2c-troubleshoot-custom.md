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
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="60e4c-103">Azure Active Directory B2C: Zbierania dzienników</span><span class="sxs-lookup"><span data-stu-id="60e4c-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="60e4c-104">Ten artykuł zawiera kroki do zbierania dzienników z usługi Azure AD B2C, dzięki czemu można diagnozować problemy z zasadami dotyczącymi zasobów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="60e4c-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="60e4c-105">Obecnie hello dzienniki szczegółowe działania opisane w tym miejscu są zaprojektowane **tylko** tooaid w tworzenie zasad niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="60e4c-105">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="60e4c-106">Nie należy używać trybu tworzenia w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="60e4c-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="60e4c-107">Dzienniki zbierać wszystkie oświadczenia wysyłane tooand od dostawców tożsamości hello podczas programowania.</span><span class="sxs-lookup"><span data-stu-id="60e4c-107">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="60e4c-108">Jeśli używane w środowisku produkcyjnym, deweloperów hello przyjmuje na siebie odpowiedzialność dla wrażliwych danych osobowych (prywatnie informacje umożliwiające identyfikację) zebrane w dzienniku Insights aplikacji hello, w której jest właścicielem.</span><span class="sxs-lookup"><span data-stu-id="60e4c-108">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="60e4c-109">Te szczegółowe dzienniki są zbierane tylko, gdy zasady hello jest umieszczona na **tryb programowania**.</span><span class="sxs-lookup"><span data-stu-id="60e4c-109">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="60e4c-110">Użyj usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="60e4c-110">Use Application Insights</span></span>

<span data-ttu-id="60e4c-111">Usługa Azure AD B2C obsługuje funkcję wysyłania danych tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="60e4c-111">Azure AD B2C supports a feature for sending data tooApplication Insights.</span></span>  <span data-ttu-id="60e4c-112">Usługi Application Insights udostępnia toodiagnose sposób wyjątków i wizualizację problemy z wydajnością aplikacji.</span><span class="sxs-lookup"><span data-stu-id="60e4c-112">Application Insights provides a way toodiagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="60e4c-113">Konfiguracja usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="60e4c-113">Setup Application Insights</span></span>

1. <span data-ttu-id="60e4c-114">Przejdź toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="60e4c-114">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="60e4c-115">Upewnij się, że jesteś w dzierżawie powitalnych z subskrypcją platformy Azure (nie dzierżawy usługi Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="60e4c-115">Ensure you are in hello tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="60e4c-116">Kliknij przycisk **+ nowy** w menu nawigacji po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="60e4c-116">Click **+ New** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="60e4c-117">Wyszukaj i wybierz **usługi Application Insights**, następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="60e4c-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="60e4c-118">Wypełnij formularz hello i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="60e4c-118">Complete hello form and click **Create**.</span></span> <span data-ttu-id="60e4c-119">Wybierz **ogólne** dla hello **typu aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="60e4c-119">Select **General** for hello **Application Type**.</span></span>
1. <span data-ttu-id="60e4c-120">Po utworzeniu zasobu hello Otwórz hello zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="60e4c-120">Once hello resource has been created, open hello Application Insights resource.</span></span>
1. <span data-ttu-id="60e4c-121">Znajdź **właściwości** w hello menu po lewej i kliknij go.</span><span class="sxs-lookup"><span data-stu-id="60e4c-121">Find **Properties** in hello left-menu, and click on it.</span></span>
1. <span data-ttu-id="60e4c-122">Kopiuj hello **klucza Instrumentacji** i zapisać go do następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="60e4c-122">Copy hello **Instrumentation Key** and save it for hello next section.</span></span>

### <a name="set-up-hello-custom-policy"></a><span data-ttu-id="60e4c-123">Ustawienia zasad niestandardowych hello</span><span class="sxs-lookup"><span data-stu-id="60e4c-123">Set up hello custom policy</span></span>

1. <span data-ttu-id="60e4c-124">Otwórz plik RP hello (na przykład SignUpOrSignin.xml).</span><span class="sxs-lookup"><span data-stu-id="60e4c-124">Open hello RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="60e4c-125">Dodaj następujące atrybuty toohello hello `<TrustFrameworkPolicy>` elementu:</span><span class="sxs-lookup"><span data-stu-id="60e4c-125">Add hello following attributes toohello `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="60e4c-126">Jeśli nie istnieje już, Dodaj węzeł podrzędny `<UserJourneyBehaviors>` toohello `<RelyingParty>` węzła.</span><span class="sxs-lookup"><span data-stu-id="60e4c-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` toohello `<RelyingParty>` node.</span></span> <span data-ttu-id="60e4c-127">Należy zlokalizować natychmiast po hello`<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="60e4c-127">It must be located immediately after hello `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="60e4c-128">Dodaj następujące węźle jako element podrzędny hello hello `<UserJourneyBehaviors>` elementu.</span><span class="sxs-lookup"><span data-stu-id="60e4c-128">Add hello following node as a child of hello `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="60e4c-129">Upewnij się, że tooreplace `{Your Application Insights Key}` z hello **klucza Instrumentacji** uzyskane z usługi Application Insights w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="60e4c-129">Make sure tooreplace `{Your Application Insights Key}` with hello **Instrumentation Key** that you obtained from Application Insights in hello previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="60e4c-130">`DeveloperMode="true"`Określa, że ApplicationInsights tooexpedite hello telemetrii za pośrednictwem potoku przetwarzania hello, dobry do tworzenia aplikacji, ale ograniczonego w dużej ilości.</span><span class="sxs-lookup"><span data-stu-id="60e4c-130">`DeveloperMode="true"` tells ApplicationInsights tooexpedite hello telemetry through hello processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="60e4c-131">`ClientEnabled="true"`wysyła skryptu po stronie klienta ApplicationInsights hello śledzenia błędy po stronie klienta i widoku strony (nie wymagane).</span><span class="sxs-lookup"><span data-stu-id="60e4c-131">`ClientEnabled="true"` sends hello ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="60e4c-132">`ServerEnabled="true"`wysyła hello istniejących JSON UserJourneyRecorder jako zdarzenie niestandardowe tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="60e4c-132">`ServerEnabled="true"` sends hello existing UserJourneyRecorder JSON as a custom event tooApplication Insights.</span></span>
<span data-ttu-id="60e4c-133">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60e4c-133">Sample:</span></span>

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

3. <span data-ttu-id="60e4c-134">Przekaż hello zasad.</span><span class="sxs-lookup"><span data-stu-id="60e4c-134">Upload hello policy.</span></span>

### <a name="see-hello-logs-in-application-insights"></a><span data-ttu-id="60e4c-135">Zobacz dzienniki hello w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="60e4c-135">See hello logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="60e4c-136">Brak krótki opóźnienie (mniej niż pięć minut), aby zobaczyć nowe dzienniki w usłudze Application Insights.</span><span class="sxs-lookup"><span data-stu-id="60e4c-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="60e4c-137">Otwórz hello zasobu usługi Application Insights, który został utworzony w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="60e4c-137">Open hello Application Insights resource that you created in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="60e4c-138">W hello **omówienie** menu, kliknij polecenie **Analytics**.</span><span class="sxs-lookup"><span data-stu-id="60e4c-138">In hello **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="60e4c-139">Otwórz nową kartę w usłudze Application Insights.</span><span class="sxs-lookup"><span data-stu-id="60e4c-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="60e4c-140">Poniżej przedstawiono listę zapytań, których można użyć toosee hello dzienników</span><span class="sxs-lookup"><span data-stu-id="60e4c-140">Here is a list of queries you can use toosee hello logs</span></span>

| <span data-ttu-id="60e4c-141">Zapytanie</span><span class="sxs-lookup"><span data-stu-id="60e4c-141">Query</span></span> | <span data-ttu-id="60e4c-142">Opis</span><span class="sxs-lookup"><span data-stu-id="60e4c-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="60e4c-143">Dane śledzenia</span><span class="sxs-lookup"><span data-stu-id="60e4c-143">traces</span></span> | <span data-ttu-id="60e4c-144">Wyświetl wszystkie dzienniki hello generowane przez usługę Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="60e4c-144">See all of hello logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="60e4c-145">ślady \\</span><span class="sxs-lookup"><span data-stu-id="60e4c-145">traces \\</span></span>| <span data-ttu-id="60e4c-146">gdzie sygnatury czasowej > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="60e4c-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="60e4c-147">Zobacz wszystkie dzienniki hello generowane przez usługę Azure AD B2C dla hello ostatni dzień</span><span class="sxs-lookup"><span data-stu-id="60e4c-147">See all of hello logs generated by Azure AD B2C for hello last day</span></span>

<span data-ttu-id="60e4c-148">wpisy Hello może trwać długo.</span><span class="sxs-lookup"><span data-stu-id="60e4c-148">hello entries may be long.</span></span>  <span data-ttu-id="60e4c-149">Wyeksportuj tooCSV dla bliższe spojrzenie.</span><span class="sxs-lookup"><span data-stu-id="60e4c-149">Export tooCSV for a closer look.</span></span>

<span data-ttu-id="60e4c-150">Dowiedz się więcej o narzędzie analityczne hello [tutaj](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="60e4c-150">You can learn more about hello Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="60e4c-151">Społeczność Hello opracowała deweloperzy tożsamości użytkownika toohelp podglądu podróży.</span><span class="sxs-lookup"><span data-stu-id="60e4c-151">hello community has developed a user journey viewer toohelp identity developers.</span></span>  <span data-ttu-id="60e4c-152">Nie jest obsługiwane przez firmę Microsoft i staje się dostępna wyłącznie jako — jest.</span><span class="sxs-lookup"><span data-stu-id="60e4c-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="60e4c-153">Odczytuje z wystąpieniem usługi Application Insights i udostępnia widok struktury także hello użytkownika przebieg zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="60e4c-153">It reads from your Application Insights instance and provides a well-structure view of hello user journey events.</span></span>  <span data-ttu-id="60e4c-154">Uzyskaj hello kodu źródłowego i wdrożyć ją w własne rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="60e4c-154">You obtain hello source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="60e4c-155">Obecnie hello dzienniki szczegółowe działania opisane w tym miejscu są zaprojektowane **tylko** tooaid w tworzenie zasad niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="60e4c-155">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="60e4c-156">Nie należy używać trybu tworzenia w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="60e4c-156">Do not use development mode in production.</span></span>  <span data-ttu-id="60e4c-157">Dzienniki zbierać wszystkie oświadczenia wysyłane tooand od dostawców tożsamości hello podczas programowania.</span><span class="sxs-lookup"><span data-stu-id="60e4c-157">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="60e4c-158">Jeśli używane w środowisku produkcyjnym, deweloperów hello przyjmuje na siebie odpowiedzialność dla wrażliwych danych osobowych (prywatnie informacje umożliwiające identyfikację) zebrane w dzienniku Insights aplikacji hello, w której jest właścicielem.</span><span class="sxs-lookup"><span data-stu-id="60e4c-158">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="60e4c-159">Te szczegółowe dzienniki są zbierane tylko, gdy zasady hello jest umieszczona na **tryb programowania**.</span><span class="sxs-lookup"><span data-stu-id="60e4c-159">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="60e4c-160">Repozytorium Github dla nieobsługiwany Przykłady zasad niestandardowych oraz narzędzia pokrewne</span><span class="sxs-lookup"><span data-stu-id="60e4c-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="60e4c-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="60e4c-161">Next Steps</span></span>

<span data-ttu-id="60e4c-162">Eksplorowanie danych hello toohelp usługi Application Insights rozumiesz sposób hello Framework obsługi tożsamości podstawowej B2C działa toodeliver napotyka własną tożsamości.</span><span class="sxs-lookup"><span data-stu-id="60e4c-162">Explore hello data in Application Insights toohelp you understand how hello Identity Experience Framework underlying B2C works toodeliver your own identity experiences.</span></span>
