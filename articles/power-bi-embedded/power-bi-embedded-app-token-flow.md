---
title: aaaAuthenticating i autoryzacji z Power BI Embedded
description: "Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="16c26-103">Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="16c26-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="16c26-104">korzysta z usługi Power BI Embedded Hello **klucze** i **tokenów aplikacji** do uwierzytelniania i autoryzacji, zamiast jawnego użytkownika końcowego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="16c26-104">hello Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="16c26-105">W tym modelu aplikacji zarządza uwierzytelniania i autoryzacji dla użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="16c26-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="16c26-106">W razie potrzeby aplikacji tworzy i wysyła żądanego raportu hello tokenów aplikacji hello, które informuje toorender naszej usługi.</span><span class="sxs-lookup"><span data-stu-id="16c26-106">When necessary, your app creates and sends hello App Tokens that tells our service toorender hello requested report.</span></span> <span data-ttu-id="16c26-107">Ten projekt nie wymaga toouse Twojej aplikacji usługi Azure Active Directory do uwierzytelniania i autoryzacji, użytkowników, mimo że nadal można.</span><span class="sxs-lookup"><span data-stu-id="16c26-107">This design doesn't require your app toouse Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-tooauthenticate"></a><span data-ttu-id="16c26-108">Dwa sposoby tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="16c26-108">Two ways tooauthenticate</span></span>

<span data-ttu-id="16c26-109">**Klucz** — można używać kluczy dla wszystkich wywołań interfejsu API REST osadzonych Power BI.</span><span class="sxs-lookup"><span data-stu-id="16c26-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="16c26-110">klucze Hello znajdują się w hello **portalu Azure** , klikając **wszystkie ustawienia** , a następnie **klucze dostępu**.</span><span class="sxs-lookup"><span data-stu-id="16c26-110">hello keys can be found in hello **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="16c26-111">Zawsze należy traktować klucz, tak jakby był on hasła.</span><span class="sxs-lookup"><span data-stu-id="16c26-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="16c26-112">Te klucze mają toomake uprawnienia wywołać jakiegokolwiek interfejsu API REST dla kolekcji określonego obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="16c26-112">These keys have permissions toomake any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="16c26-113">toouse klucza na wywołanie interfejsu REST Dodaj powitania po nagłówek autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="16c26-113">toouse a key on a REST call, add hello following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="16c26-114">**Tokenu aplikacji** -tokenów aplikacji są używane dla wszystkich żądań osadzania.</span><span class="sxs-lookup"><span data-stu-id="16c26-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="16c26-115">Są one zaprojektowane toobe Uruchom po stronie klienta, dzięki czemu są ograniczone tooa pojedynczy raport i jej najlepsze praktyki tooset czas wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="16c26-115">They’re designed toobe run client-side, so they're restricted tooa single report and it’s best practice tooset an expiration time.</span></span>

<span data-ttu-id="16c26-116">Tokenów aplikacji są JWT (JSON Web Token), który jest podpisany przez jeden z kluczy.</span><span class="sxs-lookup"><span data-stu-id="16c26-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="16c26-117">Token aplikacji może zawierać powitania po oświadczeń:</span><span class="sxs-lookup"><span data-stu-id="16c26-117">Your app token can contain hello following claims:</span></span>

