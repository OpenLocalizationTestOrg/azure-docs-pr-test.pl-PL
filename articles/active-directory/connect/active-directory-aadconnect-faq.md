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
ms.openlocfilehash: fd5988b2d4170166902bb5cc39603d4a0f83be59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="787bd-103">Często zadawane pytania dotyczące usługi Azure Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="787bd-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="787bd-104">Ogólne instalacji</span><span class="sxs-lookup"><span data-stu-id="787bd-104">General installation</span></span>
<span data-ttu-id="787bd-105">**Pytanie: będzie instalacji działać, jeśli administrator globalny usługi Azure AD ma 2FA włączone?**</span><span class="sxs-lookup"><span data-stu-id="787bd-105">**Q: Will installation work if the Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="787bd-106">Z kompilacji w lutym 2016 r. jest to obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="787bd-106">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="787bd-107">**Pytanie: czy istnieje sposób, aby zainstalować program Azure AD Connect nienadzorowanej?**</span><span class="sxs-lookup"><span data-stu-id="787bd-107">**Q: Is there a way to install Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="787bd-108">Możliwe jest tylko zainstalować program Azure AD Connect przy użyciu Kreatora instalacji.</span><span class="sxs-lookup"><span data-stu-id="787bd-108">It is only supported to install Azure AD Connect using the installation wizard.</span></span> <span data-ttu-id="787bd-109">Instalacja nienadzorowana i dyskretnej nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="787bd-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="787bd-110">**Pytanie: czy masz lasu, gdy nie można skontaktować się z jednej domeny. Jak zainstalować usługi Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="787bd-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="787bd-111">Z kompilacji w lutym 2016 r. jest to obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="787bd-111">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="787bd-112">**Pytanie: agenta programu health usług AD DS działa w instalacji server core?**</span><span class="sxs-lookup"><span data-stu-id="787bd-112">**Q: Does the AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="787bd-113">Tak.</span><span class="sxs-lookup"><span data-stu-id="787bd-113">Yes.</span></span> <span data-ttu-id="787bd-114">Po zainstalowaniu agenta, można ukończyć procesu rejestracji, za pomocą następującego polecenia cmdlet programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="787bd-114">After installing the agent, you can complete the registration process using the following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="787bd-115">Sieć</span><span class="sxs-lookup"><span data-stu-id="787bd-115">Network</span></span>
<span data-ttu-id="787bd-116">**Pytanie: czy mam zapory, urządzenia sieciowego lub czegoś innego, która ogranicza maksymalny czas połączenia pozostają otwarte w sieci. Jak długo Moje próg limitu czasu po stronie klienta należy przy użyciu usługi Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="787bd-116">**Q: I have a firewall, network device, or something else that limits the maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="787bd-117">Całe oprogramowanie sieciowe, urządzenia fizyczne lub czymkolwiek innym, która ogranicza maksymalny czas połączenia może pozostawać otwarte, powinna używać progu co najmniej 5 minut (300 sekund) dla połączenia między serwerami, na którym jest zainstalowany klient programu Azure AD Connect i Usługa Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="787bd-117">All networking software, physical devices, or anything else that limits the maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between the server where the Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="787bd-118">Dotyczy to również wszystkich wydanych narzędzia synchronizacji pakietu Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="787bd-118">This also applies to all previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="787bd-119">**Pytanie: czy domeny drugiego poziomu (jednej etykiety domen) obsługiwane?**</span><span class="sxs-lookup"><span data-stu-id="787bd-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="787bd-120">Nie, usługi Azure AD Connect nie obsługuje lokalnymi lasami/domenami przy użyciu drugiego poziomu.</span><span class="sxs-lookup"><span data-stu-id="787bd-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="787bd-121">**Pytanie: czy "kropkami" o nazwie NetBios obsługiwane?**</span><span class="sxs-lookup"><span data-stu-id="787bd-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="787bd-122">Nie, usługi Azure AD Connect nie obsługuje lokalnymi lasami/domenami, których nazwa NetBios zawiera kropkę "." w nazwie.</span><span class="sxs-lookup"><span data-stu-id="787bd-122">No, Azure AD Connect does not support on-premises forests/domains where the NetBios name contains a period "." in the name.</span></span>

