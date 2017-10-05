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
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="31571-103">Azure Active Directory B2C: Zbierania dzienników</span><span class="sxs-lookup"><span data-stu-id="31571-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="31571-104">Ten artykuł zawiera kroki do zbierania dzienników z usługi Azure AD B2C, dzięki czemu można diagnozować problemy z zasadami dotyczącymi zasobów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="31571-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="31571-105">Obecnie dzienniki szczegółowe działania opisane w tym miejscu są zaprojektowane **tylko** ułatwiających tworzenie niestandardowych zasad.</span><span class="sxs-lookup"><span data-stu-id="31571-105">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="31571-106">Nie należy używać trybu tworzenia w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="31571-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="31571-107">Dzienniki zbierać wszystkie oświadczenia wysyłane do i z dostawców tożsamości w czasie projektowania.</span><span class="sxs-lookup"><span data-stu-id="31571-107">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="31571-108">Jeśli używane w środowisku produkcyjnym, deweloper przyjmuje na siebie odpowiedzialność dla wrażliwych danych osobowych (prywatnie informacje umożliwiające identyfikację) zebrane w dzienniku Insights aplikacji, w której jest właścicielem.</span><span class="sxs-lookup"><span data-stu-id="31571-108">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="31571-109">Te szczegółowe dzienniki są zbierane tylko, gdy zasady jest umieszczona na **tryb programowania**.</span><span class="sxs-lookup"><span data-stu-id="31571-109">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="31571-110">Użyj usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="31571-110">Use Application Insights</span></span>

<span data-ttu-id="31571-111">Usługa Azure AD B2C obsługuje funkcję wysyłania danych do usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="31571-111">Azure AD B2C supports a feature for sending data to Application Insights.</span></span>  <span data-ttu-id="31571-112">Usługa Application Insights umożliwia diagnozowanie wyjątków i wizualizację problemy z wydajnością aplikacji.</span><span class="sxs-lookup"><span data-stu-id="31571-112">Application Insights provides a way to diagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="31571-113">Konfiguracja usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="31571-113">Setup Application Insights</span></span>