| <span data-ttu-id="16c26-118">Claim</span><span class="sxs-lookup"><span data-stu-id="16c26-118">Claim</span></span> | <span data-ttu-id="16c26-119">Opis</span><span class="sxs-lookup"><span data-stu-id="16c26-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="16c26-120">**VER**</span><span class="sxs-lookup"><span data-stu-id="16c26-120">**ver**</span></span> |<span data-ttu-id="16c26-121">Wersja Hello tokenu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="16c26-121">hello version of hello app token.</span></span> <span data-ttu-id="16c26-122">0.2.0 jest hello bieżącej wersji.</span><span class="sxs-lookup"><span data-stu-id="16c26-122">0.2.0 is hello current version.</span></span> |
| <span data-ttu-id="16c26-123">**lub**</span><span class="sxs-lookup"><span data-stu-id="16c26-123">**aud**</span></span> |<span data-ttu-id="16c26-124">Witaj przeznaczony odbiorcy tokenu hello.</span><span class="sxs-lookup"><span data-stu-id="16c26-124">hello intended recipient of hello token.</span></span> <span data-ttu-id="16c26-125">Do użytku w usłudze Power BI Embedded: "https://analysis.windows.net/powerbi/api".</span><span class="sxs-lookup"><span data-stu-id="16c26-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="16c26-126">**iss**</span><span class="sxs-lookup"><span data-stu-id="16c26-126">**iss**</span></span> |<span data-ttu-id="16c26-127">Ciąg wskazujący aplikacji hello wystawiony hello token.</span><span class="sxs-lookup"><span data-stu-id="16c26-127">A string indicating hello application which issued hello token.</span></span> |
| <span data-ttu-id="16c26-128">**Typ**</span><span class="sxs-lookup"><span data-stu-id="16c26-128">**type**</span></span> |<span data-ttu-id="16c26-129">Typ Hello tokenu aplikacji, która jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="16c26-129">hello type of app token which is being created.</span></span> <span data-ttu-id="16c26-130">Bieżący typ hello obsługiwane tylko **osadzić**.</span><span class="sxs-lookup"><span data-stu-id="16c26-130">Current hello only supported type is **embed**.</span></span> |
| <span data-ttu-id="16c26-131">**WCN**</span><span class="sxs-lookup"><span data-stu-id="16c26-131">**wcn**</span></span> |<span data-ttu-id="16c26-132">Token hello nazwę kolekcji obszaru roboczego zostało wystawione.</span><span class="sxs-lookup"><span data-stu-id="16c26-132">Workspace collection name hello token is being issued for.</span></span> |
| <span data-ttu-id="16c26-133">**bazy danych WID**</span><span class="sxs-lookup"><span data-stu-id="16c26-133">**wid**</span></span> |<span data-ttu-id="16c26-134">Token hello identyfikator obszaru roboczego zostało wystawione.</span><span class="sxs-lookup"><span data-stu-id="16c26-134">Workspace ID hello token is being issued for.</span></span> |
| <span data-ttu-id="16c26-135">**Identyfikator RID**</span><span class="sxs-lookup"><span data-stu-id="16c26-135">**rid**</span></span> |<span data-ttu-id="16c26-136">Token hello Identyfikatora raportu zostało wystawione.</span><span class="sxs-lookup"><span data-stu-id="16c26-136">Report ID hello token is being issued for.</span></span> |
| <span data-ttu-id="16c26-137">**Nazwa użytkownika** (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="16c26-137">**username** (optional)</span></span> |<span data-ttu-id="16c26-138">Używane zabezpieczenia na poziomie wiersza, jest to ciąg, który może ułatwić identyfikację hello użytkownika, stosując zasady zabezpieczenia na poziomie wiersza.</span><span class="sxs-lookup"><span data-stu-id="16c26-138">Used with RLS, this is a string that can help identify hello user when applying RLS rules.</span></span> |
| <span data-ttu-id="16c26-139">**role** (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="16c26-139">**roles** (optional)</span></span> |<span data-ttu-id="16c26-140">Ciąg zawierający tooselect ról hello podczas stosowania zasad zabezpieczeń na poziomie wiersza.</span><span class="sxs-lookup"><span data-stu-id="16c26-140">A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="16c26-141">Przekazywanie więcej niż jednej roli, powinien zostać przekazany jako tablica ciągu.</span><span class="sxs-lookup"><span data-stu-id="16c26-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="16c26-142">**punkt połączenia usługi** (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="16c26-142">**scp** (optional)</span></span> |<span data-ttu-id="16c26-143">Ciąg zawierający hello zakresy uprawnień.</span><span class="sxs-lookup"><span data-stu-id="16c26-143">A string containing hello permissions scopes.</span></span> <span data-ttu-id="16c26-144">Przekazywanie więcej niż jednej roli, powinien zostać przekazany jako tablica ciągu.</span><span class="sxs-lookup"><span data-stu-id="16c26-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="16c26-145">**EXP** (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="16c26-145">**exp** (optional)</span></span> |<span data-ttu-id="16c26-146">Wskazuje czas hello, w których hello wygaśnięcia tokenu.</span><span class="sxs-lookup"><span data-stu-id="16c26-146">Indicates hello time in which hello token will expire.</span></span> <span data-ttu-id="16c26-147">Te mają być przekazywane w jako systemu Unix sygnatur czasowych.</span><span class="sxs-lookup"><span data-stu-id="16c26-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="16c26-148">**NBF** (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="16c26-148">**nbf** (optional)</span></span> |<span data-ttu-id="16c26-149">Wskazuje czas hello, w których hello token zaczyna się ważny.</span><span class="sxs-lookup"><span data-stu-id="16c26-149">Indicates hello time in which hello token starts being valid.</span></span> <span data-ttu-id="16c26-150">Te mają być przekazywane w jako systemu Unix sygnatur czasowych.</span><span class="sxs-lookup"><span data-stu-id="16c26-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="16c26-151">Przykładowy token aplikacji będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="16c26-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="16c26-152">Gdy zdekodowany, ekran będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="16c26-152">When decoded, it will look something like this:</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

<span data-ttu-id="16c26-153">Brak dostępnych metod w hello zestawów SDK, które ułatwia tworzenie apptokens.</span><span class="sxs-lookup"><span data-stu-id="16c26-153">There are methods available within hello SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="16c26-154">Na przykład dla platformy .NET można przyjrzeć się hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) klasy i hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) metody.</span><span class="sxs-lookup"><span data-stu-id="16c26-154">For example, for .NET you can look at hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="16c26-155">Dla hello zestawu .NET SDK, mogą odwoływać się za[zakresy](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span><span class="sxs-lookup"><span data-stu-id="16c26-155">For hello .NET SDK, you can refer too[Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="16c26-156">Zakresy</span><span class="sxs-lookup"><span data-stu-id="16c26-156">Scopes</span></span>

<span data-ttu-id="16c26-157">Tokeny osadzania można toorestrict użycia zasobów hello, który zapewnia dostęp do.</span><span class="sxs-lookup"><span data-stu-id="16c26-157">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="16c26-158">Z tego powodu można wygenerować token z zakresu uprawnień.</span><span class="sxs-lookup"><span data-stu-id="16c26-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="16c26-159">Oto Hello hello dostępnych zakresów dla Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="16c26-159">hello following are hello available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="16c26-160">Zakres</span><span class="sxs-lookup"><span data-stu-id="16c26-160">Scope</span></span>|<span data-ttu-id="16c26-161">Opis</span><span class="sxs-lookup"><span data-stu-id="16c26-161">Description</span></span>|
|---|---|
|<span data-ttu-id="16c26-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="16c26-162">Dataset.Read</span></span>|<span data-ttu-id="16c26-163">Udostępnia uprawnienie tooread hello określony zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="16c26-163">Provides permission tooread hello specified dataset.</span></span>|
|<span data-ttu-id="16c26-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="16c26-164">Dataset.Write</span></span>|<span data-ttu-id="16c26-165">Udostępnia uprawnienie toowrite toohello określony zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="16c26-165">Provides permission toowrite toohello specified dataset.</span></span>|
|<span data-ttu-id="16c26-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="16c26-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="16c26-167">Udostępnia uprawnienie zapisu i tooread toohello określonego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="16c26-167">Provides permission tooread and write toohello specificed dataset.</span></span>|
|<span data-ttu-id="16c26-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="16c26-168">Report.Read</span></span>|<span data-ttu-id="16c26-169">Udostępnia uprawnienie tooview hello określony raport.</span><span class="sxs-lookup"><span data-stu-id="16c26-169">Provides permission tooview hello specified report.</span></span>|
|<span data-ttu-id="16c26-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="16c26-170">Report.ReadWrite</span></span>|<span data-ttu-id="16c26-171">Zapewnia możliwość tooview uprawnień i edytowanie hello określonego raportu.</span><span class="sxs-lookup"><span data-stu-id="16c26-171">Provides permission tooview and edit hello specified report.</span></span>|
|<span data-ttu-id="16c26-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="16c26-172">Workspace.Report.Create</span></span>|<span data-ttu-id="16c26-173">Zapewnia nowy raport w hello określony toocreate uprawnień obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="16c26-173">Provides permission toocreate a new report within hello specified workspace.</span></span>|
|<span data-ttu-id="16c26-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="16c26-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="16c26-175">Udostępnia uprawnienie tooclone istniejącego raportu w hello określony obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="16c26-175">Provides permission tooclone an existing report within hello specified workspace.</span></span>|

<span data-ttu-id="16c26-176">Przy użyciu spacji między zakresy hello podobnie następującej hello, możesz podać wiele zakresów.</span><span class="sxs-lookup"><span data-stu-id="16c26-176">You can supply multiple scopes by using a space between hello scopes like hello following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="16c26-177">**Wymagane oświadczenia - zakresów**</span><span class="sxs-lookup"><span data-stu-id="16c26-177">**Required claims - scopes**</span></span>

<span data-ttu-id="16c26-178">punkt połączenia usługi: scopesClaim {scopesClaim} może być ciąg lub tablica ciągów, biorąc pod uwagę hello dozwolone uprawnienia tooworkspace zasobów (raport, zestaw danych itp.)</span><span class="sxs-lookup"><span data-stu-id="16c26-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting hello allowed permissions tooworkspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="16c26-179">Token dekodowane, z zakresów zdefiniowanych, będzie wyglądać podobnie następujące toohello.</span><span class="sxs-lookup"><span data-stu-id="16c26-179">A decoded token, with scopes defined, would look similar toohello following.</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a><span data-ttu-id="16c26-180">Operacje i zakresy</span><span class="sxs-lookup"><span data-stu-id="16c26-180">Operations and scopes</span></span>

|<span data-ttu-id="16c26-181">Operacja</span><span class="sxs-lookup"><span data-stu-id="16c26-181">Operation</span></span>|<span data-ttu-id="16c26-182">Zasób docelowy</span><span class="sxs-lookup"><span data-stu-id="16c26-182">Target resource</span></span>|<span data-ttu-id="16c26-183">Token uprawnień</span><span class="sxs-lookup"><span data-stu-id="16c26-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="16c26-184">Tworzenie nowego raportu oparte na zestawie danych (w pamięci).</span><span class="sxs-lookup"><span data-stu-id="16c26-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="16c26-185">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="16c26-185">Dataset</span></span>|<span data-ttu-id="16c26-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="16c26-186">Dataset.Read</span></span>|
|<span data-ttu-id="16c26-187">Tworzenie nowego raportu oparte na zestawie danych (w pamięci) i Zapisz hello raportu.</span><span class="sxs-lookup"><span data-stu-id="16c26-187">Create (in-memory) a new report based on a dataset and save hello report.</span></span>|<span data-ttu-id="16c26-188">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="16c26-188">Dataset</span></span>|<span data-ttu-id="16c26-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="16c26-189">* Dataset.Read</span></span><br><span data-ttu-id="16c26-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="16c26-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="16c26-191">Wyświetlanie i Eksploruj/edytowanie (w pamięci) istniejącego raportu.</span><span class="sxs-lookup"><span data-stu-id="16c26-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="16c26-192">Report.Read oznacza Dataset.Read.</span><span class="sxs-lookup"><span data-stu-id="16c26-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="16c26-193">To nie zezwala na edycję toosave uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="16c26-193">This will not allow permissions toosave edits.</span></span>|<span data-ttu-id="16c26-194">Raport</span><span class="sxs-lookup"><span data-stu-id="16c26-194">Report</span></span>|<span data-ttu-id="16c26-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="16c26-195">Report.Read</span></span>|
|<span data-ttu-id="16c26-196">Edytuj i zapisuj istniejącego raportu.</span><span class="sxs-lookup"><span data-stu-id="16c26-196">Edit and save an existing report.</span></span>|<span data-ttu-id="16c26-197">Raport</span><span class="sxs-lookup"><span data-stu-id="16c26-197">Report</span></span>|<span data-ttu-id="16c26-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="16c26-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="16c26-199">Zapisz kopię raportu (Zapisz jako).</span><span class="sxs-lookup"><span data-stu-id="16c26-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="16c26-200">Raport</span><span class="sxs-lookup"><span data-stu-id="16c26-200">Report</span></span>|<span data-ttu-id="16c26-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="16c26-201">* Report.Read</span></span><br><span data-ttu-id="16c26-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="16c26-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-hello-flow-works"></a><span data-ttu-id="16c26-203">Oto, jak działa hello przepływu</span><span class="sxs-lookup"><span data-stu-id="16c26-203">Here's how hello flow works</span></span>
1. <span data-ttu-id="16c26-204">Skopiuj hello interfejsu API klucze tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16c26-204">Copy hello API keys tooyour application.</span></span> <span data-ttu-id="16c26-205">Można uzyskać klucze hello **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="16c26-205">You can get hello keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="16c26-206">Token deklaracji rozkazujących oświadczenia i ma czasu wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="16c26-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="16c26-207">Pobiera podpisany token kluczy dostępu do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="16c26-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="16c26-208">Użytkownik żąda tooview raportu.</span><span class="sxs-lookup"><span data-stu-id="16c26-208">User requests tooview a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="16c26-209">Token została zweryfikowana za pomocą kluczy dostępu do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="16c26-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="16c26-210">Usługa Power BI Embedded wysyła toouser raportu.</span><span class="sxs-lookup"><span data-stu-id="16c26-210">Power BI Embedded sends a report toouser.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="16c26-211">Po **Power BI Embedded** wysyła użytkownika toohello raportu hello użytkownika można wyświetlić raport hello w niestandardowych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16c26-211">After **Power BI Embedded** sends a report toohello user, hello user can view hello report in your custom app.</span></span> <span data-ttu-id="16c26-212">Na przykład, jeśli importowany hello [analizowania sprzedaży PBIX dane przykładowe](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello przykładową aplikację sieci web będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="16c26-212">For example, if you imported hello [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="16c26-213">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="16c26-213">See Also</span></span>

[<span data-ttu-id="16c26-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="16c26-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="16c26-215">Rozpoczęcie pracy z przykładem Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="16c26-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="16c26-216">Typowe scenariusze Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="16c26-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="16c26-217">Wprowadzenie do programu Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="16c26-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="16c26-218">Usługa Power BI CSharp repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="16c26-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="16c26-219">Masz więcej pytań?</span><span class="sxs-lookup"><span data-stu-id="16c26-219">More questions?</span></span> [<span data-ttu-id="16c26-220">Spróbuj hello Power BI społeczności</span><span class="sxs-lookup"><span data-stu-id="16c26-220">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

