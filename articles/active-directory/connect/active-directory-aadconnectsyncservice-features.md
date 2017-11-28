---
title: Synchronizacja Connect aaaAzure AD service funkcji i konfiguracji | Dokumentacja firmy Microsoft
description: "Zawiera opis funkcji po stronie usługi dla usługi synchronizacji programu Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="243c8-103">Funkcje usługi synchronizacji programu Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="243c8-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="243c8-104">Witaj funkcji synchronizacji programu Azure AD Connect zawiera dwa składniki:</span><span class="sxs-lookup"><span data-stu-id="243c8-104">hello synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="243c8-105">Witaj lokalnymi składnika o nazwie **synchronizacja programu Azure AD Connect**, nazywany również **aparatu synchronizacji**.</span><span class="sxs-lookup"><span data-stu-id="243c8-105">hello on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="243c8-106">Usługa Hello znajdującej się w usłudze Azure AD, znanej także jako **usługi synchronizacji programu Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="243c8-106">hello service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="243c8-107">W tym temacie wyjaśniono, jak hello następujące funkcje programu hello **usługi synchronizacji programu Azure AD Connect** pracy i jak można je również skonfigurować za pomocą środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="243c8-107">This topic explains how hello following features of hello **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="243c8-108">Te ustawienia są konfigurowane przez hello [Azure Active Directory modułu dla środowiska Windows PowerShell](http://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="243c8-108">These settings are configured by hello [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="243c8-109">Pobierz i zainstaluj go niezależnie od Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="243c8-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="243c8-110">polecenia cmdlet Hello opisane w niniejszym dokumencie zostały wprowadzone w hello [wersji marca 2016 (kompilacja 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="243c8-110">hello cmdlets documented in this topic were introduced in hello [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="243c8-111">Jeśli nie masz hello poleceń cmdlet w tym temacie lub tworzy hello sam wyniku, a następnie upewnij się, że możesz uruchomić hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="243c8-111">If you do not have hello cmdlets documented in this topic or they do not produce hello same result, then make sure you run hello latest version.</span></span>

<span data-ttu-id="243c8-112">Konfiguracja hello toosee w katalogu usługi Azure AD, uruchom `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="243c8-112">toosee hello configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="243c8-113">![Get-MsolDirSyncFeatures wyników](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="243c8-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="243c8-114">Wiele z tych ustawień można zmienić tylko przy użyciu usługi Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="243c8-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="243c8-115">Witaj następujące ustawienia można skonfigurować przy `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="243c8-115">hello following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="243c8-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="243c8-116">DirSyncFeature</span></span> | <span data-ttu-id="243c8-117">Komentarz</span><span class="sxs-lookup"><span data-stu-id="243c8-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="243c8-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="243c8-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="243c8-119">Umożliwia toojoin obiektów userPrincipalName dodanie adresu tooprimary SMTP.</span><span class="sxs-lookup"><span data-stu-id="243c8-119">Allows objects toojoin on userPrincipalName in addition tooprimary SMTP address.</span></span> |
| [<span data-ttu-id="243c8-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="243c8-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="243c8-121">Umożliwia atrybutu userPrincipalName hello tooupdate aparatu synchronizacji hello zarządzane licencjonowanych użytkowników (niefederacyjnych).</span><span class="sxs-lookup"><span data-stu-id="243c8-121">Allows hello sync engine tooupdate hello userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="243c8-122">Po włączeniu funkcji nie można wyłączyć ponownie.</span><span class="sxs-lookup"><span data-stu-id="243c8-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="243c8-123">Z 24 sierpnia 2016 hello funkcji *zduplikowany atrybut odporności* jest domyślnie włączona dla nowej usługi Azure AD katalogów.</span><span class="sxs-lookup"><span data-stu-id="243c8-123">From August 24, 2016 hello feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="243c8-124">Ta funkcja będzie również wprowadzanie i włączone na katalogi utworzone przed tą datą.</span><span class="sxs-lookup"><span data-stu-id="243c8-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="243c8-125">Otrzymasz wiadomość e-mail z powiadomieniem po katalogu o tooget ta funkcja jest włączona.</span><span class="sxs-lookup"><span data-stu-id="243c8-125">You will receive an email notification when your directory is about tooget this feature enabled.</span></span>
> 
> 

<span data-ttu-id="243c8-126">Witaj następujące ustawienia są skonfigurowane przy użyciu usługi Azure AD Connect i nie można zmodyfikować przez `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="243c8-126">hello following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="243c8-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="243c8-127">DirSyncFeature</span></span> | <span data-ttu-id="243c8-128">Komentarz</span><span class="sxs-lookup"><span data-stu-id="243c8-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="243c8-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="243c8-129">DeviceWriteback</span></span> |[<span data-ttu-id="243c8-130">Azure AD Connect: Włączanie zapisywania zwrotnego urządzeń</span><span class="sxs-lookup"><span data-stu-id="243c8-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="243c8-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="243c8-131">DirectoryExtensions</span></span> |[<span data-ttu-id="243c8-132">Synchronizacja programu Azure AD Connect: rozszerzenia katalogów</span><span class="sxs-lookup"><span data-stu-id="243c8-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="243c8-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="243c8-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="243c8-134">Umożliwia toobe atrybutu poddane kwarantannie, gdy jest duplikatem innego obiektu, a nie awarii całego obiektu hello podczas eksportowania.</span><span class="sxs-lookup"><span data-stu-id="243c8-134">Allows an attribute toobe quarantined when it is a duplicate of another object rather than failing hello entire object during export.</span></span> |
| <span data-ttu-id="243c8-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="243c8-135">PasswordSync</span></span> |[<span data-ttu-id="243c8-136">Implementowanie synchronizacji haseł z synchronizacji Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="243c8-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="243c8-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="243c8-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="243c8-138">Podglądu: Zapisywanie zwrotne grup</span><span class="sxs-lookup"><span data-stu-id="243c8-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="243c8-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="243c8-139">UserWriteback</span></span> |<span data-ttu-id="243c8-140">Nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="243c8-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="243c8-141">Zduplikowany atrybut odporności</span><span class="sxs-lookup"><span data-stu-id="243c8-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="243c8-142">Zamiast niepowodzeniem tooprovision obiekty z zduplikowane nazwy UPN / proxyAddresses, zduplikowany atrybut hello jest "poddane kwarantannie" i przypisano wartości tymczasowej.</span><span class="sxs-lookup"><span data-stu-id="243c8-142">Instead of failing tooprovision objects with duplicate UPNs / proxyAddresses, hello duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="243c8-143">Po rozwiązaniu konfliktu hello hello tymczasowej nazwy UPN jest zmieniany automatycznie toohello poprawnej wartości.</span><span class="sxs-lookup"><span data-stu-id="243c8-143">When hello conflict is resolved, hello temporary UPN is changed toohello proper value automatically.</span></span> <span data-ttu-id="243c8-144">Aby uzyskać więcej informacji, zobacz [tożsamości synchronizacji i zduplikowany atrybut odporności](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="243c8-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="243c8-145">UserPrincipalName nietrwałego dopasowania</span><span class="sxs-lookup"><span data-stu-id="243c8-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="243c8-146">Gdy ta funkcja jest włączona, soft-match jest włączone dla nazwy UPN w toohello dodanie [podstawowego adresu SMTP](https://support.microsoft.com/kb/2641663), który jest zawsze włączona.</span><span class="sxs-lookup"><span data-stu-id="243c8-146">When this feature is enabled, soft-match is enabled for UPN in addition toohello [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="243c8-147">Soft-match jest używane toomatch istniejących użytkowników chmury w usłudze Azure AD z lokalnymi użytkownikami.</span><span class="sxs-lookup"><span data-stu-id="243c8-147">Soft-match is used toomatch existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="243c8-148">Jeśli potrzebujesz toomatch lokalnych kont usługi AD z istniejących kont utworzonych w chmurze hello nie używasz usługi Exchange Online, a następnie ta funkcja jest przydatna.</span><span class="sxs-lookup"><span data-stu-id="243c8-148">If you need toomatch on-premises AD accounts with existing accounts created in hello cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="243c8-149">W tym scenariuszu zwykle nie masz atrybutem Przyczyna tooset hello SMTP w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="243c8-149">In this scenario, you generally don’t have a reason tooset hello SMTP attribute in hello cloud.</span></span>

<span data-ttu-id="243c8-150">Ta funkcja jest na domyślnie dla nowo utworzone katalogów usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="243c8-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="243c8-151">Możesz sprawdzić, czy ta funkcja jest włączona dla Ciebie, uruchamiając:</span><span class="sxs-lookup"><span data-stu-id="243c8-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="243c8-152">Jeśli ta funkcja nie jest włączona dla katalogu usługi Azure AD, następnie możesz je włączyć, uruchamiając:</span><span class="sxs-lookup"><span data-stu-id="243c8-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="243c8-153">Synchronizowanie aktualizacji userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="243c8-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="243c8-154">W przeszłości atrybutu UserPrincipalName toohello aktualizacje przy użyciu usługi synchronizacji hello z lokalnymi został zablokowany, chyba że oba te warunki są spełnione:</span><span class="sxs-lookup"><span data-stu-id="243c8-154">Historically, updates toohello UserPrincipalName attribute using hello sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="243c8-155">Użytkownik Hello jest zarządzany (niefederacyjnych).</span><span class="sxs-lookup"><span data-stu-id="243c8-155">hello user is managed (non-federated).</span></span>
* <span data-ttu-id="243c8-156">Witaj użytkownika nie ma przypisanej licencji.</span><span class="sxs-lookup"><span data-stu-id="243c8-156">hello user has not been assigned a license.</span></span>

<span data-ttu-id="243c8-157">Aby uzyskać więcej informacji, zobacz [użytkownika nazwy w usłudze Office 365, Azure lub Intune nie są zgodne hello lokalną nazwą UPN lub alternatywnym Identyfikatorem logowania](https://support.microsoft.com/kb/2523192).</span><span class="sxs-lookup"><span data-stu-id="243c8-157">For more details, see [User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="243c8-158">Włączenie tej funkcji umożliwia hello synchronizacji aparat tooupdate hello userPrincipalName, gdy jest zmienione lokalnymi i użyciu synchronizacji haseł. Jeśli używasz federacyjnych, ta funkcja nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="243c8-158">Enabling this feature allows hello sync engine tooupdate hello userPrincipalName when it is changed on-premises and you use password sync. If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="243c8-159">Ta funkcja jest na domyślnie dla nowo utworzone katalogów usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="243c8-159">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="243c8-160">Możesz sprawdzić, czy ta funkcja jest włączona dla Ciebie, uruchamiając:</span><span class="sxs-lookup"><span data-stu-id="243c8-160">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="243c8-161">Jeśli ta funkcja nie jest włączona dla katalogu usługi Azure AD, następnie możesz je włączyć, uruchamiając:</span><span class="sxs-lookup"><span data-stu-id="243c8-161">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="243c8-162">Po włączeniu tej funkcji, zostaną one istniejące wartości userPrincipalName — jest.</span><span class="sxs-lookup"><span data-stu-id="243c8-162">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="243c8-163">Dla następnej zmiany hello userPrincipalName atrybutu lokalnymi synchronizacja różnicowa normalne hello na użytkowników spowoduje zaktualizowanie hello głównej nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="243c8-163">On next change of hello userPrincipalName attribute on-premises, hello normal delta sync on users will update hello UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="243c8-164">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="243c8-164">See also</span></span>
* [<span data-ttu-id="243c8-165">Synchronizacja programu Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="243c8-165">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="243c8-166">[Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="243c8-166">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

