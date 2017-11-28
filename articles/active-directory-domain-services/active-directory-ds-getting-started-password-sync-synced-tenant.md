---
title: "Azure AD Domain Services: włączanie synchronizacji haseł | Microsoft Docs"
description: "Wprowadzenie do usługi Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: a7a6ee0f83d3d9bdaf236717efb39155a26934e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="f17c8-103">Włącz tooAzure synchronizacji haseł usług domenowych w usłudze Active Directory</span><span class="sxs-lookup"><span data-stu-id="f17c8-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="f17c8-104">W poprzednich zadaniach włączono usługi Azure Active Directory Domain Services dla dzierżawy usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f17c8-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="f17c8-105">następne zadanie Hello jest tooenable synchronizacji skrótów poświadczeń wymaganych dla NT LAN Manager (NTLM) i protokołu Kerberos tooAzure uwierzytelniania usług domenowych w usłudze AD.</span><span class="sxs-lookup"><span data-stu-id="f17c8-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="f17c8-106">Po skonfigurowaniu synchronizacji poświadczeń użytkowników można zalogować toohello domeny zarządzanej przy użyciu poświadczeń firmowych.</span><span class="sxs-lookup"><span data-stu-id="f17c8-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="f17c8-107">etapy Hello są różne dla kont użytkowników programu vs konta użytkownika tylko do chmury, które są synchronizowane z katalogiem lokalnym za pomocą programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f17c8-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="f17c8-108">Jeśli dzierżawy usługi Azure AD ma kombinację chmury tylko użytkownicy i użytkowników z lokalnej usługi AD, należy tooperform obu czynności.</span><span class="sxs-lookup"><span data-stu-id="f17c8-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="f17c8-109">**Konta użytkowników tylko w chmurze**: [synchronizacji haseł dla kont użytkowników tylko w chmurze tooyour domeny zarządzanej](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="f17c8-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="f17c8-110">**Lokalne konta użytkowników**: [synchronizacji haseł dla kont użytkowników synchronizowane z lokalnej domeny zarządzane AD tooyour](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="f17c8-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a><span data-ttu-id="f17c8-111">Zadanie 5: Włączanie domeny zarządzanej tooyour synchronizacji haseł dla kont użytkowników synchronizowane z lokalnej usługi AD</span><span class="sxs-lookup"><span data-stu-id="f17c8-111">Task 5: enable password synchronization tooyour managed domain for user accounts synced with your on-premises AD</span></span>
<span data-ttu-id="f17c8-112">A zsynchronizowane Azure AD dzierżawy ustawiono toosynchronize z katalogiem lokalnym w organizacji za pomocą usługi Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f17c8-112">A synced Azure AD tenant is set toosynchronize with your organization's on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="f17c8-113">Domyślnie program Azure AD Connect nie synchronizuje się NTLM i Kerberos tooAzure skróty poświadczeń AD.</span><span class="sxs-lookup"><span data-stu-id="f17c8-113">By default, Azure AD Connect does not synchronize NTLM and Kerberos credential hashes tooAzure AD.</span></span> <span data-ttu-id="f17c8-114">toouse usług domenowych Azure AD, należy tooconfigure Azure AD Connect toosynchronize skrótów poświadczeń wymaganych do uwierzytelniania NTLM i Kerberos.</span><span class="sxs-lookup"><span data-stu-id="f17c8-114">toouse Azure AD Domain Services, you need tooconfigure Azure AD Connect toosynchronize credential hashes required for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="f17c8-115">Witaj, wykonaj czynności włączenie synchronizacji skrótów poświadczeń wymaganych hello z dzierżawy usługi Azure AD tooyour katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="f17c8-115">hello following steps enable synchronization of hello required credential hashes from your on-premises directory tooyour Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="f17c8-116">Jeśli Twoja organizacja ma kont użytkowników, które są synchronizowane z katalogu lokalnego, musisz włączyć synchronizację skrótów NTLM i Kerberos w domenie zarządzanej hello toouse kolejności.</span><span class="sxs-lookup"><span data-stu-id="f17c8-116">If your organization has user accounts that are synchronized from your on-premises directory, your must enable synchronization of NTLM and Kerberos hashes in order toouse hello managed domain.</span></span> <span data-ttu-id="f17c8-117">Konto użytkownika zsynchronizowanej to konto, które zostało utworzone w katalogu lokalnego i jest zsynchronizowanych tooyour dzierżawy usługi Azure AD za pomocą usługi Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f17c8-117">A synced user account is an account that was created in your on-premises directory and is synchronized tooyour Azure AD tenant using Azure AD Connect.</span></span>
>
>

### <a name="install-or-update-azure-ad-connect"></a><span data-ttu-id="f17c8-118">Instalowanie lub aktualizowanie programu Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="f17c8-118">Install or update Azure AD Connect</span></span>
<span data-ttu-id="f17c8-119">Zainstaluj najnowsze zalecane hello wersję programu Azure AD Connect w domenie przyłączony komputer.</span><span class="sxs-lookup"><span data-stu-id="f17c8-119">Install hello latest recommended release of Azure AD Connect on a domain joined computer.</span></span> <span data-ttu-id="f17c8-120">Jeśli masz istniejące wystąpienie Instalatora Azure AD Connect, należy tooupdate go toouse hello najnowszą wersję programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f17c8-120">If you have an existing instance of Azure AD Connect setup, you need tooupdate it toouse hello latest version of Azure AD Connect.</span></span> <span data-ttu-id="f17c8-121">tooavoid znanych problemów i błędów, które może już zostać naprawione, upewnij się, że należy zawsze używać najnowszej wersji hello programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f17c8-121">tooavoid known issues/bugs that may have already been fixed, ensure you always use hello latest version of Azure AD Connect.</span></span>

<span data-ttu-id="f17c8-122">**[Pobieranie programu Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span><span class="sxs-lookup"><span data-stu-id="f17c8-122">**[Download Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span></span>

<span data-ttu-id="f17c8-123">Zalecana wersja: **1.1.553.0** — opublikowana 27 czerwca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="f17c8-123">Recommended version: **1.1.553.0** - published on June 27, 2017.</span></span>

> [!WARNING]
> <span data-ttu-id="f17c8-124">Witaj, należy zainstalować najnowsze zalecane wersji programu Azure AD Connect tooenable hello haseł w starszej wersji (wymaganych do uwierzytelniania NTLM i Kerberos) poświadczenia toosynchronize tooyour usługi Azure AD dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="f17c8-124">You MUST install hello latest recommended release of Azure AD Connect tooenable hello legacy password credentials (required for NTLM and Kerberos authentication) toosynchronize tooyour Azure AD tenant.</span></span> <span data-ttu-id="f17c8-125">Ta funkcja nie jest dostępne w poprzednich wersjach programu Azure AD Connect lub hello starszej wersji narzędzia DirSync.</span><span class="sxs-lookup"><span data-stu-id="f17c8-125">This functionality is not available in prior releases of Azure AD Connect or with hello legacy DirSync tool.</span></span>
>
>

<span data-ttu-id="f17c8-126">Instrukcje dotyczące instalacji programu Azure AD Connect są dostępne w następujących hello artykułu - [wprowadzenie do korzystania z usługi Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="f17c8-126">Installation instructions for Azure AD Connect are available in hello following article - [Getting started with Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span></span>

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a><span data-ttu-id="f17c8-127">Włącz synchronizację NTLM i Kerberos tooAzure skróty poświadczeń AD</span><span class="sxs-lookup"><span data-stu-id="f17c8-127">Enable synchronization of NTLM and Kerberos credential hashes tooAzure AD</span></span>
<span data-ttu-id="f17c8-128">Wykonaj hello następującego skryptu programu PowerShell w każdym lesie usługi AD tooforce pełnej synchronizacji haseł i Włącz wszystkich użytkowników lokalnych poświadczeń skrótów toosync tooyour usługi Azure AD dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="f17c8-128">Execute hello following PowerShell script on each AD forest, tooforce full password synchronization, and enable all on-premises users’ credential hashes toosync tooyour Azure AD tenant.</span></span> <span data-ttu-id="f17c8-129">Ten skrypt umożliwia hello skrótów poświadczeń wymaganych do dzierżawy zsynchronizowane tooyour usługi Azure AD toobe uwierzytelniania NTLM/Kerberos.</span><span class="sxs-lookup"><span data-stu-id="f17c8-129">This script enables hello credential hashes required for NTLM/Kerberos authentication toobe synchronized tooyour Azure AD tenant.</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"  
$azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"  
Import-Module adsync  
$c = Get-ADSyncConnector -Name $adConnector  
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1  
$c.GlobalParameters.Remove($p.Name)  
$c.GlobalParameters.Add($p)  
$c = Add-ADSyncConnector -Connector $c  
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false   
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true  
```

<span data-ttu-id="f17c8-130">W zależności od rozmiaru hello katalogu (liczby użytkowników, grup itp.), synchronizacja poświadczeń skróty tooAzure AD jest czasochłonne.</span><span class="sxs-lookup"><span data-stu-id="f17c8-130">Depending on hello size of your directory (number of users, groups etc.), synchronization of credential hashes tooAzure AD takes time.</span></span> <span data-ttu-id="f17c8-131">Witaj haseł będzie można korzystać w domenie zarządzanej usług domenowych Azure AD hello wkrótce po zsynchronizowaniu skrótów poświadczeń hello tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="f17c8-131">hello passwords will be usable on hello Azure AD Domain Services managed domain shortly after hello credential hashes have synchronized tooAzure AD.</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="f17c8-132">Powiązana zawartość</span><span class="sxs-lookup"><span data-stu-id="f17c8-132">Related Content</span></span>
* [<span data-ttu-id="f17c8-133">Włącz tooAAD synchronizacji haseł usługi domenowe dla tylko w chmurze platformy Azure AD directory</span><span class="sxs-lookup"><span data-stu-id="f17c8-133">Enable password synchronization tooAAD Domain Services for a cloud-only Azure AD directory</span></span>](active-directory-ds-getting-started-password-sync.md)
* [<span data-ttu-id="f17c8-134">Administrowanie domeną zarządzaną usług Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="f17c8-134">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="f17c8-135">Przyłączanie się do systemu Windows maszyny wirtualnej tooan usług domenowych Azure AD zarządzanej domeny</span><span class="sxs-lookup"><span data-stu-id="f17c8-135">Join a Windows virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="f17c8-136">Przyłącz do Red Hat Enterprise Linux maszyny wirtualnej tooan usług domenowych Azure AD zarządzanej domeny</span><span class="sxs-lookup"><span data-stu-id="f17c8-136">Join a Red Hat Enterprise Linux virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
