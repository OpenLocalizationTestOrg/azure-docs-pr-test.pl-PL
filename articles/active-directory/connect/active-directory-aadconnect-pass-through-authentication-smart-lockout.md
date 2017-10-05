---
title: 'Azure AD Connect: Uwierzytelniania przekazywanego - blokady inteligentnej | Dokumentacja firmy Microsoft'
description: "W tym artykule opisano sposób ochrony sieci lokalnych kont usługi Azure Active Directory (Azure AD) przekazywanego uwierzytelniania przed atakami siłowymi haseł w chmurze."
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
ms.openlocfilehash: c84b2406e6373701c83c509342129bd6d7d4034b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="b476a-104">Uwierzytelniania przekazywanego usługi Azure Active Directory: Blokady inteligentnej</span><span class="sxs-lookup"><span data-stu-id="b476a-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="b476a-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b476a-105">Overview</span></span>

<span data-ttu-id="b476a-106">Usługi Azure AD chroni przed atakami siłowymi hasła i uniemożliwia użytkownikom oryginalnego blokowanie poza ich usługi Office 365 i aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b476a-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="b476a-107">Ta funkcja o nazwie **blokady inteligentnej**, jest obsługiwana w przypadku korzystania z uwierzytelniania przekazywanego jako metodę logowania.</span><span class="sxs-lookup"><span data-stu-id="b476a-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="b476a-108">Blokady inteligentnej jest domyślnie włączona dla wszystkich dzierżawców i kont użytkowników, są chronione przez cały czas; nie istnieje potrzeba aby ją włączyć.</span><span class="sxs-lookup"><span data-stu-id="b476a-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all the time; there is no need to turn it on.</span></span>

<span data-ttu-id="b476a-109">Blokady inteligentnej działa przez śledzenie nieudanych prób logowania i po pewnym **próg blokady**, rozpoczynając **czas trwania blokady**.</span><span class="sxs-lookup"><span data-stu-id="b476a-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="b476a-110">Wszelkich prób logowania z osoba atakująca czas trwania blokady są odrzucane.</span><span class="sxs-lookup"><span data-stu-id="b476a-110">Any sign-in attempts from the attacker during the Lockout Duration are rejected.</span></span> <span data-ttu-id="b476a-111">Jeśli ataku, kolejnych nieudanych prób zalogowania po zakończeniu czas trwania blokady wynik w dłuższym czasie trwania blokady.</span><span class="sxs-lookup"><span data-stu-id="b476a-111">If the attack continues, the subsequent failed sign-in attempts after the Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="b476a-112">Domyślna wartość progowa blokady to 10 nieudanych prób, a domyślny czas trwania blokady wynosi 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="b476a-112">The default Lockout Threshold is 10 failed attempts, and the default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="b476a-113">Blokady inteligentnej rozróżnia również logowania z oryginalnego użytkowników i osoby atakujące i tylko blokowane osoby atakujące w większości przypadków.</span><span class="sxs-lookup"><span data-stu-id="b476a-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out the attackers in most cases.</span></span> <span data-ttu-id="b476a-114">Ta funkcja zapobiega osoby atakujące złośliwie zablokowania oryginalnego użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b476a-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="b476a-115">Firma Microsoft umożliwia zachowanie logowania, urządzenia użytkowników & przeglądarek i innymi sygnałami odróżnia oryginalnego użytkownika, osoby atakujące.</span><span class="sxs-lookup"><span data-stu-id="b476a-115">We use past sign-in behavior, users’ devices & browsers and other signals to distinguish between genuine users and attackers.</span></span> <span data-ttu-id="b476a-116">Firma Microsoft stale umożliwiają zwiększenie nasze algorytmy.</span><span class="sxs-lookup"><span data-stu-id="b476a-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="b476a-117">Ponieważ uwierzytelniania przekazywanego przekazuje żądania weryfikacji haseł na lokalnej usługi Active Directory (AD), należy uniemożliwić osobom atakującym blokowania kont usługi AD użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b476a-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need to prevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="b476a-118">Ponieważ masz zasad blokady konta AD (w szczególności [ **próg blokady konta** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) i [ **Zresetuj licznik blokady konta po zasady**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), należy skonfigurować progu blokady konta usługi Azure AD i wartości czasu trwania blokady odpowiednio do ataków w chmurze przed dotarciem lokalnej usługi AD.</span><span class="sxs-lookup"><span data-stu-id="b476a-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need to configure Azure AD’s Lockout Threshold and Lockout Duration values appropriately to filter out attacks in the cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="b476a-119">Funkcji blokady inteligentnej jest wolny i jest _na_ domyślnie dla wszystkich klientów.</span><span class="sxs-lookup"><span data-stu-id="b476a-119">The Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="b476a-120">Modyfikowanie progu blokady konta usługi Azure AD i czas trwania blokady wartości przy użyciu interfejsu API programu Graph musi jednak dzierżawy mają co najmniej jedną licencję usługi Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="b476a-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant to have at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="b476a-121">Nie wymagają licencji usługi Azure AD Premium P2 _dla każdego użytkownika_ uzyskanie funkcji blokady inteligentnej przy użyciu uwierzytelniania przekazywanego.</span><span class="sxs-lookup"><span data-stu-id="b476a-121">You don't need an Azure AD Premium P2 license _per user_ to get the Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="b476a-122">Aby upewnić się, że użytkowników lokalnych kont usługi AD są również chronione, należy upewnić się, że:</span><span class="sxs-lookup"><span data-stu-id="b476a-122">To ensure that your users’ on-premises AD accounts are well protected, you need to ensure that:</span></span>

