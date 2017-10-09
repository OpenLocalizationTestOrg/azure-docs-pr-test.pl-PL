---
title: "podręcznikowym ochronę tożsamości w usłudze Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Azure AD Identity Protection umożliwia zdolność hello toolimit tooexploit osoba atakująca, którego bezpieczeństwo zostało naruszone tożsamości lub urządzenie i toosecure tożsamości lub urządzenia, które wcześniej były toobe podejrzenia lub znanych naruszenia zabezpieczeń."
services: active-directory
keywords: "ochronę tożsamości usługi Azure active directory, usługa cloud app discovery, zarządzanie aplikacjami, zabezpieczeń, ryzyka, poziom ryzyka, luki w zabezpieczeniach, zasady zabezpieczeń"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="d094f-104">Azure podręcznikowym ochronę tożsamości w usłudze Active Directory</span><span class="sxs-lookup"><span data-stu-id="d094f-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="d094f-105">Tego podręcznika dotyczącego ułatwia:</span><span class="sxs-lookup"><span data-stu-id="d094f-105">This playbook helps you to:</span></span>

* <span data-ttu-id="d094f-106">Wypełnij dane w środowisku Identity Protection hello symulowanie symulacje zdarzenia o podwyższonym ryzyku i luk w zabezpieczeniach</span><span class="sxs-lookup"><span data-stu-id="d094f-106">Populate data in hello Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="d094f-107">Konfigurowanie zasad dostępu warunkowego opartego na ryzyko i testowanie wpływu hello tych zasad</span><span class="sxs-lookup"><span data-stu-id="d094f-107">Set up risk-based conditional access policies and test hello impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="d094f-108">Symulacja zdarzeń o podwyższonym ryzyku</span><span class="sxs-lookup"><span data-stu-id="d094f-108">Simulating Risk Events</span></span>
<span data-ttu-id="d094f-109">W tej sekcji przedstawiono kroki symulowanie hello następujące typy zdarzeń ryzyka:</span><span class="sxs-lookup"><span data-stu-id="d094f-109">This section provides you with steps for simulating hello following risk event types:</span></span>

* <span data-ttu-id="d094f-110">Logowania z anonimowych adresów IP (prosty)</span><span class="sxs-lookup"><span data-stu-id="d094f-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="d094f-111">Logowania z nieznanych lokalizacji (umiarkowany)</span><span class="sxs-lookup"><span data-stu-id="d094f-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="d094f-112">Niemożliwa podróż tooatypical lokalizacje (trudne)</span><span class="sxs-lookup"><span data-stu-id="d094f-112">Impossible travel tooatypical locations (difficult)</span></span>

<span data-ttu-id="d094f-113">Inne zdarzenia o podwyższonym ryzyku nie symulowane w bezpieczny sposób.</span><span class="sxs-lookup"><span data-stu-id="d094f-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="d094f-114">Logowania z anonimowych adresów IP</span><span class="sxs-lookup"><span data-stu-id="d094f-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="d094f-115">Ten typ zdarzenia ryzyka identyfikuje użytkowników, którzy zalogowali się pomyślnie z adresu IP, który został zidentyfikowany jako adres IP anonimowy serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="d094f-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="d094f-116">Te serwery proxy są używane przez osoby, które mają toohide adres IP swoich urządzeń i może służyć do złośliwymi działaniami.</span><span class="sxs-lookup"><span data-stu-id="d094f-116">These proxies are used by people who want toohide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="d094f-117">**toosimulate logowania z anonimowych adresów IP, wykonaj następujące kroki hello**:</span><span class="sxs-lookup"><span data-stu-id="d094f-117">**toosimulate a sign-in from an anonymous IP, perform hello following steps**:</span></span>

