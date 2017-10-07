---
title: 'Azure AD Connect: Uwierzytelniania przekazywanego - blokady inteligentnej | Dokumentacja firmy Microsoft'
description: "W tym artykule opisano, jak Azure Active Directory (Azure AD) przekazywanego uwierzytelniania przed atakami siłowymi haseł w chmurze hello chroni konta lokalnego."
services: active-directory
keywords: "Azure AD Connect przekazywanego uwierzytelniania, instalacji usługi Active Directory, wymaganych składników dla usługi Azure AD, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="877d0-104">Uwierzytelniania przekazywanego usługi Azure Active Directory: Blokady inteligentnej</span><span class="sxs-lookup"><span data-stu-id="877d0-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="877d0-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="877d0-105">Overview</span></span>

<span data-ttu-id="877d0-106">Usługi Azure AD chroni przed atakami siłowymi hasła i uniemożliwia użytkownikom oryginalnego blokowanie poza ich usługi Office 365 i aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="877d0-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="877d0-107">Ta funkcja o nazwie **blokady inteligentnej**, jest obsługiwana w przypadku korzystania z uwierzytelniania przekazywanego jako metodę logowania.</span><span class="sxs-lookup"><span data-stu-id="877d0-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="877d0-108">Blokady inteligentnej jest domyślnie włączona dla wszystkich dzierżawców i ochrony kont użytkowników cały czas hello; nie konieczności tooturn nie istnieje on w.</span><span class="sxs-lookup"><span data-stu-id="877d0-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all hello time; there is no need tooturn it on.</span></span>

<span data-ttu-id="877d0-109">Blokady inteligentnej działa przez śledzenie nieudanych prób logowania i po pewnym **próg blokady**, rozpoczynając **czas trwania blokady**.</span><span class="sxs-lookup"><span data-stu-id="877d0-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="877d0-110">Wszelkich prób logowania z atakująca hello podczas hello czas trwania blokady są odrzucane.</span><span class="sxs-lookup"><span data-stu-id="877d0-110">Any sign-in attempts from hello attacker during hello Lockout Duration are rejected.</span></span> <span data-ttu-id="877d0-111">Jeśli atak powitania będzie nadal występować, hello kolejnych nieudanych prób zalogowania po zakończeniu hello czas trwania blokady wynik w dłuższym czasie trwania blokady.</span><span class="sxs-lookup"><span data-stu-id="877d0-111">If hello attack continues, hello subsequent failed sign-in attempts after hello Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="877d0-112">Domyślna Hello progu blokady konta to 10 nieudanych prób i domyślnego hello czas trwania blokady wynosi 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="877d0-112">hello default Lockout Threshold is 10 failed attempts, and hello default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="877d0-113">Blokady inteligentnej rozróżnia również logowania z oryginalnego użytkowników i osoby atakujące i tylko blokowane osoby atakujące hello w większości przypadków.</span><span class="sxs-lookup"><span data-stu-id="877d0-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out hello attackers in most cases.</span></span> <span data-ttu-id="877d0-114">Ta funkcja zapobiega osoby atakujące złośliwie zablokowania oryginalnego użytkowników.</span><span class="sxs-lookup"><span data-stu-id="877d0-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="877d0-115">Używamy poza logowania zachowanie użytkowników urządzeń & przeglądarek i innych toodistinguish sygnały między użytkownikami oryginalny i osoby atakujące.</span><span class="sxs-lookup"><span data-stu-id="877d0-115">We use past sign-in behavior, users’ devices & browsers and other signals toodistinguish between genuine users and attackers.</span></span> <span data-ttu-id="877d0-116">Firma Microsoft stale umożliwiają zwiększenie nasze algorytmy.</span><span class="sxs-lookup"><span data-stu-id="877d0-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="877d0-117">Ponieważ uwierzytelniania przekazywanego przekazuje żądania weryfikacji haseł na lokalnej usługi Active Directory (AD), należy atakującym tooprevent blokowania kont usługi AD użytkowników.</span><span class="sxs-lookup"><span data-stu-id="877d0-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need tooprevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="877d0-118">Ponieważ masz zasad blokady konta AD (w szczególności [ **próg blokady konta** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) i [ **Zresetuj licznik blokady konta po zasady** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), należy próg blokady tooconfigure usługi Azure AD i czas trwania blokady odpowiednio wartości toofilter limit ataków w chmurze hello przed dotarciem lokalnej usługi AD.</span><span class="sxs-lookup"><span data-stu-id="877d0-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need tooconfigure Azure AD’s Lockout Threshold and Lockout Duration values appropriately toofilter out attacks in hello cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="877d0-119">funkcji blokady inteligentnej Hello jest wolny i jest _na_ domyślnie dla wszystkich klientów.</span><span class="sxs-lookup"><span data-stu-id="877d0-119">hello Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="877d0-120">Modyfikowanie progu blokady konta usługi Azure AD i czas trwania blokady wartości przy użyciu interfejsu API programu Graph musi jednak licencji dzierżawy toohave co najmniej jednej usługi Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="877d0-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant toohave at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="877d0-121">Nie wymagają licencji usługi Azure AD Premium P2 _dla każdego użytkownika_ funkcji blokady inteligentnej hello tooget przy użyciu uwierzytelniania przekazywanego.</span><span class="sxs-lookup"><span data-stu-id="877d0-121">You don't need an Azure AD Premium P2 license _per user_ tooget hello Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="877d0-122">tooensure czy użytkowników lokalnych kont usługi AD są również chronione, należy tooensure który:</span><span class="sxs-lookup"><span data-stu-id="877d0-122">tooensure that your users’ on-premises AD accounts are well protected, you need tooensure that:</span></span>

