---
title: "Azure Active Directory Connect: Często zadawane pytania dotyczące - | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera często zadawane pytania dotyczące usługi Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="c4b1a-103">Często zadawane pytania dotyczące usługi Azure Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="c4b1a-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="c4b1a-104">Ogólne instalacji</span><span class="sxs-lookup"><span data-stu-id="c4b1a-104">General installation</span></span>
<span data-ttu-id="c4b1a-105">**Pytanie: czy będzie instalacji działać, jeśli hello Azure AD administratora globalnego ma 2FA włączone?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-105">**Q: Will installation work if hello Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="c4b1a-106">Z kompilacjami powitania od lutego 2016 jest to obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-106">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="c4b1a-107">**Pytanie: czy istnieje tooinstall sposób Azure AD Connect nienadzorowanej?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-107">**Q: Is there a way tooinstall Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="c4b1a-108">Jest tylko obsługiwana tooinstall Azure AD Connect przy użyciu Kreatora instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-108">It is only supported tooinstall Azure AD Connect using hello installation wizard.</span></span> <span data-ttu-id="c4b1a-109">Instalacja nienadzorowana i dyskretnej nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="c4b1a-110">**Pytanie: czy masz lasu, gdy nie można skontaktować się z jednej domeny. Jak zainstalować usługi Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="c4b1a-111">Z kompilacjami powitania od lutego 2016 jest to obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-111">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="c4b1a-112">**Pytanie: czy hello pracy agenta kondycji usług AD DS w instalacji server core?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-112">**Q: Does hello AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="c4b1a-113">Tak.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-113">Yes.</span></span> <span data-ttu-id="c4b1a-114">Po zainstalowaniu agenta hello, można ukończyć procesu rejestracji hello za pomocą następującego polecenia cmdlet programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="c4b1a-114">After installing hello agent, you can complete hello registration process using hello following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="c4b1a-115">Sieć</span><span class="sxs-lookup"><span data-stu-id="c4b1a-115">Network</span></span>
<span data-ttu-id="c4b1a-116">**Pytanie: czy mam zapory, urządzenia sieciowego lub czegoś innego, która ogranicza hello maksymalny czas połączenia pozostają otwarte w sieci. Jak długo Moje próg limitu czasu po stronie klienta należy przy użyciu usługi Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-116">**Q: I have a firewall, network device, or something else that limits hello maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="c4b1a-117">Całe oprogramowanie sieciowe, urządzenia fizyczne lub jakikolwiek inny limity hello maksymalnego czasu połączenia może pozostawać otwarte powinien używać progu co najmniej 5 minut (300 sekund) do obsługi łączności między hello serwer, gdzie hello klienta usługi Azure AD Connect jest zainstalowany i Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-117">All networking software, physical devices, or anything else that limits hello maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between hello server where hello Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="c4b1a-118">Dotyczy to również narzędzia synchronizacji pakietu Microsoft Identity tooall wydane wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-118">This also applies tooall previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="c4b1a-119">**Pytanie: czy domeny drugiego poziomu (jednej etykiety domen) obsługiwane?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="c4b1a-120">Nie, usługi Azure AD Connect nie obsługuje lokalnymi lasami/domenami przy użyciu drugiego poziomu.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="c4b1a-121">**Pytanie: czy "kropkami" o nazwie NetBios obsługiwane?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="c4b1a-122">Nie, usługi Azure AD Connect nie obsługuje lokalnymi lasami/domenami, których nazwa NetBios hello zawiera kropkę "." w nazwie hello.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-122">No, Azure AD Connect does not support on-premises forests/domains where hello NetBios name contains a period "." in hello name.</span></span>

## <a name="federation"></a><span data-ttu-id="c4b1a-123">Federacyjna</span><span class="sxs-lookup"><span data-stu-id="c4b1a-123">Federation</span></span>
<span data-ttu-id="c4b1a-124">**Pytanie: co zrobić, jeśli otrzymuję wiadomość e-mail, który monit toorenew certyfikatu usługi Office 365**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-124">**Q: What do I do if I receive an email that asking me toorenew my Office 365 certificate**</span></span>  
<span data-ttu-id="c4b1a-125">Użyj wskazówek hello, opisaną w hello [odnawiania certyfikatów](active-directory-aadconnect-o365-certs.md) tematu w sposób toorenew hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-125">Use hello guidance that is outlined in hello [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how toorenew hello certificate.</span></span>