1. <span data-ttu-id="31571-114">Przejdź do witryny [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31571-114">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="31571-115">Upewnij się, że jesteś w dzierżawcy z subskrypcją platformy Azure (nie dzierżawy usługi Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="31571-115">Ensure you are in the tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="31571-116">Kliknij przycisk **+ nowy** w menu nawigacji po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="31571-116">Click **+ New** in the left-hand navigation menu.</span></span>
1. <span data-ttu-id="31571-117">Wyszukaj i wybierz **usługi Application Insights**, następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="31571-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="31571-118">Wypełnij formularz, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="31571-118">Complete the form and click **Create**.</span></span> <span data-ttu-id="31571-119">Wybierz **ogólne** dla **typu aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="31571-119">Select **General** for the **Application Type**.</span></span>
1. <span data-ttu-id="31571-120">Po utworzeniu zasobu, należy otworzyć zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="31571-120">Once the resource has been created, open the Application Insights resource.</span></span>
1. <span data-ttu-id="31571-121">Znajdź **właściwości** w menu po lewej i kliknij go.</span><span class="sxs-lookup"><span data-stu-id="31571-121">Find **Properties** in the left-menu, and click on it.</span></span>
1. <span data-ttu-id="31571-122">Kopiuj **klucza Instrumentacji** i zapisz go w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="31571-122">Copy the **Instrumentation Key** and save it for the next section.</span></span>

### <a name="set-up-the-custom-policy"></a><span data-ttu-id="31571-123">Ustawienia zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="31571-123">Set up the custom policy</span></span>

1. <span data-ttu-id="31571-124">Otwórz plik RP (na przykład SignUpOrSignin.xml).</span><span class="sxs-lookup"><span data-stu-id="31571-124">Open the RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="31571-125">Dodaj następujące atrybuty `<TrustFrameworkPolicy>` elementu:</span><span class="sxs-lookup"><span data-stu-id="31571-125">Add the following attributes to the `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="31571-126">Jeśli nie istnieje już, Dodaj węzeł podrzędny `<UserJourneyBehaviors>` do `<RelyingParty>` węzła.</span><span class="sxs-lookup"><span data-stu-id="31571-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` to the `<RelyingParty>` node.</span></span> <span data-ttu-id="31571-127">Znajdować się natychmiast po`<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="31571-127">It must be located immediately after the `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="31571-128">Dodaj następujący węzeł jako element podrzędny `<UserJourneyBehaviors>` elementu.</span><span class="sxs-lookup"><span data-stu-id="31571-128">Add the following node as a child of the `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="31571-129">Upewnij się zastąpić `{Your Application Insights Key}` z **klucza Instrumentacji** uzyskane z usługi Application Insights w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="31571-129">Make sure to replace `{Your Application Insights Key}` with the **Instrumentation Key** that you obtained from Application Insights in the previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="31571-130">`DeveloperMode="true"`Określa, że ApplicationInsights w celu przyspieszenia telemetrii za pośrednictwem potoku przetwarzania dobry do tworzenia aplikacji, ale ograniczonego w dużej ilości.</span><span class="sxs-lookup"><span data-stu-id="31571-130">`DeveloperMode="true"` tells ApplicationInsights to expedite the telemetry through the processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="31571-131">`ClientEnabled="true"`wysyła ApplicationInsights skryptu po stronie klienta do śledzenia błędy po stronie klienta i widoku strony (nie wymagane).</span><span class="sxs-lookup"><span data-stu-id="31571-131">`ClientEnabled="true"` sends the ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="31571-132">`ServerEnabled="true"`wysyła istniejących JSON UserJourneyRecorder jako zdarzenie niestandardowe do usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="31571-132">`ServerEnabled="true"` sends the existing UserJourneyRecorder JSON as a custom event to Application Insights.</span></span>
<span data-ttu-id="31571-133">Przykład:</span><span class="sxs-lookup"><span data-stu-id="31571-133">Sample:</span></span>

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

3. <span data-ttu-id="31571-134">Przekaż zasad.</span><span class="sxs-lookup"><span data-stu-id="31571-134">Upload the policy.</span></span>

### <a name="see-the-logs-in-application-insights"></a><span data-ttu-id="31571-135">Można znaleźć w dziennikach w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="31571-135">See the logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="31571-136">Brak krótki opóźnienie (mniej niż pięć minut), aby zobaczyć nowe dzienniki w usłudze Application Insights.</span><span class="sxs-lookup"><span data-stu-id="31571-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="31571-137">Otwórz zasobu usługi Application Insights, który został utworzony w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31571-137">Open the Application Insights resource that you created in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="31571-138">W **omówienie** menu, kliknij polecenie **Analytics**.</span><span class="sxs-lookup"><span data-stu-id="31571-138">In the **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="31571-139">Otwórz nową kartę w usłudze Application Insights.</span><span class="sxs-lookup"><span data-stu-id="31571-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="31571-140">Poniżej przedstawiono listę zapytania używanego do znajduje się w dziennikach</span><span class="sxs-lookup"><span data-stu-id="31571-140">Here is a list of queries you can use to see the logs</span></span>

| <span data-ttu-id="31571-141">Zapytanie</span><span class="sxs-lookup"><span data-stu-id="31571-141">Query</span></span> | <span data-ttu-id="31571-142">Opis</span><span class="sxs-lookup"><span data-stu-id="31571-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="31571-143">Dane śledzenia</span><span class="sxs-lookup"><span data-stu-id="31571-143">traces</span></span> | <span data-ttu-id="31571-144">Wyświetl wszystkie dzienniki generowane przez usługę Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="31571-144">See all of the logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="31571-145">ślady \\</span><span class="sxs-lookup"><span data-stu-id="31571-145">traces \\</span></span>| <span data-ttu-id="31571-146">gdzie sygnatury czasowej > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="31571-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="31571-147">Wyświetl wszystkie dzienniki generowane przez usługę Azure AD B2C w ciągu ostatniego dnia</span><span class="sxs-lookup"><span data-stu-id="31571-147">See all of the logs generated by Azure AD B2C for the last day</span></span>

<span data-ttu-id="31571-148">Wpisy może trwać długo.</span><span class="sxs-lookup"><span data-stu-id="31571-148">The entries may be long.</span></span>  <span data-ttu-id="31571-149">Eksportuj do pliku CSV dla bliższe spojrzenie.</span><span class="sxs-lookup"><span data-stu-id="31571-149">Export to CSV for a closer look.</span></span>

<span data-ttu-id="31571-150">Dowiedz się więcej o narzędziu Analytics [tutaj](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="31571-150">You can learn more about the Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="31571-151">Społeczność opracowała podglądu przebieg użytkownika, aby pomóc deweloperom w tożsamości.</span><span class="sxs-lookup"><span data-stu-id="31571-151">The community has developed a user journey viewer to help identity developers.</span></span>  <span data-ttu-id="31571-152">Nie jest obsługiwane przez firmę Microsoft i staje się dostępna wyłącznie jako — jest.</span><span class="sxs-lookup"><span data-stu-id="31571-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="31571-153">Odczytuje z wystąpieniem usługi Application Insights i udostępnia widok struktury także użytkownika przebieg zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="31571-153">It reads from your Application Insights instance and provides a well-structure view of the user journey events.</span></span>  <span data-ttu-id="31571-154">Uzyskanie kodu źródłowego i wdrożyć ją w własne rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="31571-154">You obtain the source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="31571-155">Obecnie dzienniki szczegółowe działania opisane w tym miejscu są zaprojektowane **tylko** ułatwiających tworzenie niestandardowych zasad.</span><span class="sxs-lookup"><span data-stu-id="31571-155">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="31571-156">Nie należy używać trybu tworzenia w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="31571-156">Do not use development mode in production.</span></span>  <span data-ttu-id="31571-157">Dzienniki zbierać wszystkie oświadczenia wysyłane do i z dostawców tożsamości w czasie projektowania.</span><span class="sxs-lookup"><span data-stu-id="31571-157">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="31571-158">Jeśli używane w środowisku produkcyjnym, deweloper przyjmuje na siebie odpowiedzialność dla wrażliwych danych osobowych (prywatnie informacje umożliwiające identyfikację) zebrane w dzienniku Insights aplikacji, w której jest właścicielem.</span><span class="sxs-lookup"><span data-stu-id="31571-158">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="31571-159">Te szczegółowe dzienniki są zbierane tylko, gdy zasady jest umieszczona na **tryb programowania**.</span><span class="sxs-lookup"><span data-stu-id="31571-159">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="31571-160">Repozytorium Github dla nieobsługiwany Przykłady zasad niestandardowych oraz narzędzia pokrewne</span><span class="sxs-lookup"><span data-stu-id="31571-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="31571-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="31571-161">Next Steps</span></span>

<span data-ttu-id="31571-162">Eksplorowanie danych w usłudze Application Insights, aby ułatwić zrozumienie sposobu wykonywania Framework obsługi tożsamości podstawowej B2C działa, aby dostarczyć własny tożsamości.</span><span class="sxs-lookup"><span data-stu-id="31571-162">Explore the data in Application Insights to help you understand how the Identity Experience Framework underlying B2C works to deliver your own identity experiences.</span></span>