1. <span data-ttu-id="d094f-118">Pobierz hello [przeglądarki Tor](https://www.torproject.org/projects/torbrowser.html.en).</span><span class="sxs-lookup"><span data-stu-id="d094f-118">Download hello [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="d094f-119">Przy użyciu przeglądarki Tor hello Przejdź zbyt[https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d094f-119">Using hello Tor Browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="d094f-120">Wprowadź poświadczenia hello hello konta tooappear w hello **logowania z anonimowych adresów IP** raportu.</span><span class="sxs-lookup"><span data-stu-id="d094f-120">Enter hello credentials of hello account you want tooappear in hello **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="d094f-121">Logowanie Hello będą widoczne na pulpicie nawigacyjnym Identity Protection hello w ciągu 5 minut.</span><span class="sxs-lookup"><span data-stu-id="d094f-121">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="d094f-122">Logowania z nieznanych lokalizacji</span><span class="sxs-lookup"><span data-stu-id="d094f-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="d094f-123">Hello nieznanych lokalizacji ryzyko jest mechanizm oceny w czasie rzeczywistym logowania, który uwzględnia poza logowania w lokalizacji (IP, szerokości geograficznej / długości i ASN) toodetermine nowe / nieznanych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="d094f-123">hello unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) toodetermine new / unfamiliar locations.</span></span> <span data-ttu-id="d094f-124">Hello system przechowuje poprzednie adresów IP, szerokości geograficznej / długości i numerów ASN użytkownika i traktuje te lokalizacje znanych toobe.</span><span class="sxs-lookup"><span data-stu-id="d094f-124">hello system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these toobe familiar locations.</span></span> <span data-ttu-id="d094f-125">Lokalizacja logowania jest uznawany za doświadczenia w pracy, jeśli hello lokalizacji logowania nie pasuje do żadnego z istniejącej lokalizacji znanych hello.</span><span class="sxs-lookup"><span data-stu-id="d094f-125">A sign-in location is considered unfamiliar if hello sign-in location does not match any of hello existing familiar locations.</span></span>

<span data-ttu-id="d094f-126">Ochrona tożsamości usługi Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="d094f-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="d094f-127">ma okres learning początkowej 14 dni, w których nie Flaga wszelkie nowe lokalizacje jako nieznanych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="d094f-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="d094f-128">ignoruje logowania z urządzeń znanych i lokalizacje, które są istniejącej lokalizacji znanych tooan geograficznie Zamknij.</span><span class="sxs-lookup"><span data-stu-id="d094f-128">ignores sign-ins from familiar devices and locations that are geographically close tooan existing familiar location.</span></span>

<span data-ttu-id="d094f-129">toosimulate nieznanych lokalizacji i masz toosign w z lokalizacji i urządzenia, które konta hello nie zalogował się z przed.</span><span class="sxs-lookup"><span data-stu-id="d094f-129">toosimulate unfamiliar locations, you have toosign in from a location and device that hello account has not signed in from before.</span></span> 

<span data-ttu-id="d094f-130">**toosimulate logowania z nieznanych lokalizacji, wykonaj hello następujące kroki**:</span><span class="sxs-lookup"><span data-stu-id="d094f-130">**toosimulate a sign-in from an unfamiliar location, perform hello following steps**:</span></span>

1. <span data-ttu-id="d094f-131">Wybierz konto, które ma co najmniej 14 dni historii logowania.</span><span class="sxs-lookup"><span data-stu-id="d094f-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="d094f-132">Wykonaj jedną:</span><span class="sxs-lookup"><span data-stu-id="d094f-132">Do either:</span></span>
   
   <span data-ttu-id="d094f-133">a.</span><span class="sxs-lookup"><span data-stu-id="d094f-133">a.</span></span> <span data-ttu-id="d094f-134">Podczas korzystania z sieci VPN, przejdź zbyt[https://myapps.microsoft.com](https://myapps.microsoft.com) i wprowadź poświadczenia hello hello konta toosimulate hello ryzyka zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="d094f-134">While using a VPN, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com) and enter hello credentials of hello account you want toosimulate hello risk event for.</span></span>
   
   <span data-ttu-id="d094f-135">b.</span><span class="sxs-lookup"><span data-stu-id="d094f-135">b.</span></span> <span data-ttu-id="d094f-136">Poproś kojarzenie w innej lokalizacji toosign przy użyciu poświadczeń konta hello (niezalecane).</span><span class="sxs-lookup"><span data-stu-id="d094f-136">Ask an associate in a different location toosign in using hello account’s credentials (not recommended).</span></span>

<span data-ttu-id="d094f-137">Logowanie Hello będą widoczne na pulpicie nawigacyjnym Identity Protection hello w ciągu 5 minut.</span><span class="sxs-lookup"><span data-stu-id="d094f-137">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-tooatypical-location"></a><span data-ttu-id="d094f-138">Niemożliwa podróż tooatypical lokalizacji</span><span class="sxs-lookup"><span data-stu-id="d094f-138">Impossible travel tooatypical location</span></span>
<span data-ttu-id="d094f-139">Symuluje warunku niemożliwa podróż hello jest trudne, ponieważ hello algorytm machine learning tooweed limit false alarmów, takich jak niemożliwa podróż ze znanych urządzeń lub logowania z sieci VPN, które są używane przez innych użytkowników w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="d094f-139">Simulating hello impossible travel condition is difficult because hello algorithm uses machine learning tooweed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in hello directory.</span></span> <span data-ttu-id="d094f-140">Ponadto hello algorytm wymaga 3 dni too14 historię logowania dla użytkownika hello przed rozpoczęciem generowania zdarzeń o podwyższonym ryzyku.</span><span class="sxs-lookup"><span data-stu-id="d094f-140">Additionally, hello algorithm requires a sign-in history of 3 too14 days for hello user before it begins generating risk events.</span></span>

<span data-ttu-id="d094f-141">**toosimulate niemożliwa podróż tooatypical lokalizacji, wykonaj hello następujące kroki**:</span><span class="sxs-lookup"><span data-stu-id="d094f-141">**toosimulate an impossible travel tooatypical location, perform hello following steps**:</span></span>

1. <span data-ttu-id="d094f-142">Za pomocą przeglądarki standardowe Przejdź zbyt[https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d094f-142">Using your standard browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="d094f-143">Wprowadź poświadczenia hello hello konta, którego chcesz toogenerate niemożliwa podróż zdarzenie ryzyka dla.</span><span class="sxs-lookup"><span data-stu-id="d094f-143">Enter hello credentials of hello account you want toogenerate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="d094f-144">Zmień agenta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d094f-144">Change your user agent.</span></span> <span data-ttu-id="d094f-145">Można zmienić agenta użytkownika w programie Internet Explorer z Developer Tools, lub zmień agenta użytkownika przeglądarki Firefox lub Chrome przy użyciu dodatku przełącznik agenta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d094f-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="d094f-146">Zmienianie adresu IP.</span><span class="sxs-lookup"><span data-stu-id="d094f-146">Change your IP address.</span></span> <span data-ttu-id="d094f-147">Adres IP można zmienić za pomocą sieci VPN, dodatek Tor, lub kręci się nowego komputera na platformie Azure w centrum danych.</span><span class="sxs-lookup"><span data-stu-id="d094f-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="d094f-148">Logowanie za[https://myapps.microsoft.com](https://myapps.microsoft.com) przy użyciu hello tych samych poświadczeń jako przed i za kilka minut po hello poprzedniej logowania.</span><span class="sxs-lookup"><span data-stu-id="d094f-148">Sign-in too[https://myapps.microsoft.com](https://myapps.microsoft.com) using hello same credentials as before and within a few minutes after hello previous sign-in.</span></span>

<span data-ttu-id="d094f-149">Logowanie Hello będą widoczne na pulpicie nawigacyjnym Identity Protection hello w ciągu 2-4 godzin.</span><span class="sxs-lookup"><span data-stu-id="d094f-149">hello sign-in will show up in hello Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="d094f-150">Z powodu modeli zaangażowany uczenia maszynowego złożonych hello istnieje ryzyko, które nie ma pobrać pobierany się.</span><span class="sxs-lookup"><span data-stu-id="d094f-150">Because of hello complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="d094f-151">Możesz tooreplicate te kroki dla wielu kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d094f-151">You might want tooreplicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="d094f-152">Symuluje luk w zabezpieczeniach</span><span class="sxs-lookup"><span data-stu-id="d094f-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="d094f-153">Luki w zabezpieczeniach występują słabych w środowisku usługi Azure AD, które mogą być używane przez aktora nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="d094f-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="d094f-154">Obecnie 3 typy luk w zabezpieczeniach są udostępniane w Azure AD Identity Protection, zwiększają inne funkcje usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d094f-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="d094f-155">Te luki w zabezpieczeniach zostanie wyświetlony na pulpicie nawigacyjnym Identity Protection hello automatycznie po skonfigurowaniu tych funkcji.</span><span class="sxs-lookup"><span data-stu-id="d094f-155">These Vulnerabilities will be displayed on hello Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="d094f-156">Usługi Azure AD [uwierzytelnianie wieloskładnikowe?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d094f-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="d094f-157">Usługi Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d094f-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="d094f-158">Usługi Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d094f-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="d094f-159">Ryzyko naruszenia zabezpieczeń użytkownika</span><span class="sxs-lookup"><span data-stu-id="d094f-159">User compromise risk</span></span>
<span data-ttu-id="d094f-160">**tootest ryzyko naruszenia zabezpieczeń użytkownika, wykonaj hello następujące kroki**:</span><span class="sxs-lookup"><span data-stu-id="d094f-160">**tootest User compromise risk, perform hello following steps**:</span></span>

1. <span data-ttu-id="d094f-161">Logowanie za[https://portal.azure.com](https://portal.azure.com) przy użyciu poświadczeń administratora globalnego dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="d094f-161">Sign-in too[https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="d094f-162">Przejdź za**Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="d094f-162">Navigate too**Identity Protection**.</span></span> 
3. <span data-ttu-id="d094f-163">Na powitania głównego **Azure AD Identity Protection** bloku, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="d094f-163">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="d094f-164">Na powitania **ustawienia portalu** bloku, w obszarze **reguły zabezpieczeń**, kliknij przycisk **ryzyko naruszenia zabezpieczeń użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="d094f-164">On hello **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="d094f-165">Na powitania **Zaloguj ryzyka** bloku, Włącz **Włącz regułę** wyłączone, a następnie kliknij przycisk **zapisać** ustawienia.</span><span class="sxs-lookup"><span data-stu-id="d094f-165">On hello **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="d094f-166">Symulowanie doświadczenia w pracy dla danego konta użytkownika, lokalizacji lub anonimowe zdarzenie ryzyka adresu IP.</span><span class="sxs-lookup"><span data-stu-id="d094f-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="d094f-167">To spowoduje podniesienie poziomu hello poziom ryzyka użytkownika dla tego użytkownika za**średni**.</span><span class="sxs-lookup"><span data-stu-id="d094f-167">This will elevate hello user risk level for that user too**Medium**.</span></span>
7. <span data-ttu-id="d094f-168">Poczekaj kilka minut, a następnie sprawdź tego poziomu użytkownika dla użytkownika jest **średni**.</span><span class="sxs-lookup"><span data-stu-id="d094f-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="d094f-169">Przejdź toohello **ustawienia portalu** bloku.</span><span class="sxs-lookup"><span data-stu-id="d094f-169">Go toohello **Portal Settings** blade.</span></span>
9. <span data-ttu-id="d094f-170">Na powitania **ryzyko naruszenia zabezpieczeń użytkownika** bloku, w obszarze **Włącz regułę**, wybierz pozycję **na** .</span><span class="sxs-lookup"><span data-stu-id="d094f-170">On hello **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="d094f-171">Wybierz jedną z hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="d094f-171">Select one of hello following options:</span></span>
    
    <span data-ttu-id="d094f-172">a.</span><span class="sxs-lookup"><span data-stu-id="d094f-172">a.</span></span> <span data-ttu-id="d094f-173">tooblock, wybierz opcję **średni** w obszarze **Zaloguj bloku**.</span><span class="sxs-lookup"><span data-stu-id="d094f-173">tooblock, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="d094f-174">b.</span><span class="sxs-lookup"><span data-stu-id="d094f-174">b.</span></span> <span data-ttu-id="d094f-175">tooenforce zmiany bezpieczne hasło, wybierz opcję **średni** w obszarze **wymusić uwierzytelnianie wieloskładnikowe**.</span><span class="sxs-lookup"><span data-stu-id="d094f-175">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="d094f-176">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d094f-176">Click **Save**.</span></span>
12. <span data-ttu-id="d094f-177">Teraz możesz przetestować dostępu warunkowego opartego na ryzyko, logując się przy użyciu użytkownik z poziomem ryzyka z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="d094f-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="d094f-178">Hello użytkownika ryzykiem w przypadku średniej, w zależności od konfiguracji hello zgodnie z zasadami, logowanie jest albo zablokowania lub zostało wymuszone toochange Twojego hasła.</span><span class="sxs-lookup"><span data-stu-id="d094f-178">If hello user risk is Medium, depending on hello configuration of your policy, your sign-in is be either blocked or you are forced toochange your password.</span></span> 
    <br><br><span data-ttu-id="d094f-179">
    ![Podręcznikowym](./media/active-directory-identityprotection-playbook/201.png "Podręcznikowym")
    </span><span class="sxs-lookup"><span data-stu-id="d094f-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="d094f-180">Ryzyko logowania</span><span class="sxs-lookup"><span data-stu-id="d094f-180">Sign-in risk</span></span>
<span data-ttu-id="d094f-181">**tootest logowania ryzyko, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d094f-181">**tootest a sign in risk, perform hello following steps:**</span></span>

1. <span data-ttu-id="d094f-182">Logowanie za[https://portal.azure.com ](https://portal.azure.com) przy użyciu poświadczeń administratora globalnego dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="d094f-182">Sign-in too[https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="d094f-183">Przejdź za**Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="d094f-183">Navigate too**Identity Protection**.</span></span>
3. <span data-ttu-id="d094f-184">Na powitania głównego **Azure AD Identity Protection** bloku, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="d094f-184">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="d094f-185">Na powitania **ustawienia portalu** bloku, w obszarze **reguły zabezpieczeń**, kliknij przycisk **Zaloguj ryzyka**.</span><span class="sxs-lookup"><span data-stu-id="d094f-185">On hello **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="d094f-186">Na powitania ** Zaloguj ryzyka ** bloku, wybierz opcję **na** w obszarze **Włącz regułę**.</span><span class="sxs-lookup"><span data-stu-id="d094f-186">On hello **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="d094f-187">Wybierz jedną z hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="d094f-187">Select one of hello following options:</span></span>
   
   <span data-ttu-id="d094f-188">a.</span><span class="sxs-lookup"><span data-stu-id="d094f-188">a.</span></span> <span data-ttu-id="d094f-189">tooblock, wybierz opcję **średni** w obszarze **bloku Zaloguj**</span><span class="sxs-lookup"><span data-stu-id="d094f-189">tooblock, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="d094f-190">b.</span><span class="sxs-lookup"><span data-stu-id="d094f-190">b.</span></span> <span data-ttu-id="d094f-191">tooenforce zmiany bezpieczne hasło, wybierz opcję **średni** w obszarze **wymusić uwierzytelnianie wieloskładnikowe**.</span><span class="sxs-lookup"><span data-stu-id="d094f-191">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="d094f-192">tooblock, wybierz nośnik w bloku logowania.</span><span class="sxs-lookup"><span data-stu-id="d094f-192">tooblock, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="d094f-193">uwierzytelnianie wieloskładnikowe tooenforce, wybierz opcję **średni** w obszarze **wymusić uwierzytelnianie wieloskładnikowe**.</span><span class="sxs-lookup"><span data-stu-id="d094f-193">tooenforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="d094f-194">Kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d094f-194">Click on **Save**.</span></span>
10. <span data-ttu-id="d094f-195">Teraz możesz przetestować dostępu warunkowego opartego na ryzyko symulując hello nieznanych lokalizacji lub anonimowe IP ryzyka zdarzeń, ponieważ są one zarówno **średni** ryzyka zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="d094f-195">You can now test risk-based conditional access by simulating hello unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="d094f-196">![Podręcznikowym](./media/active-directory-identityprotection-playbook/200.png "Podręcznikowym")</span><span class="sxs-lookup"><span data-stu-id="d094f-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="d094f-197">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d094f-197">See also</span></span>
* [<span data-ttu-id="d094f-198">Ochronę tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d094f-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