## <a name="federation"></a><span data-ttu-id="787bd-123">Federacyjna</span><span class="sxs-lookup"><span data-stu-id="787bd-123">Federation</span></span>
<span data-ttu-id="787bd-124">**Pytanie: co należy zrobić, jeśli otrzymuję wiadomość e-mail, który monit o odnawiania certyfikatu usługi Office 365**</span><span class="sxs-lookup"><span data-stu-id="787bd-124">**Q: What do I do if I receive an email that asking me to renew my Office 365 certificate**</span></span>  
<span data-ttu-id="787bd-125">Użyj wskazówek opisaną w [odnawiania certyfikatów](active-directory-aadconnect-o365-certs.md) temacie dotyczące sposobu odnawiania certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="787bd-125">Use the guidance that is outlined in the [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how to renew the certificate.</span></span>

<span data-ttu-id="787bd-126">**Pytanie: czy masz "Automatycznie Aktualizuj jednostki uzależnionej" dla jednostki uzależnionej usługi Office 365. Czy muszę wykonywać żadnych czynności w przypadku, gdy mój token certyfikatu podpisywania automatycznie najedzie na?**</span><span class="sxs-lookup"><span data-stu-id="787bd-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have to take any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="787bd-127">Użyj wskazówek opisaną w artykule [odnawiania certyfikatów](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="787bd-127">Use the guidance that is outlined in the article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="787bd-128">Środowisko</span><span class="sxs-lookup"><span data-stu-id="787bd-128">Environment</span></span>
<span data-ttu-id="787bd-129">**Q: Zmień nazwę serwera, po zainstalowaniu usługi Azure AD Connect jest obsługiwane?**</span><span class="sxs-lookup"><span data-stu-id="787bd-129">**Q: Is it supported to rename the server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="787bd-130">Nie.</span><span class="sxs-lookup"><span data-stu-id="787bd-130">No.</span></span> <span data-ttu-id="787bd-131">Zmiana nazwy serwera spowoduje, że aparat synchronizacji nie będą mogli nawiązywać połączeń z bazą danych SQL i usługa nie będzie możliwe jej uruchomienie.</span><span class="sxs-lookup"><span data-stu-id="787bd-131">Changing the server name will cause the sync engine to not be able to connect to the SQL database and the service will not be able to start.</span></span>

## <a name="identity-data"></a><span data-ttu-id="787bd-132">Danych tożsamości</span><span class="sxs-lookup"><span data-stu-id="787bd-132">Identity data</span></span>
<span data-ttu-id="787bd-133">**Pyt.: atrybut nazwy UPN (userPrincipalName) w usłudze Azure AD nie odpowiada UPN lokalnego — Dlaczego?**</span><span class="sxs-lookup"><span data-stu-id="787bd-133">**Q: The UPN (userPrincipalName) attribute in Azure AD does not match the on-prem UPN - why?**</span></span>  
<span data-ttu-id="787bd-134">Zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="787bd-134">See these articles:</span></span>

* [<span data-ttu-id="787bd-135">Niezgodne nazwy użytkowników w usłudze Office 365, Azure lub Intune lokalną nazwą UPN lub alternatywnym Identyfikatorem logowania</span><span class="sxs-lookup"><span data-stu-id="787bd-135">User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="787bd-136">Zmiany nie są synchronizowane przez narzędzie do synchronizacji usługi Azure Active Directory po zmianie nazwy UPN konta użytkownika, aby użyć innej domeny federacyjnej</span><span class="sxs-lookup"><span data-stu-id="787bd-136">Changes aren't synced by the Azure Active Directory Sync tool after you change the UPN of a user account to use a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="787bd-137">Można również skonfigurować usługi Azure AD, aby umożliwić aparatu synchronizacji można zaktualizować właściwości userPrincipalName zgodnie z opisem w [funkcji Usługa synchronizacji Azure AD Connect](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="787bd-137">You can also configure Azure AD to allow the sync engine to update the userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="787bd-138">**P: jest obsługiwane nietrwałego dopasowania grupy AD skontaktuj się z obiekty z istniejących obiektów usługi Azure AD grupy/skontaktuj się z lokalnymi?**</span><span class="sxs-lookup"><span data-stu-id="787bd-138">**Q: Is it supported to soft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="787bd-139">Nie jest to obecnie nieobsługiwane.</span><span class="sxs-lookup"><span data-stu-id="787bd-139">No, this is currently not supported.</span></span>

<span data-ttu-id="787bd-140">**Pytanie: czy jest ona obsługiwana na ręczne ustawienie atrybutu nazwę ImmutableId w istniejących obiektach Azure AD grupy/skontaktuj się z twardego dopasowanie do obiektów grupy AD skontaktuj się z lokalnymi?**</span><span class="sxs-lookup"><span data-stu-id="787bd-140">**Q: Is it supported to manually set ImmutableId attribute on existing Azure AD Group/Contact objects to hard match it to on-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="787bd-141">Nie jest to obecnie nieobsługiwane.</span><span class="sxs-lookup"><span data-stu-id="787bd-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="787bd-142">Konfiguracja niestandardowa</span><span class="sxs-lookup"><span data-stu-id="787bd-142">Custom configuration</span></span>
<span data-ttu-id="787bd-143">**Pytanie: gdzie są udokumentowane poleceń cmdlet programu PowerShell dla usługi Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="787bd-143">**Q: Where are the PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="787bd-144">Z wyjątkiem poleceń cmdlet opisane w tej lokacji innych poleceń cmdlet programu PowerShell znaleziono w programie Azure AD Connect nie są obsługiwane przez klienta.</span><span class="sxs-lookup"><span data-stu-id="787bd-144">With the exception of the cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="787bd-145">**Pytanie: czy można użyć "Serwera serwer eksportu/importu" znaleziony w *Menedżera usługi synchronizacji* na przenoszenie konfiguracji między serwerami?**</span><span class="sxs-lookup"><span data-stu-id="787bd-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* to move configuration between servers?**</span></span>  
<span data-ttu-id="787bd-146">Nie.</span><span class="sxs-lookup"><span data-stu-id="787bd-146">No.</span></span> <span data-ttu-id="787bd-147">Ta opcja nie pobierze wszystkie ustawienia konfiguracji i nie powinna być używana.</span><span class="sxs-lookup"><span data-stu-id="787bd-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="787bd-148">Zamiast tego należy użyć Kreatora tworzenia konfiguracji podstawowej na drugim serwerze i generowania skryptów programu PowerShell, aby przenieść wszystkie reguły niestandardowej między serwerami za pomocą edytora reguły synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="787bd-148">You should instead use the wizard to create the base configuration on the second server and use the sync rule editor to generate PowerShell scripts to move any custom rule between servers.</span></span> <span data-ttu-id="787bd-149">Zobacz [migracji w kierunku](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="787bd-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="787bd-150">**Pytanie: hasła można buforować Azure strony logowania i może to być zablokowana, ponieważ zawiera on element input hasła z automatycznego uzupełniania = "false" atrybutu?**</span><span class="sxs-lookup"><span data-stu-id="787bd-150">**Q: Can passwords be cached for the Azure sign-in page and can this be prevented since it contains a password input element with the autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="787bd-151">Obecnie nie obsługujemy modyfikowanie atrybutów HTML hasła pola wejściowego, tym autocomplete tag.</span><span class="sxs-lookup"><span data-stu-id="787bd-151">We currently do not support modifying the HTML attributes of the Password input field, including the autocomplete tag.</span></span> <span data-ttu-id="787bd-152">Obecnie pracujemy nad elementem, który umożliwia niestandardowych skryptów Javascript, której będzie można dodać atrybutu do pole hasła.</span><span class="sxs-lookup"><span data-stu-id="787bd-152">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="787bd-153">Powinna to być nowsze część 2017 r.</span><span class="sxs-lookup"><span data-stu-id="787bd-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="787bd-154">**Pytanie: czy w witrynie Azure logowania są wyświetlane nazwy użytkowników dla użytkowników, którzy wcześniej zalogowali się pomyślnie.  Można to zachowanie wyłączyć?**</span><span class="sxs-lookup"><span data-stu-id="787bd-154">**Q: On the Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="787bd-155">Obecnie nie obsługujemy modyfikowania atrybutów HTML strony logowania.</span><span class="sxs-lookup"><span data-stu-id="787bd-155">We currently do not support modifying the HTML attributes of the sign-in page.</span></span> <span data-ttu-id="787bd-156">Obecnie pracujemy nad elementem, który umożliwia niestandardowych skryptów Javascript, której będzie można dodać atrybutu do pole hasła.</span><span class="sxs-lookup"><span data-stu-id="787bd-156">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="787bd-157">Powinna to być nowsze część 2017 r.</span><span class="sxs-lookup"><span data-stu-id="787bd-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="787bd-158">**Pytanie: czy istnieje sposób, aby zapobiec równoczesnych sesji?**</span><span class="sxs-lookup"><span data-stu-id="787bd-158">**Q: Is there a way to prevent concurrent sessions?**</span></span></br>
<span data-ttu-id="787bd-159">Nie.</span><span class="sxs-lookup"><span data-stu-id="787bd-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="787bd-160">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="787bd-160">Troubleshooting</span></span>
<span data-ttu-id="787bd-161">**Pytanie: jak uzyskać pomoc dotyczącą usługi Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="787bd-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="787bd-162">Wyszukaj w bazie wiedzy Microsoft Knowledge Base (KB)</span><span class="sxs-lookup"><span data-stu-id="787bd-162">Search the Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="787bd-163">Wyszukiwanie Microsoft Knowledge Base (KB) dla techniczne rozwiązania typowych problemów naprawa w razie awarii o obsłudze programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="787bd-163">Search the Microsoft Knowledge Base (KB) for technical solutions to common break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="787bd-164">Fora dotyczące usługi Active Directory platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="787bd-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="787bd-165">Można wyszukiwać i wyszukać technicznych pytania i odpowiedzi od społeczności lub zadać pytanie własne klikając [tutaj](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="787bd-165">You can search and browse for technical questions and answers from the community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="787bd-166">Dział obsługi klienta usługi Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="787bd-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="787bd-167">Aby uzyskać pomoc techniczną za pośrednictwem portalu Azure, użyj tego łącza.</span><span class="sxs-lookup"><span data-stu-id="787bd-167">Use this link to get support through the Azure portal.</span></span>

