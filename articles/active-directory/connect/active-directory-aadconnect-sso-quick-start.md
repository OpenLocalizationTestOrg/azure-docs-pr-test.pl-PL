---
title: "Azure AD Connect: Bezproblemowe logowanie jednokrotne — Szybki Start | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak rozpocząć pracę z usługi Azure Active Directory bezproblemowe logowanie jednokrotne."
services: active-directory
keywords: "Co to jest usługa Azure AD Connect, zainstaluj usługę Active Directory, wymaganych składników dla usługi Azure AD, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 977108687734a5eb7f7a30419de2a6bdef184d0e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="fef23-104">Azure Active Directory bezproblemowe logowanie jednokrotne: Szybki start</span><span class="sxs-lookup"><span data-stu-id="fef23-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-to-deploy-seamless-sso"></a><span data-ttu-id="fef23-105">Jak wdrożyć bezproblemowe logowanie Jednokrotne</span><span class="sxs-lookup"><span data-stu-id="fef23-105">How to deploy Seamless SSO</span></span>

<span data-ttu-id="fef23-106">Azure Active Directory bezproblemowe logowanie jednokrotne (Azure AD bezproblemowe logowanie Jednokrotne) automatycznie podpisuje użytkowników, gdy są na komputerach stacjonarnych firmowej podłączone do sieci firmowej.</span><span class="sxs-lookup"><span data-stu-id="fef23-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected to your corporate network.</span></span> <span data-ttu-id="fef23-107">Umożliwia użytkownikom łatwy dostęp do aplikacji opartej na chmurze bez konieczności żadnych składników dodatkowych lokalnych.</span><span class="sxs-lookup"><span data-stu-id="fef23-107">It provides your users easy access to your cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="fef23-108">Funkcja logowania jednokrotnego bezproblemowe jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="fef23-108">The Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="fef23-109">Aby wdrożyć bezproblemowe logowania jednokrotnego, musisz wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fef23-109">To deploy Seamless SSO, you need to follow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="fef23-110">Krok 1: Sprawdź wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fef23-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="fef23-111">Upewnij się, że zostały spełnione następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="fef23-111">Ensure that the following prerequisites are in place:</span></span>

