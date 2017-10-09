---
title: "Azure AD Connect: Bezproblemowe logowanie jednokrotne — Szybki Start | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób uruchamiania tooget z usługi Azure Active Directory bezproblemowe logowanie jednokrotne."
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
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="877ee-104">Azure Active Directory bezproblemowe logowanie jednokrotne: Szybki start</span><span class="sxs-lookup"><span data-stu-id="877ee-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-toodeploy-seamless-sso"></a><span data-ttu-id="877ee-105">Jak toodeploy bezproblemowe logowanie Jednokrotne</span><span class="sxs-lookup"><span data-stu-id="877ee-105">How toodeploy Seamless SSO</span></span>

<span data-ttu-id="877ee-106">Azure Active Directory bezproblemowe logowanie jednokrotne (Azure AD bezproblemowe logowanie Jednokrotne) automatycznie podpisuje użytkowników, gdy są w sieci firmowej tooyour połączonych komputerów firmowych.</span><span class="sxs-lookup"><span data-stu-id="877ee-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected tooyour corporate network.</span></span> <span data-ttu-id="877ee-107">Umożliwia użytkownikom łatwe tooyour aplikacji działających w chmurze bez konieczności żadnych składników dodatkowych lokalnych.</span><span class="sxs-lookup"><span data-stu-id="877ee-107">It provides your users easy access tooyour cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="877ee-108">funkcja logowania jednokrotnego bezproblemowe Hello jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="877ee-108">hello Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="877ee-109">toodeploy bezproblemowe logowanie Jednokrotne, należy toofollow następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="877ee-109">toodeploy Seamless SSO, you need toofollow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="877ee-110">Krok 1: Sprawdź wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="877ee-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="877ee-111">Upewnij się, że hello następujące wymagania wstępne zostały spełnione:</span><span class="sxs-lookup"><span data-stu-id="877ee-111">Ensure that hello following prerequisites are in place:</span></span>