1.  <span data-ttu-id="b476a-123">Progu blokady konta usługi Azure AD jest _mniej_ niż próg blokady konta przez usługi AD.</span><span class="sxs-lookup"><span data-stu-id="b476a-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="b476a-124">Firma Microsoft zaleca, ustaw wartości, tak aby próg blokady konta przez usługi AD jest co najmniej dwie lub trzy razy progu blokady konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b476a-124">We recommend that you set the values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="b476a-125">Czas trwania blokady usługi Azure AD (reprezentowane w sekundach) jest _dłużej_ niż Directory resetowania konta blokady licznika po (reprezentowane w minutach).</span><span class="sxs-lookup"><span data-stu-id="b476a-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="b476a-126">Sprawdź zasad blokady konta usługi AD</span><span class="sxs-lookup"><span data-stu-id="b476a-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="b476a-127">Użyj poniższych instrukcji, aby sprawdzić zasad blokady konta usługi AD:</span><span class="sxs-lookup"><span data-stu-id="b476a-127">Use the following instructions to verify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="b476a-128">Otwórz narzędzie Zarządzanie zasadami grupy.</span><span class="sxs-lookup"><span data-stu-id="b476a-128">Open the Group Policy Management tool.</span></span>
2.  <span data-ttu-id="b476a-129">Edytowanie zasad grupy, która jest stosowana do wszystkich użytkowników, na przykład domyślnych zasad domeny.</span><span class="sxs-lookup"><span data-stu-id="b476a-129">Edit the group policy that is applied to all users, for example, the Default Domain Policy.</span></span>
3.  <span data-ttu-id="b476a-130">Przejdź do zasady blokowania komputera Konfiguracja komputera\Zasady\Ustawienia systemu Windows\Ustawienia zabezpieczeń\Zasady konta\Zasady.</span><span class="sxs-lookup"><span data-stu-id="b476a-130">Navigate to Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="b476a-131">Sprawdź wartości progu blokady konta i zresetuj licznik blokady konta po.</span><span class="sxs-lookup"><span data-stu-id="b476a-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![Zasady blokowania kont usługi AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-the-graph-api-to-manage-your-tenants-smart-lockout-values"></a><span data-ttu-id="b476a-133">Umożliwia zarządzanie wartości blokady inteligentnej Twojej dzierżawy interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="b476a-133">Use the Graph API to manage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="b476a-134">Modyfikowanie progu blokady konta i czas trwania blokady wartości przy użyciu interfejsu API programu Graph usługi Azure AD to funkcja usługi Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="b476a-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="b476a-135">Również potrzebuje użytkownik musi być administratorem globalnym w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="b476a-135">It also needs you to be a Global Administrator on your tenant.</span></span>