1. <span data-ttu-id="fef23-112">Konfigurowanie serwera usługi Azure AD Connect: Jeśli używasz [uwierzytelniania przekazywanego](active-directory-aadconnect-pass-through-authentication.md) jako metody logowania, są wymagane żadne dalsze akcje.</span><span class="sxs-lookup"><span data-stu-id="fef23-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="fef23-113">Jeśli używasz [synchronizacji skrótu hasła](active-directory-aadconnectsync-implement-password-synchronization.md) jako metody logowania, a w przypadku zapory między Azure AD Connect i Azure AD, upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="fef23-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="fef23-114">W przypadku korzystania z wersji 1.1.484.0 lub nowszej programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="fef23-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="fef23-115">Azure AD Connect może komunikować się z `*.msappproxy.net` adresy URL i przez port 443.</span><span class="sxs-lookup"><span data-stu-id="fef23-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="fef23-116">To wymaganie wstępne dotyczy tylko po włączeniu funkcji, nie do rzeczywistego użytkownika logowania.</span><span class="sxs-lookup"><span data-stu-id="fef23-116">This prerequisite is applicable only when you enable the feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="fef23-117">Azure AD Connect można nawiązywać połączenia IP bezpośrednio z [zakresy IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="fef23-117">Azure AD Connect can make direct IP connections to the [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="fef23-118">Ponownie te wymagania wstępne ma zastosowanie tylko wtedy, gdy zostanie włączona funkcja.</span><span class="sxs-lookup"><span data-stu-id="fef23-118">Again, this prerequisite is applicable only when you enable the feature.</span></span>
2. <span data-ttu-id="fef23-119">Dla każdego lasu usługi AD, synchronizacji z usługą Azure AD (za pomocą usługi Azure AD Connect) i dla użytkowników, których chcesz włączyć bezproblemowe logowanie Jednokrotne potrzebne są poświadczenia administratora domeny.</span><span class="sxs-lookup"><span data-stu-id="fef23-119">You need Domain Administrator credentials for each AD forest that you synchronize to Azure AD (using Azure AD Connect) and for whose users you want to enable Seamless SSO.</span></span>

## <a name="step-2-enable-the-feature"></a><span data-ttu-id="fef23-120">Krok 2: Włączanie funkcji</span><span class="sxs-lookup"><span data-stu-id="fef23-120">Step 2: Enable the feature</span></span>

<span data-ttu-id="fef23-121">Bezproblemowe logowanie Jednokrotne można włączyć za pomocą [Azure AD Connect](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="fef23-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="fef23-122">Jeśli przeprowadzasz nową instalację programu Azure AD Connect, wybierz [niestandardową ścieżkę](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="fef23-122">If you are doing a fresh installation of Azure AD Connect, choose the [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="fef23-123">Na stronie "Logowanie użytkowników" zaznacz opcję "Włącz pojedynczy znak".</span><span class="sxs-lookup"><span data-stu-id="fef23-123">At the "User sign-in" page, check the "Enable single sign on" option.</span></span>

![Azure AD Connect - logowanie użytkowników](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="fef23-125">Jeśli masz już zainstalowany program Azure AD Connect, wybierz polecenie "Zmień użytkownika strony logowania" w Azure AD Connect, a następnie kliknij przycisk "Dalej".</span><span class="sxs-lookup"><span data-stu-id="fef23-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="fef23-126">Następnie zaznacz opcję "Włącz pojedynczy znak".</span><span class="sxs-lookup"><span data-stu-id="fef23-126">Then check the "Enable single sign on" option.</span></span>

![Azure AD Connect - zmiany logowania użytkownika](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="fef23-128">Kontynuuj pracę z kreatorem, aż do strony "Włącz pojedynczy znak".</span><span class="sxs-lookup"><span data-stu-id="fef23-128">Continue through the wizard until you get to the "Enable single sign on" page.</span></span> <span data-ttu-id="fef23-129">Podaj poświadczenia administratora domeny dla każdego lasu usługi AD, synchronizacji z usługą Azure AD (za pomocą usługi Azure AD Connect) i dla użytkowników, których chcesz włączyć bezproblemowe logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="fef23-129">Provide Domain Administrator credentials for each AD forest that you synchronize to Azure AD (using Azure AD Connect) and for whose users you want to enable Seamless SSO.</span></span> 

<span data-ttu-id="fef23-130">Po zakończeniu działania kreatora bezproblemowe rejestracji Jednokrotnej jest włączona na dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="fef23-130">After completion of the wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="fef23-131">Poświadczenia administratora domeny nie są przechowywane w programie Azure AD Connect lub w usłudze Azure AD, ale tylko służą do włączenia tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="fef23-131">The Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used to enable the feature.</span></span>

<span data-ttu-id="fef23-132">Wykonaj te instrukcje, aby sprawdzić prawidłowo włączone bezproblemowe rejestracji Jednokrotnej:</span><span class="sxs-lookup"><span data-stu-id="fef23-132">Follow these instructions to verify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="fef23-133">Zaloguj się do [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) przy użyciu poświadczeń administratora globalnego dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="fef23-133">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with the Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="fef23-134">Wybierz **usługi Azure Active Directory** w nawigacji po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fef23-134">Select **Azure Active Directory** on the left-hand navigation.</span></span>
3. <span data-ttu-id="fef23-135">Wybierz **programu Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="fef23-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="fef23-136">Sprawdź, czy **bezproblemowe logowanie jednokrotne** funkcji jest pokazywana jako **włączone**.</span><span class="sxs-lookup"><span data-stu-id="fef23-136">Verify that the **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Portal Azure — blok Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-the-feature"></a><span data-ttu-id="fef23-138">Krok 3: Wdrażanie funkcji</span><span class="sxs-lookup"><span data-stu-id="fef23-138">Step 3: Roll out the feature</span></span>

<span data-ttu-id="fef23-139">Aby wdrożyć funkcję dla użytkowników, należy dodać adresów URL usługi Azure AD (https://autologon.microsoftazuread-sso.com i https://aadg.windows.net.nsatc.net) do ustawień intranetowej strefy użytkowników przy użyciu zasad grupy w usłudze Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fef23-139">To roll out the feature to your users, you need to add two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) to users' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="fef23-140">Poniższe instrukcje prawidłowe tylko dla programu Internet Explorer i Google Chrome w systemie Windows (Jeśli zestaw adresów URL zaufanych witryn współużytkuje z programu Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="fef23-140">The following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="fef23-141">Przeczytaj następnej sekcji, aby uzyskać instrukcje dotyczące konfigurowania Mozilla Firefox i Google Chrome na komputerach Mac.</span><span class="sxs-lookup"><span data-stu-id="fef23-141">Read the next section for instructions to set up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-to-modify-users-intranet-zone-settings"></a><span data-ttu-id="fef23-142">Dlaczego należy zmodyfikować ustawienia strefy Intranet użytkowników?</span><span class="sxs-lookup"><span data-stu-id="fef23-142">Why do you need to modify users' Intranet zone settings?</span></span>

<span data-ttu-id="fef23-143">Domyślnie przeglądarka automatycznie oblicza prawo strefy (w Internecie lub intranecie) z adresu URL.</span><span class="sxs-lookup"><span data-stu-id="fef23-143">By default, the browser automatically calculates the right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="fef23-144">Na przykład http://contoso/ jest mapowany do strefy Intranet, podczas gdy http://intranet.contoso.com/ jest mapowany na strefie Internet (ponieważ adres URL zawiera kropkę).</span><span class="sxs-lookup"><span data-stu-id="fef23-144">For example, http://contoso/ is mapped to the Intranet zone, whereas http://intranet.contoso.com/ is mapped to the Internet zone (because the URL contains a period).</span></span> <span data-ttu-id="fef23-145">Przeglądarki nie wysyłaj biletów Kerberos do punktu końcowego w chmurze — takich jak Azure adresów URL AD - chyba, że adres URL jest w sposób jawny dodane do strefy Intranet w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="fef23-145">Browsers don't send Kerberos tickets to a cloud endpoint - like the two Azure AD URLs - unless its URL is explicitly added to the browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="fef23-146">Szczegółowe procedury</span><span class="sxs-lookup"><span data-stu-id="fef23-146">Detailed steps</span></span>

1. <span data-ttu-id="fef23-147">Otwórz narzędzie Zarządzanie zasadami grupy.</span><span class="sxs-lookup"><span data-stu-id="fef23-147">Open the Group Policy Management tool.</span></span>
2. <span data-ttu-id="fef23-148">Edytowanie zasad grupy, która jest stosowana do niektórych lub wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="fef23-148">Edit the Group Policy that is applied to some or all your users.</span></span> <span data-ttu-id="fef23-149">W tym przykładzie używamy **domyślne zasady domeny**.</span><span class="sxs-lookup"><span data-stu-id="fef23-149">In this example, we use the **Default Domain Policy**.</span></span>
3. <span data-ttu-id="fef23-150">Przejdź do **strony Panel\Security formantu użytkownika Konfiguracja komputera\Szablony administracyjne\Składniki systemu Windows\Internet Explorer\Internetowy** i wybierz **witrynę do strefy przypisania listy**.</span><span class="sxs-lookup"><span data-stu-id="fef23-150">Navigate to **User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site to Zone Assignment List**.</span></span>
<span data-ttu-id="fef23-151">![Logowanie jednokrotne](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="fef23-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="fef23-152">Włącz zasady, a następnie wprowadź następujące wartości (gdzie bilety Kerberos są przekazywane URL usługi Azure AD) i danych (*1* wskazuje strefy Intranet) w oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="fef23-152">Enable the policy, and enter the following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in the dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="fef23-153">Jeśli chcesz uniemożliwić użytkownikom niektóre przy użyciu logowania jednokrotnego bezproblemowe — na przykład, jeśli ci użytkownicy są logują się na udostępnionym kioski — ustawioną poprzednimi wartościami *4*.</span><span class="sxs-lookup"><span data-stu-id="fef23-153">If you want to disallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set the preceding values to *4*.</span></span> <span data-ttu-id="fef23-154">Ta akcja dodaje adresy URL usługi Azure AD do strefy witryny z ograniczeniami, a nie powiedzie się bezproblemowe logowanie Jednokrotne cały czas.</span><span class="sxs-lookup"><span data-stu-id="fef23-154">This action adds the Azure AD URLs to the Restricted Zone, and fails Seamless SSO all the time.</span></span>

5. <span data-ttu-id="fef23-155">Kliknij przycisk **OK** i **OK** ponownie.</span><span class="sxs-lookup"><span data-stu-id="fef23-155">Click **OK** and **OK** again.</span></span>

![Logowanie jednokrotne](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="fef23-157">Zagadnienia dotyczące przeglądarki</span><span class="sxs-lookup"><span data-stu-id="fef23-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="fef23-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="fef23-158">Mozilla Firefox</span></span>

<span data-ttu-id="fef23-159">Mozilla Firefox nie automatycznie wykonuje uwierzytelnianie Kerberos.</span><span class="sxs-lookup"><span data-stu-id="fef23-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="fef23-160">Każdy użytkownik będzie musiał ręcznie dodać adresy URL usługi Azure AD do ich ustawień przeglądarki Firefox, wykonując następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fef23-160">Each user has to manually add the Azure AD URLs to their Firefox settings using the following steps:</span></span>
1. <span data-ttu-id="fef23-161">Uruchom program Firefox, a następnie wprowadź `about:config` na pasku adresu.</span><span class="sxs-lookup"><span data-stu-id="fef23-161">Run Firefox and enter `about:config` in the address bar.</span></span> <span data-ttu-id="fef23-162">Odrzucić żadnych powiadomień, które są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="fef23-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="fef23-163">Wyszukaj **network.negotiate-auth.trusted URI** preferencji.</span><span class="sxs-lookup"><span data-stu-id="fef23-163">Search for the **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="fef23-164">Ta opcja wyświetla listę zaufanych witryn w programie Firefox uwierzytelniania Kerberos.</span><span class="sxs-lookup"><span data-stu-id="fef23-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="fef23-165">Kliknij prawym przyciskiem myszy i wybierz polecenie "Modyfikuj".</span><span class="sxs-lookup"><span data-stu-id="fef23-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="fef23-166">Wprowadź "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" w tym polu.</span><span class="sxs-lookup"><span data-stu-id="fef23-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in the field.</span></span>
5. <span data-ttu-id="fef23-167">Kliknij przycisk "OK" i ponownie otwórz przeglądarkę.</span><span class="sxs-lookup"><span data-stu-id="fef23-167">Click "OK" and reopen the browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="fef23-168">Przeglądarka Safari w systemie Mac OS</span><span class="sxs-lookup"><span data-stu-id="fef23-168">Safari on Mac OS</span></span>

<span data-ttu-id="fef23-169">Upewnij się, że maszynę z systemem Mac OS jest przyłączony do usługi AD.</span><span class="sxs-lookup"><span data-stu-id="fef23-169">Ensure that the machine running Mac OS is joined to AD.</span></span> <span data-ttu-id="fef23-170">Zobacz instrukcje na temat w tym [tutaj](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span><span class="sxs-lookup"><span data-stu-id="fef23-170">See instructions on how to do that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="fef23-171">Google Chrome w systemie Mac OS</span><span class="sxs-lookup"><span data-stu-id="fef23-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="fef23-172">Google Chrome na innych platform z systemem innym niż Windows i Mac OS, można znaleźć w temacie [w tym artykule](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) informacji na temat dozwolonych programu Azure AD adresy URL zintegrowane uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="fef23-172">For Google Chrome on Mac OS and other non-Windows platforms, refer to [this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how to whitelist the Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="fef23-173">Wdrażanie usługi Azure AD adresy URL Firefox i Google Chrome na użytkowników komputerów Mac za pomocą rozszerzenia innych firm zasad grupy usługi Active Directory jest poza zakres tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="fef23-173">Using third-party Active Directory Group Policy extensions to roll out the Azure AD URLs to Firefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="fef23-174">Znane ograniczenia</span><span class="sxs-lookup"><span data-stu-id="fef23-174">Known limitations</span></span>

<span data-ttu-id="fef23-175">Bezproblemowe logowanie Jednokrotne nie działa w trybie prywatnym przeglądania na przeglądarki Firefox i krawędzi.</span><span class="sxs-lookup"><span data-stu-id="fef23-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="fef23-176">Również nie działa w programie Internet Explorer Jeśli przeglądarka jest uruchomiony w trybie ochrona rozszerzona.</span><span class="sxs-lookup"><span data-stu-id="fef23-176">It also doesn't work on Internet Explorer if the browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="fef23-177">Firma Microsoft niedawno wycofane obsługę krawędzi do badania problemów zgłoszonych przez klientów.</span><span class="sxs-lookup"><span data-stu-id="fef23-177">We recently rolled back support for Edge to investigate customer-reported issues.</span></span>

## <a name="step-4-test-the-feature"></a><span data-ttu-id="fef23-178">Krok 4: Testowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="fef23-178">Step 4: Test the feature</span></span>

<span data-ttu-id="fef23-179">Aby przetestować tę funkcję dla określonego użytkownika, upewnij się, że _wszystkie_ są spełnione następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="fef23-179">To test the feature for a specific user, ensure that _all_ the following conditions are in place:</span></span>
  - <span data-ttu-id="fef23-180">Użytkownik loguje się na urządzeniach firmowych.</span><span class="sxs-lookup"><span data-stu-id="fef23-180">The user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="fef23-181">Urządzenia został wcześniej przyłączony do domeny usługi Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="fef23-181">The device has been previously joined to your Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="fef23-182">Urządzenie korzysta z bezpośredniego połączenia do Twojej domeny kontrolera (DC), w firmowej sieci przewodowej lub bezprzewodowej lub za pośrednictwem połączenia dostępu zdalnego, takich jak połączenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="fef23-182">The device has a direct connection to your Domain Controller (DC), either on the corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="fef23-183">Masz [wprowadzanie funkcję](##step-3-roll-out-the-feature) do tego użytkownika za pomocą zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="fef23-183">You have [rolled out the feature](##step-3-roll-out-the-feature) to this user using Group Policy.</span></span>

<span data-ttu-id="fef23-184">Do przetestowania tego scenariusza, w którym użytkownik musi wprowadzić tylko nazwę użytkownika, ale nie hasło:</span><span class="sxs-lookup"><span data-stu-id="fef23-184">To test the scenario where the user enters only the username, but not the password:</span></span>
- <span data-ttu-id="fef23-185">Zaloguj się do *https://myapps.microsoft.com/* w nowej sesji przeglądarki prywatnych.</span><span class="sxs-lookup"><span data-stu-id="fef23-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="fef23-186">Do przetestowania tego scenariusza, w którym użytkownik nie musi wprowadzić nazwę użytkownika lub hasło:</span><span class="sxs-lookup"><span data-stu-id="fef23-186">To test the scenario where the user doesn't have to enter the username or the password:</span></span> 
- <span data-ttu-id="fef23-187">Zaloguj się do *https://myapps.microsoft.com/contoso.onmicrosoft.com* w nowej sesji przeglądarki prywatnych.</span><span class="sxs-lookup"><span data-stu-id="fef23-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="fef23-188">Zastąp "*contoso*" nazwą swojej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="fef23-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="fef23-189">Lub zaloguj się do *https://myapps.microsoft.com/contoso.com* w nowej sesji przeglądarki prywatnych.</span><span class="sxs-lookup"><span data-stu-id="fef23-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="fef23-190">Zastąp "*contoso.com*" z zweryfikowanej domeny (nie domeny federacyjnej) w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="fef23-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="fef23-191">Krok 5: Przerzucane kluczy</span><span class="sxs-lookup"><span data-stu-id="fef23-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="fef23-192">W kroku 2 Azure AD Connect tworzy konta komputerów (reprezentujący usługi Azure AD) we wszystkich lasach AD, na których włączono bezproblemowe logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="fef23-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all the AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="fef23-193">Dowiedz się więcej szczegółów w [tutaj](active-directory-aadconnect-sso-how-it-works.md).</span><span class="sxs-lookup"><span data-stu-id="fef23-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="fef23-194">Ze względów bezpieczeństwa zaleca się, że często wdrożysz za pośrednictwem protokołu Kerberos kluczy odszyfrowywania tych kont komputerów.</span><span class="sxs-lookup"><span data-stu-id="fef23-194">For improved security, it is recommended that  you frequently roll over the Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="fef23-195">Nie trzeba wykonać ten krok _natychmiast_ po włączeniu funkcji.</span><span class="sxs-lookup"><span data-stu-id="fef23-195">You don't need to do this step _immediately_ after you have enabled the feature.</span></span> <span data-ttu-id="fef23-196">Przerzuć klucze Kerberos odszyfrowywania co najmniej 30 dni.</span><span class="sxs-lookup"><span data-stu-id="fef23-196">Roll over the Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fef23-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fef23-197">Next steps</span></span>

- <span data-ttu-id="fef23-198">[**Nowości techniczne** ](active-directory-aadconnect-sso-how-it-works.md) -zrozumieć sposób działania tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="fef23-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="fef23-199">[**Często zadawane pytania** ](active-directory-aadconnect-sso-faq.md) — odpowiedzi na często zadawane pytania.</span><span class="sxs-lookup"><span data-stu-id="fef23-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="fef23-200">[**Rozwiązywanie problemów z** ](active-directory-aadconnect-troubleshoot-sso.md) — Dowiedz się, jak rozwiązać typowe problemy z funkcją.</span><span class="sxs-lookup"><span data-stu-id="fef23-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="fef23-201">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="fef23-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