1.  <span data-ttu-id="877d0-123">Progu blokady konta usługi Azure AD jest _mniej_ niż próg blokady konta przez usługi AD.</span><span class="sxs-lookup"><span data-stu-id="877d0-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="877d0-124">Firma Microsoft zaleca ustawienie wartości hello próg blokady konta przez usługi AD jest co najmniej dwie lub trzy razy progu blokady konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="877d0-124">We recommend that you set hello values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="877d0-125">Czas trwania blokady usługi Azure AD (reprezentowane w sekundach) jest _dłużej_ niż Directory resetowania konta blokady licznika po (reprezentowane w minutach).</span><span class="sxs-lookup"><span data-stu-id="877d0-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="877d0-126">Sprawdź zasad blokady konta usługi AD</span><span class="sxs-lookup"><span data-stu-id="877d0-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="877d0-127">Użyj zasad blokady konta AD hello następujące instrukcje tooverify:</span><span class="sxs-lookup"><span data-stu-id="877d0-127">Use hello following instructions tooverify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="877d0-128">Narzędzia do zarządzania zasadami grupy Otwórz hello.</span><span class="sxs-lookup"><span data-stu-id="877d0-128">Open hello Group Policy Management tool.</span></span>
2.  <span data-ttu-id="877d0-129">Edytuj hello zasady grupy zastosowane tooall użytkowników, na przykład hello domyślne zasady domeny.</span><span class="sxs-lookup"><span data-stu-id="877d0-129">Edit hello group policy that is applied tooall users, for example, hello Default Domain Policy.</span></span>
3.  <span data-ttu-id="877d0-130">Przejdź tooComputer Konfiguracja komputera\Zasady\Ustawienia systemu Windows\Ustawienia zabezpieczeń\Zasady konta\Zasady blokady zasady.</span><span class="sxs-lookup"><span data-stu-id="877d0-130">Navigate tooComputer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="877d0-131">Sprawdź wartości progu blokady konta i zresetuj licznik blokady konta po.</span><span class="sxs-lookup"><span data-stu-id="877d0-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![Zasady blokowania kont usługi AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a><span data-ttu-id="877d0-133">Użyj toomanage interfejsu API programu Graph hello wartości blokady inteligentnej Twojej dzierżawy</span><span class="sxs-lookup"><span data-stu-id="877d0-133">Use hello Graph API toomanage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="877d0-134">Modyfikowanie progu blokady konta i czas trwania blokady wartości przy użyciu interfejsu API programu Graph usługi Azure AD to funkcja usługi Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="877d0-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="877d0-135">On również wymaga od Ciebie toobe administratora globalnego w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="877d0-135">It also needs you toobe a Global Administrator on your tenant.</span></span>