<span data-ttu-id="c4b1a-126">**Pytanie: czy masz "Automatycznie Aktualizuj jednostki uzależnionej" dla jednostki uzależnionej usługi Office 365. Należy tootake żadnych działań po Moje token certyfikatu podpisywania automatycznie najedzie na?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have tootake any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="c4b1a-127">Użyj wskazówek hello, opisaną w artykule hello [odnawiania certyfikatów](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="c4b1a-127">Use hello guidance that is outlined in hello article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="c4b1a-128">Środowisko</span><span class="sxs-lookup"><span data-stu-id="c4b1a-128">Environment</span></span>
<span data-ttu-id="c4b1a-129">**Pytanie: jest obsługiwane it toorename powitania serwera po zainstalowaniu usługi Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-129">**Q: Is it supported toorename hello server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="c4b1a-130">Nie.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-130">No.</span></span> <span data-ttu-id="c4b1a-131">Zmiana nazwy serwera hello toonot aparatu synchronizacji hello Przyczyna będą mogli tooconnect toohello SQL database i hello usługi nie będą mogli toostart.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-131">Changing hello server name will cause hello sync engine toonot be able tooconnect toohello SQL database and hello service will not be able toostart.</span></span>

## <a name="identity-data"></a><span data-ttu-id="c4b1a-132">Danych tożsamości</span><span class="sxs-lookup"><span data-stu-id="c4b1a-132">Identity data</span></span>
<span data-ttu-id="c4b1a-133">**Pytanie: hello atrybut nazwy UPN (userPrincipalName) w usłudze Azure AD nie odpowiada hello UPN lokalnego — Dlaczego?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-133">**Q: hello UPN (userPrincipalName) attribute in Azure AD does not match hello on-prem UPN - why?**</span></span>  
<span data-ttu-id="c4b1a-134">Zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="c4b1a-134">See these articles:</span></span>

* [<span data-ttu-id="c4b1a-135">Nazwy użytkowników nie są zgodne w usłudze Office 365, Azure lub Intune hello lokalną nazwą UPN lub alternatywnym Identyfikatorem logowania</span><span class="sxs-lookup"><span data-stu-id="c4b1a-135">User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="c4b1a-136">Zmiany nie są synchronizowane przez narzędzie do synchronizacji usługi Azure Active Directory powitania po zmianie hello UPN toouse konto użytkownika innej domeny federacyjnej</span><span class="sxs-lookup"><span data-stu-id="c4b1a-136">Changes aren't synced by hello Azure Active Directory Sync tool after you change hello UPN of a user account toouse a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="c4b1a-137">Można również skonfigurować userPrincipalName hello tooupdate aparatu synchronizacji usługi Azure AD tooallow hello zgodnie z opisem w [funkcji Usługa synchronizacji Azure AD Connect](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="c4b1a-137">You can also configure Azure AD tooallow hello sync engine tooupdate hello userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="c4b1a-138">**Pytanie: jest it obsługiwane toosoft dopasowania lokalnych obiektów grupy AD skontaktuj się z obiektami usługi Azure AD grupy/skontaktuj się z istniejącą?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-138">**Q: Is it supported toosoft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="c4b1a-139">Nie jest to obecnie nieobsługiwane.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-139">No, this is currently not supported.</span></span>

<span data-ttu-id="c4b1a-140">**P: jest toomanually it obsługiwane atrybut nazwę ImmutableId na istniejące usługi Azure AD grupy/skontaktuj się z obiektów toohard dopasowanie tooon lokalnych obiektów grupy AD skontaktuj się z?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-140">**Q: Is it supported toomanually set ImmutableId attribute on existing Azure AD Group/Contact objects toohard match it tooon-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="c4b1a-141">Nie jest to obecnie nieobsługiwane.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="c4b1a-142">Konfiguracja niestandardowa</span><span class="sxs-lookup"><span data-stu-id="c4b1a-142">Custom configuration</span></span>
<span data-ttu-id="c4b1a-143">**Pytanie: gdzie są polecenia cmdlet programu PowerShell hello Azure AD Connect udokumentowane?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-143">**Q: Where are hello PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="c4b1a-144">Z wyjątkiem hello poleceń cmdlet hello opisane w tej lokacji innych poleceń cmdlet programu PowerShell znaleziono w programie Azure AD Connect nie są obsługiwane przez klienta.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-144">With hello exception of hello cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="c4b1a-145">**Pytanie: czy można użyć "Serwera serwer eksportu/importu" znaleziony w *Menedżera usługi synchronizacji* konfiguracji toomove między serwerami?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* toomove configuration between servers?**</span></span>  
<span data-ttu-id="c4b1a-146">Nie.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-146">No.</span></span> <span data-ttu-id="c4b1a-147">Ta opcja nie pobierze wszystkie ustawienia konfiguracji i nie powinna być używana.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="c4b1a-148">Zamiast tego należy użyć konfiguracji podstawowej hello toocreate kreatora hello na drugim serwerze hello i użyć reguły synchronizacji hello Edytor toomove skryptów PowerShell toogenerate wszystkie reguły niestandardowej między serwerami.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-148">You should instead use hello wizard toocreate hello base configuration on hello second server and use hello sync rule editor toogenerate PowerShell scripts toomove any custom rule between servers.</span></span> <span data-ttu-id="c4b1a-149">Zobacz [migracji w kierunku](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="c4b1a-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="c4b1a-150">**Pytanie: hasła można buforować strony hello Azure logowania i może to być zablokowana, ponieważ zawiera element input hasła Autouzupełnianie hello = "false" atrybutu?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-150">**Q: Can passwords be cached for hello Azure sign-in page and can this be prevented since it contains a password input element with hello autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="c4b1a-151">Obecnie nie obsługujemy modyfikowania atrybutów HTML hello pola wejściowego hasła hello, tym hello autouzupełniania tagu.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-151">We currently do not support modifying hello HTML attributes of hello Password input field, including hello autocomplete tag.</span></span> <span data-ttu-id="c4b1a-152">Obecnie pracujemy funkcja, która pozwoli niestandardowych skryptów Javascript, co pozwoli tooadd wszystkie pola atrybutu toohello hasła.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-152">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="c4b1a-153">Powinna to być nowsze część 2017 r.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="c4b1a-154">**P: na hello Azure strony logowania są wyświetlane nazwy użytkowników dla użytkowników, którzy wcześniej zalogowali się pomyślnie.  Można to zachowanie wyłączyć?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-154">**Q: On hello Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="c4b1a-155">Obecnie nie obsługujemy modyfikowanie hello atrybuty HTML strony logowania hello.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-155">We currently do not support modifying hello HTML attributes of hello sign-in page.</span></span> <span data-ttu-id="c4b1a-156">Obecnie pracujemy funkcja, która pozwoli niestandardowych skryptów Javascript, co pozwoli tooadd wszystkie pola atrybutu toohello hasła.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-156">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="c4b1a-157">Powinna to być nowsze część 2017 r.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="c4b1a-158">**Pytanie: czy istnieje tooprevent sposób równoczesnych sesji?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-158">**Q: Is there a way tooprevent concurrent sessions?**</span></span></br>
<span data-ttu-id="c4b1a-159">Nie.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="c4b1a-160">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="c4b1a-160">Troubleshooting</span></span>
<span data-ttu-id="c4b1a-161">**Pytanie: jak uzyskać pomoc dotyczącą usługi Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="c4b1a-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="c4b1a-162">Witaj wyszukiwania bazy wiedzy Microsoft Knowledge Base (KB)</span><span class="sxs-lookup"><span data-stu-id="c4b1a-162">Search hello Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="c4b1a-163">Witaj wyszukiwania bazy wiedzy Microsoft Knowledge Base (KB) dla rozwiązań technicznych toocommon naprawa w razie awarii problemy dotyczące pomocy technicznej programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-163">Search hello Microsoft Knowledge Base (KB) for technical solutions toocommon break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="c4b1a-164">Fora dotyczące usługi Active Directory platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c4b1a-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="c4b1a-165">Można wyszukiwać i wyszukać technicznych pytania i odpowiedzi od społeczności hello lub zadać pytanie własne klikając [tutaj](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="c4b1a-165">You can search and browse for technical questions and answers from hello community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="c4b1a-166">Dział obsługi klienta usługi Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="c4b1a-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="c4b1a-167">Użyj tej obsługi tooget łącza za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c4b1a-167">Use this link tooget support through hello Azure portal.</span></span>