1. <span data-ttu-id="877ee-112">Konfigurowanie serwera usługi Azure AD Connect: Jeśli używasz [uwierzytelniania przekazywanego](active-directory-aadconnect-pass-through-authentication.md) jako metody logowania, są wymagane żadne dalsze akcje.</span><span class="sxs-lookup"><span data-stu-id="877ee-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="877ee-113">Jeśli używasz [synchronizacji skrótu hasła](active-directory-aadconnectsync-implement-password-synchronization.md) jako metody logowania, a w przypadku zapory między Azure AD Connect i Azure AD, upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="877ee-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="877ee-114">W przypadku korzystania z wersji 1.1.484.0 lub nowszej programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="877ee-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="877ee-115">Azure AD Connect może komunikować się z `*.msappproxy.net` adresy URL i przez port 443.</span><span class="sxs-lookup"><span data-stu-id="877ee-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="877ee-116">To wymaganie wstępne dotyczy tylko po włączeniu funkcji hello nie do rzeczywistego użytkownika logowania.</span><span class="sxs-lookup"><span data-stu-id="877ee-116">This prerequisite is applicable only when you enable hello feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="877ee-117">Azure AD Connect można wprowadzać bezpośredniego toohello połączeń IP [zakresy IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="877ee-117">Azure AD Connect can make direct IP connections toohello [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="877ee-118">Ponownie te wymagania wstępne ma zastosowanie tylko wtedy, gdy zostanie włączona funkcja hello.</span><span class="sxs-lookup"><span data-stu-id="877ee-118">Again, this prerequisite is applicable only when you enable hello feature.</span></span>
2. <span data-ttu-id="877ee-119">Potrzebne są poświadczenia administratora domeny dla każdego lasu usługi AD, aby synchronizować tooAzure AD (za pomocą usługi Azure AD Connect) oraz dla użytkowników, którzy mają tooenable bezproblemowe logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="877ee-119">You need Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span>

## <a name="step-2-enable-hello-feature"></a><span data-ttu-id="877ee-120">Krok 2: Włączanie funkcji hello</span><span class="sxs-lookup"><span data-stu-id="877ee-120">Step 2: Enable hello feature</span></span>

<span data-ttu-id="877ee-121">Bezproblemowe logowanie Jednokrotne można włączyć za pomocą [Azure AD Connect](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="877ee-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="877ee-122">Jeśli przeprowadzasz nową instalację programu Azure AD Connect, wybierz hello [niestandardową ścieżkę](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="877ee-122">If you are doing a fresh installation of Azure AD Connect, choose hello [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="877ee-123">Na powitania "użytkownika" strony logowania zaznacz opcję "Włącz logowanie jednokrotne" hello.</span><span class="sxs-lookup"><span data-stu-id="877ee-123">At hello "User sign-in" page, check hello "Enable single sign on" option.</span></span>

![Azure AD Connect - logowanie użytkowników](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="877ee-125">Jeśli masz już zainstalowany program Azure AD Connect, wybierz polecenie "Zmień użytkownika strony logowania" w Azure AD Connect, a następnie kliknij przycisk "Dalej".</span><span class="sxs-lookup"><span data-stu-id="877ee-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="877ee-126">Następnie zaznacz opcję "Włącz logowanie jednokrotne" hello.</span><span class="sxs-lookup"><span data-stu-id="877ee-126">Then check hello "Enable single sign on" option.</span></span>

![Azure AD Connect - zmiany logowania użytkownika](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="877ee-128">Kontynuacja za pomocą Kreatora hello pobrać toohello "Włącz logowanie jednokrotne" strony.</span><span class="sxs-lookup"><span data-stu-id="877ee-128">Continue through hello wizard until you get toohello "Enable single sign on" page.</span></span> <span data-ttu-id="877ee-129">Podaj poświadczenia administratora domeny dla każdego lasu usługi AD, aby synchronizować tooAzure AD (za pomocą usługi Azure AD Connect) oraz dla użytkowników, którzy mają tooenable bezproblemowe logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="877ee-129">Provide Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span> 

<span data-ttu-id="877ee-130">Po zakończeniu Kreatora hello bezproblemowe rejestracji Jednokrotnej jest włączona na dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="877ee-130">After completion of hello wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="877ee-131">poświadczenia administratora domeny Hello nie są przechowywane w programie Azure AD Connect lub w usłudze Azure AD, ale są tylko używane tooenable hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="877ee-131">hello Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used tooenable hello feature.</span></span>

<span data-ttu-id="877ee-132">Wykonaj te tooverify instrukcje prawidłowo włączona bezproblemowe rejestracji Jednokrotnej:</span><span class="sxs-lookup"><span data-stu-id="877ee-132">Follow these instructions tooverify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="877ee-133">Zaloguj się toohello [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) z hello poświadczenia administratora globalnego dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="877ee-133">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with hello Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="877ee-134">Wybierz **usługi Azure Active Directory** na powitania nawigacji po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="877ee-134">Select **Azure Active Directory** on hello left-hand navigation.</span></span>
3. <span data-ttu-id="877ee-135">Wybierz **programu Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="877ee-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="877ee-136">Sprawdź, że hello **bezproblemowe logowanie jednokrotne** funkcji jest pokazywana jako **włączone**.</span><span class="sxs-lookup"><span data-stu-id="877ee-136">Verify that hello **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Portal Azure — blok Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a><span data-ttu-id="877ee-138">Krok 3: Wdrażanie funkcji hello</span><span class="sxs-lookup"><span data-stu-id="877ee-138">Step 3: Roll out hello feature</span></span>

<span data-ttu-id="877ee-139">tooroll hello funkcji tooyour użytkowników, należy tooadd dwie usługi Azure AD adresów URL (https://autologon.microsoftazuread-sso.com i https://aadg.windows.net.nsatc.net) toousers ustawienia strefy Intranet przy użyciu zasad grupy w usłudze Active Directory.</span><span class="sxs-lookup"><span data-stu-id="877ee-139">tooroll out hello feature tooyour users, you need tooadd two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) toousers' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="877ee-140">Witaj następujące instrukcje działa tylko dla programu Internet Explorer i Google Chrome w systemie Windows (Jeśli zestaw adresów URL zaufanych witryn współużytkuje z programu Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="877ee-140">hello following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="877ee-141">Przeczytaj hello następnej sekcji tooset instrukcje Mozilla Firefox i Google Chrome na komputerach Mac.</span><span class="sxs-lookup"><span data-stu-id="877ee-141">Read hello next section for instructions tooset up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a><span data-ttu-id="877ee-142">Dlaczego należy ustawienia strefy Intranet toomodify użytkowników?</span><span class="sxs-lookup"><span data-stu-id="877ee-142">Why do you need toomodify users' Intranet zone settings?</span></span>

<span data-ttu-id="877ee-143">Domyślnie przeglądarki hello automatycznie oblicza hello prawo strefy (w Internecie lub intranecie) z adresu URL.</span><span class="sxs-lookup"><span data-stu-id="877ee-143">By default, hello browser automatically calculates hello right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="877ee-144">Na przykład http://contoso/ jest mapowanych toohello strefy intranetowej, http://intranet.contoso.com/ jest mapowanych toohello strefy Internet (ponieważ hello adres URL zawiera kropkę).</span><span class="sxs-lookup"><span data-stu-id="877ee-144">For example, http://contoso/ is mapped toohello Intranet zone, whereas http://intranet.contoso.com/ is mapped toohello Internet zone (because hello URL contains a period).</span></span> <span data-ttu-id="877ee-145">Przeglądarki wysyłaj punktu końcowego chmury tooa biletów Kerberos — jak hello dwa Azure AD adresy URL - chyba, że adres URL jest dodanych w sposób jawny strefy Intranet toohello przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="877ee-145">Browsers don't send Kerberos tickets tooa cloud endpoint - like hello two Azure AD URLs - unless its URL is explicitly added toohello browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="877ee-146">Szczegółowe procedury</span><span class="sxs-lookup"><span data-stu-id="877ee-146">Detailed steps</span></span>

1. <span data-ttu-id="877ee-147">Narzędzia do zarządzania zasadami grupy Otwórz hello.</span><span class="sxs-lookup"><span data-stu-id="877ee-147">Open hello Group Policy Management tool.</span></span>
2. <span data-ttu-id="877ee-148">Edytuj hello zasady grupy zastosowane toosome lub wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="877ee-148">Edit hello Group Policy that is applied toosome or all your users.</span></span> <span data-ttu-id="877ee-149">W tym przykładzie używamy hello **domyślne zasady domeny**.</span><span class="sxs-lookup"><span data-stu-id="877ee-149">In this example, we use hello **Default Domain Policy**.</span></span>
3. <span data-ttu-id="877ee-150">Przejdź za**strony Panel\Security formantu użytkownika Konfiguracja komputera\Szablony administracyjne\Składniki systemu Windows\Internet Explorer\Internetowy** i wybierz **tooZone Lista przypisywanie lokacji**.</span><span class="sxs-lookup"><span data-stu-id="877ee-150">Navigate too**User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site tooZone Assignment List**.</span></span>
<span data-ttu-id="877ee-151">![Logowanie jednokrotne](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="877ee-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="877ee-152">Włącz hello zasady, a następnie wprowadź hello następującej wartości (Azure adresy URL usługi AD w którym bilety Kerberos są przekazywane) i danych (*1* wskazuje strefy Intranet) w oknie dialogowym hello.</span><span class="sxs-lookup"><span data-stu-id="877ee-152">Enable hello policy, and enter hello following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in hello dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="877ee-153">Toodisallow niektórych użytkowników przy użyciu logowania jednokrotnego bezproblemowe — na przykład, jeśli ci użytkownicy są logują się na udostępnionym kioski - ustawić hello poprzedzających wartości zbyt*4*.</span><span class="sxs-lookup"><span data-stu-id="877ee-153">If you want toodisallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set hello preceding values too*4*.</span></span> <span data-ttu-id="877ee-154">Ta akcja dodaje hello Azure AD adresy URL toohello strefy witryny z ograniczeniami, a nie bezproblemowe logowanie Jednokrotne cały czas hello.</span><span class="sxs-lookup"><span data-stu-id="877ee-154">This action adds hello Azure AD URLs toohello Restricted Zone, and fails Seamless SSO all hello time.</span></span>

5. <span data-ttu-id="877ee-155">Kliknij przycisk **OK** i **OK** ponownie.</span><span class="sxs-lookup"><span data-stu-id="877ee-155">Click **OK** and **OK** again.</span></span>

![Logowanie jednokrotne](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="877ee-157">Zagadnienia dotyczące przeglądarki</span><span class="sxs-lookup"><span data-stu-id="877ee-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="877ee-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="877ee-158">Mozilla Firefox</span></span>

<span data-ttu-id="877ee-159">Mozilla Firefox nie automatycznie wykonuje uwierzytelnianie Kerberos.</span><span class="sxs-lookup"><span data-stu-id="877ee-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="877ee-160">Każdy użytkownik ma toomanually Dodaj adresy URL hello Azure AD tootheir Firefox ustawienia za pomocą hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="877ee-160">Each user has toomanually add hello Azure AD URLs tootheir Firefox settings using hello following steps:</span></span>
1. <span data-ttu-id="877ee-161">Uruchom program Firefox, a następnie wprowadź `about:config` na pasku adresu hello.</span><span class="sxs-lookup"><span data-stu-id="877ee-161">Run Firefox and enter `about:config` in hello address bar.</span></span> <span data-ttu-id="877ee-162">Odrzucić żadnych powiadomień, które są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="877ee-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="877ee-163">Wyszukaj hello **network.negotiate-auth.trusted URI** preferencji.</span><span class="sxs-lookup"><span data-stu-id="877ee-163">Search for hello **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="877ee-164">Ta opcja wyświetla listę zaufanych witryn w programie Firefox uwierzytelniania Kerberos.</span><span class="sxs-lookup"><span data-stu-id="877ee-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="877ee-165">Kliknij prawym przyciskiem myszy i wybierz polecenie "Modyfikuj".</span><span class="sxs-lookup"><span data-stu-id="877ee-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="877ee-166">Wprowadź "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" hello pola.</span><span class="sxs-lookup"><span data-stu-id="877ee-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in hello field.</span></span>
5. <span data-ttu-id="877ee-167">Kliknij przycisk "OK" i ponownie otwórz hello przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="877ee-167">Click "OK" and reopen hello browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="877ee-168">Przeglądarka Safari w systemie Mac OS</span><span class="sxs-lookup"><span data-stu-id="877ee-168">Safari on Mac OS</span></span>

<span data-ttu-id="877ee-169">Upewnij się, czy maszyna hello z systemem Mac OS jest tooAD połączone.</span><span class="sxs-lookup"><span data-stu-id="877ee-169">Ensure that hello machine running Mac OS is joined tooAD.</span></span> <span data-ttu-id="877ee-170">Zobacz instrukcje na temat toodo który [tutaj](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span><span class="sxs-lookup"><span data-stu-id="877ee-170">See instructions on how toodo that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="877ee-171">Google Chrome w systemie Mac OS</span><span class="sxs-lookup"><span data-stu-id="877ee-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="877ee-172">Google Chrome na innych platform z systemem innym niż Windows i Mac OS, można znaleźć zbyt[w tym artykule](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) Aby uzyskać informacje dotyczące sposobu toowhitelist hello adresy URL usługi Azure AD dla zintegrowanego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="877ee-172">For Google Chrome on Mac OS and other non-Windows platforms, refer too[this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how toowhitelist hello Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="877ee-173">Przy użyciu innych zasad grupy usługi Active Directory tooroll rozszerzenia hello Azure AD adresy URL tooFirefox i Google Chrome na użytkowników komputerów Mac, wykracza poza zakres tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="877ee-173">Using third-party Active Directory Group Policy extensions tooroll out hello Azure AD URLs tooFirefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="877ee-174">Znane ograniczenia</span><span class="sxs-lookup"><span data-stu-id="877ee-174">Known limitations</span></span>

<span data-ttu-id="877ee-175">Bezproblemowe logowanie Jednokrotne nie działa w trybie prywatnym przeglądania na przeglądarki Firefox i krawędzi.</span><span class="sxs-lookup"><span data-stu-id="877ee-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="877ee-176">Również nie działa w programie Internet Explorer Jeśli przeglądarka hello jest uruchomiony w trybie ochrona rozszerzona.</span><span class="sxs-lookup"><span data-stu-id="877ee-176">It also doesn't work on Internet Explorer if hello browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="877ee-177">Firma Microsoft niedawno wycofane obsługę tooinvestigate krawędzi problemy zgłoszone przez klienta.</span><span class="sxs-lookup"><span data-stu-id="877ee-177">We recently rolled back support for Edge tooinvestigate customer-reported issues.</span></span>

## <a name="step-4-test-hello-feature"></a><span data-ttu-id="877ee-178">Krok 4: Testowanie hello funkcji</span><span class="sxs-lookup"><span data-stu-id="877ee-178">Step 4: Test hello feature</span></span>

<span data-ttu-id="877ee-179">Funkcja hello tootest dla określonego użytkownika, upewnij się, że _wszystkie_ hello następujące warunki zostały spełnione:</span><span class="sxs-lookup"><span data-stu-id="877ee-179">tootest hello feature for a specific user, ensure that _all_ hello following conditions are in place:</span></span>
  - <span data-ttu-id="877ee-180">Hello użytkownik loguje się na urządzeniach firmowych.</span><span class="sxs-lookup"><span data-stu-id="877ee-180">hello user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="877ee-181">Witaj urządzenie zostało tooyour wcześniej przyłączone do domeny usługi Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="877ee-181">hello device has been previously joined tooyour Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="877ee-182">urządzenie Hello ma bezpośredniego połączenia tooyour domenowych Kontrolerze, hello sieci przewodowej lub bezprzewodowej w sieci firmowej lub za pośrednictwem połączenia dostępu zdalnego, takich jak połączenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="877ee-182">hello device has a direct connection tooyour Domain Controller (DC), either on hello corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="877ee-183">Masz [wprowadzanie funkcji hello](##step-3-roll-out-the-feature) toothis użytkownika przy użyciu zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="877ee-183">You have [rolled out hello feature](##step-3-roll-out-the-feature) toothis user using Group Policy.</span></span>

<span data-ttu-id="877ee-184">Scenariusz hello tootest gdzie hello użytkownik wprowadza tylko hello nazwy użytkownika, ale nie hasło hello:</span><span class="sxs-lookup"><span data-stu-id="877ee-184">tootest hello scenario where hello user enters only hello username, but not hello password:</span></span>
- <span data-ttu-id="877ee-185">Zaloguj się do *https://myapps.microsoft.com/* w nowej sesji przeglądarki prywatnych.</span><span class="sxs-lookup"><span data-stu-id="877ee-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="877ee-186">Scenariusz hello tootest gdzie hello użytkownika nie ma hasła nazwa użytkownika lub hello hello tooenter:</span><span class="sxs-lookup"><span data-stu-id="877ee-186">tootest hello scenario where hello user doesn't have tooenter hello username or hello password:</span></span> 
- <span data-ttu-id="877ee-187">Zaloguj się do *https://myapps.microsoft.com/contoso.onmicrosoft.com* w nowej sesji przeglądarki prywatnych.</span><span class="sxs-lookup"><span data-stu-id="877ee-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="877ee-188">Zastąp "*contoso*" nazwą swojej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="877ee-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="877ee-189">Lub zaloguj się do *https://myapps.microsoft.com/contoso.com* w nowej sesji przeglądarki prywatnych.</span><span class="sxs-lookup"><span data-stu-id="877ee-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="877ee-190">Zastąp "*contoso.com*" z zweryfikowanej domeny (nie domeny federacyjnej) w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="877ee-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="877ee-191">Krok 5: Przerzucane kluczy</span><span class="sxs-lookup"><span data-stu-id="877ee-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="877ee-192">W kroku 2 Azure AD Connect tworzy kont komputerów (reprezentujący usługi Azure AD) w wszystkich lasach hello AD, na których włączono bezproblemowe logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="877ee-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all hello AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="877ee-193">Dowiedz się więcej szczegółów w [tutaj](active-directory-aadconnect-sso-how-it-works.md).</span><span class="sxs-lookup"><span data-stu-id="877ee-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="877ee-194">Ze względów bezpieczeństwa zaleca się, że można często są przerzucane hello Kerberos odszyfrowywania klucze te konta komputera.</span><span class="sxs-lookup"><span data-stu-id="877ee-194">For improved security, it is recommended that  you frequently roll over hello Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="877ee-195">Nie trzeba toodo ten krok _natychmiast_ po włączeniu funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="877ee-195">You don't need toodo this step _immediately_ after you have enabled hello feature.</span></span> <span data-ttu-id="877ee-196">Przerzuć kluczy odszyfrowujących Kerberos hello co najmniej 30 dni.</span><span class="sxs-lookup"><span data-stu-id="877ee-196">Roll over hello Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="877ee-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="877ee-197">Next steps</span></span>

- <span data-ttu-id="877ee-198">[**Nowości techniczne** ](active-directory-aadconnect-sso-how-it-works.md) -zrozumieć sposób działania tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="877ee-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="877ee-199">[**Często zadawane pytania** ](active-directory-aadconnect-sso-faq.md) -odpowiedzi toofrequently zadawane pytania.</span><span class="sxs-lookup"><span data-stu-id="877ee-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="877ee-200">[**Rozwiązywanie problemów z** ](active-directory-aadconnect-troubleshoot-sso.md) — Dowiedz się, jak tooresolve typowe problemy związane z funkcją hello.</span><span class="sxs-lookup"><span data-stu-id="877ee-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="877ee-201">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="877ee-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