<span data-ttu-id="877d0-136">Można użyć [Explorer wykres](https://developer.microsoft.com/graph/graph-explorer) tooread, ustaw i zaktualizuj wartości blokady inteligentnej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="877d0-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) tooread, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="877d0-137">Jednak możesz również wykonać te operacje programowo.</span><span class="sxs-lookup"><span data-stu-id="877d0-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="877d0-138">Inteligentne blokady odczytu wartości</span><span class="sxs-lookup"><span data-stu-id="877d0-138">Read Smart Lockout values</span></span>

<span data-ttu-id="877d0-139">Wykonaj te kroki tooread wartości blokady inteligentnej Twojej dzierżawy:</span><span class="sxs-lookup"><span data-stu-id="877d0-139">Follow these steps tooread your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="877d0-140">Zaloguj się do Eksploratora wykresu jako Administrator globalny dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="877d0-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="877d0-141">Jeśli zostanie wyświetlony monit, Udziel dostępu dla hello wymagane uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="877d0-141">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="877d0-142">Kliknij polecenie "Modyfikuj uprawnienia" i wybierz uprawnienie "Directory.ReadWrite.All" hello.</span><span class="sxs-lookup"><span data-stu-id="877d0-142">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="877d0-143">Żądania interfejsu API programu Graph hello należy skonfigurować następująco: Ustaw wersję zbyt "BETA", typ żądania zbyt "GET" i adresu URL za`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="877d0-143">Configure hello Graph API request as follows: Set version too“BETA”, request type too“GET” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="877d0-144">Kliknij przycisk "Uruchom kwerendę" toosee wartości blokady inteligentnej swojej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="877d0-144">Click "Run Query" toosee your tenant's Smart Lockout values.</span></span> <span data-ttu-id="877d0-145">Jeśli nie zdefiniowano wartości Twojej dzierżawy przed, pojawi się pusty zestaw.</span><span class="sxs-lookup"><span data-stu-id="877d0-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="877d0-146">Ustaw wartości inteligentne blokady</span><span class="sxs-lookup"><span data-stu-id="877d0-146">Set Smart Lockout values</span></span>

<span data-ttu-id="877d0-147">Wykonaj te kroki tooset wartości blokady inteligentnej Twojej dzierżawy (na powitania tylko po raz pierwszy):</span><span class="sxs-lookup"><span data-stu-id="877d0-147">Follow these steps tooset your tenant’s Smart Lockout values (for hello first time only):</span></span>

1. <span data-ttu-id="877d0-148">Zaloguj się do Eksploratora wykresu jako Administrator globalny dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="877d0-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="877d0-149">Jeśli zostanie wyświetlony monit, Udziel dostępu dla hello wymagane uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="877d0-149">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="877d0-150">Kliknij polecenie "Modyfikuj uprawnienia" i wybierz uprawnienie "Directory.ReadWrite.All" hello.</span><span class="sxs-lookup"><span data-stu-id="877d0-150">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="877d0-151">Żądania interfejsu API programu Graph hello należy skonfigurować następująco: Ustaw wersję zbyt "BETA", typ żądania zbyt "POST" i adresu URL za`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="877d0-151">Configure hello Graph API request as follows: Set version too“BETA”, request type too“POST” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="877d0-152">Skopiuj i Wklej hello następujące żądania JSON w polu "Treści żądania" hello.</span><span class="sxs-lookup"><span data-stu-id="877d0-152">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="877d0-153">Zmień wartości blokady inteligentnej hello zgodnie z potrzebami i użyj losowy identyfikator GUID dla `templateId`.</span><span class="sxs-lookup"><span data-stu-id="877d0-153">Change hello Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="877d0-154">Kliknij przycisk "Uruchom kwerendę" tooset wartości blokady inteligentnej swojej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="877d0-154">Click "Run Query" tooset your tenant's Smart Lockout values.</span></span>

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
><span data-ttu-id="877d0-155">Jeśli nie są używane, można pozostawić hello **BannedPasswordList** i **EnableBannedPasswordCheck** wartości jako pusty ("") i "false" odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="877d0-155">If you are not using them, you can leave hello **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="877d0-156">Sprawdź, czy ma ustawiony prawidłowo przy użyciu wartości blokady inteligentnej Twojej dzierżawy [te kroki](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="877d0-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="877d0-157">Aby zaktualizować inteligentne blokady</span><span class="sxs-lookup"><span data-stu-id="877d0-157">Update Smart Lockout values</span></span>

<span data-ttu-id="877d0-158">Wartości blokady inteligentnej Twojej dzierżawy (jeśli zostały skonfigurowane je przed) wykonaj tooupdate te kroki:</span><span class="sxs-lookup"><span data-stu-id="877d0-158">Follow these steps tooupdate your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="877d0-159">Zaloguj się do Eksploratora wykresu jako Administrator globalny dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="877d0-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="877d0-160">Jeśli zostanie wyświetlony monit, Udziel dostępu dla hello wymagane uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="877d0-160">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="877d0-161">Kliknij polecenie "Modyfikuj uprawnienia" i wybierz uprawnienie "Directory.ReadWrite.All" hello.</span><span class="sxs-lookup"><span data-stu-id="877d0-161">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="877d0-162">[Wykonaj te kroki tooread Twojej dzierżawy blokady inteligentnej wartości](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="877d0-162">[Follow these steps tooread your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="877d0-163">Kopiuj hello `id` wartość (GUID) elementu hello o nazwie "wyświetlanej" jako "PasswordRuleSettings".</span><span class="sxs-lookup"><span data-stu-id="877d0-163">Copy hello `id` value (a GUID) of hello item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="877d0-164">Skonfiguruj hello żądania interfejsu API programu Graph w następujący sposób: Ustaw wersję za "BETA" typ żądania za "Poprawka" i adresu URL za`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -Użyj hello identyfikatora GUID z kroku 3 dla `<id>`.</span><span class="sxs-lookup"><span data-stu-id="877d0-164">Configure hello Graph API request as follows: Set version too“BETA”, request type too“PATCH” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use hello GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="877d0-165">Skopiuj i Wklej hello następujące żądania JSON w polu "Treści żądania" hello.</span><span class="sxs-lookup"><span data-stu-id="877d0-165">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="877d0-166">Zmień wartości blokady inteligentnej hello zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="877d0-166">Change hello Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="877d0-167">Kliknij przycisk "Uruchom kwerendę" tooupdate wartości blokady inteligentnej swojej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="877d0-167">Click "Run Query" tooupdate your tenant's Smart Lockout values.</span></span>

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

<span data-ttu-id="877d0-168">Sprawdź zaktualizowano poprawnie przy użyciu wartości blokady inteligentnej Twojej dzierżawy [te kroki](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="877d0-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="877d0-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="877d0-169">Next steps</span></span>
- <span data-ttu-id="877d0-170">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="877d0-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