<span data-ttu-id="b476a-136">Można użyć [Explorer wykres](https://developer.microsoft.com/graph/graph-explorer) mogą odczytywać, wartość i Aktualizuj wartości blokady inteligentnej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b476a-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to read, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="b476a-137">Jednak możesz również wykonać te operacje programowo.</span><span class="sxs-lookup"><span data-stu-id="b476a-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="b476a-138">Inteligentne blokady odczytu wartości</span><span class="sxs-lookup"><span data-stu-id="b476a-138">Read Smart Lockout values</span></span>

<span data-ttu-id="b476a-139">Wykonaj następujące kroki, które można odczytać wartości blokady inteligentnej Twojej dzierżawy:</span><span class="sxs-lookup"><span data-stu-id="b476a-139">Follow these steps to read your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="b476a-140">Zaloguj się do Eksploratora wykresu jako Administrator globalny dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="b476a-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="b476a-141">Jeśli zostanie wyświetlony monit, należy udzielić dostępu do żądanych uprawnień.</span><span class="sxs-lookup"><span data-stu-id="b476a-141">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="b476a-142">Kliknij polecenie "Modyfikuj uprawnienia" i wybierz uprawnienie "Directory.ReadWrite.All".</span><span class="sxs-lookup"><span data-stu-id="b476a-142">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="b476a-143">Skonfiguruj żądania interfejsu API programu Graph w następujący sposób: Ustaw wersję "BETA", typ żądania "GET" i adresu URL do `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="b476a-143">Configure the Graph API request as follows: Set version to “BETA”, request type to “GET” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="b476a-144">Kliknij przycisk "Uruchom zapytanie", aby zobaczyć wartości blokady inteligentnej swojej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="b476a-144">Click "Run Query" to see your tenant's Smart Lockout values.</span></span> <span data-ttu-id="b476a-145">Jeśli nie zdefiniowano wartości Twojej dzierżawy przed, pojawi się pusty zestaw.</span><span class="sxs-lookup"><span data-stu-id="b476a-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="b476a-146">Ustaw wartości inteligentne blokady</span><span class="sxs-lookup"><span data-stu-id="b476a-146">Set Smart Lockout values</span></span>

<span data-ttu-id="b476a-147">Wykonaj następujące kroki, aby ustawić wartości blokady inteligentnej Twojej dzierżawy (po raz pierwszy tylko):</span><span class="sxs-lookup"><span data-stu-id="b476a-147">Follow these steps to set your tenant’s Smart Lockout values (for the first time only):</span></span>

1. <span data-ttu-id="b476a-148">Zaloguj się do Eksploratora wykresu jako Administrator globalny dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="b476a-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="b476a-149">Jeśli zostanie wyświetlony monit, należy udzielić dostępu do żądanych uprawnień.</span><span class="sxs-lookup"><span data-stu-id="b476a-149">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="b476a-150">Kliknij polecenie "Modyfikuj uprawnienia" i wybierz uprawnienie "Directory.ReadWrite.All".</span><span class="sxs-lookup"><span data-stu-id="b476a-150">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="b476a-151">Skonfiguruj żądania interfejsu API programu Graph w następujący sposób: Ustaw wersję do wersji "BETA", typ "POST" i adres URL żądania `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="b476a-151">Configure the Graph API request as follows: Set version to “BETA”, request type to “POST” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="b476a-152">Skopiuj i wklej następujący żądania JSON w polu "Treści żądania".</span><span class="sxs-lookup"><span data-stu-id="b476a-152">Copy and paste the following JSON request into the "Request Body" field.</span></span> <span data-ttu-id="b476a-153">Zmień wartości blokady inteligentnej zgodnie z potrzebami i użyj losowy identyfikator GUID dla `templateId`.</span><span class="sxs-lookup"><span data-stu-id="b476a-153">Change the Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="b476a-154">Kliknij przycisk "Uruchom zapytania" można ustawić wartości blokady inteligentnej swojej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="b476a-154">Click "Run Query" to set your tenant's Smart Lockout values.</span></span>

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
><span data-ttu-id="b476a-155">Jeśli nie są używane, można pozostawić **BannedPasswordList** i **EnableBannedPasswordCheck** wartości jako pusty ("") i "false" odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="b476a-155">If you are not using them, you can leave the **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="b476a-156">Sprawdź, czy ma ustawiony prawidłowo przy użyciu wartości blokady inteligentnej Twojej dzierżawy [te kroki](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="b476a-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="b476a-157">Aby zaktualizować inteligentne blokady</span><span class="sxs-lookup"><span data-stu-id="b476a-157">Update Smart Lockout values</span></span>

<span data-ttu-id="b476a-158">Wykonaj następujące kroki, aby zaktualizować wartości blokady inteligentnej Twojej dzierżawy (jeśli zostały skonfigurowane je przed):</span><span class="sxs-lookup"><span data-stu-id="b476a-158">Follow these steps to update your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="b476a-159">Zaloguj się do Eksploratora wykresu jako Administrator globalny dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="b476a-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="b476a-160">Jeśli zostanie wyświetlony monit, należy udzielić dostępu do żądanych uprawnień.</span><span class="sxs-lookup"><span data-stu-id="b476a-160">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="b476a-161">Kliknij polecenie "Modyfikuj uprawnienia" i wybierz uprawnienie "Directory.ReadWrite.All".</span><span class="sxs-lookup"><span data-stu-id="b476a-161">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="b476a-162">[Wykonaj następujące kroki, które można odczytać wartości blokady inteligentnej Twojej dzierżawy](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="b476a-162">[Follow these steps to read your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="b476a-163">Kopiuj `id` wartość (GUID) elementu o nazwie "wyświetlanej" jako "PasswordRuleSettings".</span><span class="sxs-lookup"><span data-stu-id="b476a-163">Copy the `id` value (a GUID) of the item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="b476a-164">Skonfiguruj żądania interfejsu API programu Graph w następujący sposób: Ustaw wersję "BETA", typ żądania "Poprawka" i adresu URL do `https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -Użyj identyfikatora GUID z kroku 3 dla `<id>`.</span><span class="sxs-lookup"><span data-stu-id="b476a-164">Configure the Graph API request as follows: Set version to “BETA”, request type to “PATCH” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use the GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="b476a-165">Skopiuj i wklej następujący żądania JSON w polu "Treści żądania".</span><span class="sxs-lookup"><span data-stu-id="b476a-165">Copy and paste the following JSON request into the "Request Body" field.</span></span> <span data-ttu-id="b476a-166">Zmień wartości blokady inteligentnej zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="b476a-166">Change the Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="b476a-167">Kliknij przycisk "Uruchom zapytania", aby zaktualizować wartości blokady inteligentnej swojej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="b476a-167">Click "Run Query" to update your tenant's Smart Lockout values.</span></span>

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

<span data-ttu-id="b476a-168">Sprawdź zaktualizowano poprawnie przy użyciu wartości blokady inteligentnej Twojej dzierżawy [te kroki](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="b476a-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b476a-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b476a-169">Next steps</span></span>
- <span data-ttu-id="b476a-170">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="b476a-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
