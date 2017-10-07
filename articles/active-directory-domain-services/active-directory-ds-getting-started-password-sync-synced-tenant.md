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
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>Włącz tooAzure synchronizacji haseł usług domenowych w usłudze Active Directory
W poprzednich zadaniach włączono usługi Azure Active Directory Domain Services dla dzierżawy usługi Azure Active Directory (Azure AD). następne zadanie Hello jest tooenable synchronizacji skrótów poświadczeń wymaganych dla NT LAN Manager (NTLM) i protokołu Kerberos tooAzure uwierzytelniania usług domenowych w usłudze AD. Po skonfigurowaniu synchronizacji poświadczeń użytkowników można zalogować toohello domeny zarządzanej przy użyciu poświadczeń firmowych.

etapy Hello są różne dla kont użytkowników programu vs konta użytkownika tylko do chmury, które są synchronizowane z katalogiem lokalnym za pomocą programu Azure AD Connect. Jeśli dzierżawy usługi Azure AD ma kombinację chmury tylko użytkownicy i użytkowników z lokalnej usługi AD, należy tooperform obu czynności.

<br>

> [!div class="op_single_selector"]
> * **Konta użytkowników tylko w chmurze**: [synchronizacji haseł dla kont użytkowników tylko w chmurze tooyour domeny zarządzanej](active-directory-ds-getting-started-password-sync.md)
> * **Lokalne konta użytkowników**: [synchronizacji haseł dla kont użytkowników synchronizowane z lokalnej domeny zarządzane AD tooyour](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a>Zadanie 5: Włączanie domeny zarządzanej tooyour synchronizacji haseł dla kont użytkowników synchronizowane z lokalnej usługi AD
A zsynchronizowane Azure AD dzierżawy ustawiono toosynchronize z katalogiem lokalnym w organizacji za pomocą usługi Azure AD Connect. Domyślnie program Azure AD Connect nie synchronizuje się NTLM i Kerberos tooAzure skróty poświadczeń AD. toouse usług domenowych Azure AD, należy tooconfigure Azure AD Connect toosynchronize skrótów poświadczeń wymaganych do uwierzytelniania NTLM i Kerberos. Witaj, wykonaj czynności włączenie synchronizacji skrótów poświadczeń wymaganych hello z dzierżawy usługi Azure AD tooyour katalogu lokalnego.

> [!NOTE]
> Jeśli Twoja organizacja ma kont użytkowników, które są synchronizowane z katalogu lokalnego, musisz włączyć synchronizację skrótów NTLM i Kerberos w domenie zarządzanej hello toouse kolejności. Konto użytkownika zsynchronizowanej to konto, które zostało utworzone w katalogu lokalnego i jest zsynchronizowanych tooyour dzierżawy usługi Azure AD za pomocą usługi Azure AD Connect.
>
>

### <a name="install-or-update-azure-ad-connect"></a>Instalowanie lub aktualizowanie programu Azure AD Connect
Zainstaluj najnowsze zalecane hello wersję programu Azure AD Connect w domenie przyłączony komputer. Jeśli masz istniejące wystąpienie Instalatora Azure AD Connect, należy tooupdate go toouse hello najnowszą wersję programu Azure AD Connect. tooavoid znanych problemów i błędów, które może już zostać naprawione, upewnij się, że należy zawsze używać najnowszej wersji hello programu Azure AD Connect.

**[Pobieranie programu Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**

Zalecana wersja: **1.1.553.0** — opublikowana 27 czerwca 2017 r.

> [!WARNING]
> Witaj, należy zainstalować najnowsze zalecane wersji programu Azure AD Connect tooenable hello haseł w starszej wersji (wymaganych do uwierzytelniania NTLM i Kerberos) poświadczenia toosynchronize tooyour usługi Azure AD dzierżawy. Ta funkcja nie jest dostępne w poprzednich wersjach programu Azure AD Connect lub hello starszej wersji narzędzia DirSync.
>
>

Instrukcje dotyczące instalacji programu Azure AD Connect są dostępne w następujących hello artykułu - [wprowadzenie do korzystania z usługi Azure AD Connect](../active-directory/active-directory-aadconnect.md)

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a>Włącz synchronizację NTLM i Kerberos tooAzure skróty poświadczeń AD
Wykonaj hello następującego skryptu programu PowerShell w każdym lesie usługi AD tooforce pełnej synchronizacji haseł i Włącz wszystkich użytkowników lokalnych poświadczeń skrótów toosync tooyour usługi Azure AD dzierżawy. Ten skrypt umożliwia hello skrótów poświadczeń wymaganych do dzierżawy zsynchronizowane tooyour usługi Azure AD toobe uwierzytelniania NTLM/Kerberos.

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

W zależności od rozmiaru hello katalogu (liczby użytkowników, grup itp.), synchronizacja poświadczeń skróty tooAzure AD jest czasochłonne. Witaj haseł będzie można korzystać w domenie zarządzanej usług domenowych Azure AD hello wkrótce po zsynchronizowaniu skrótów poświadczeń hello tooAzure AD.

<br>

## <a name="related-content"></a>Powiązana zawartość
* [Włącz tooAAD synchronizacji haseł usługi domenowe dla tylko w chmurze platformy Azure AD directory](active-directory-ds-getting-started-password-sync.md)
* [Administrowanie domeną zarządzaną usług Azure AD Domain Services](active-directory-ds-admin-guide-administer-domain.md)
* [Przyłączanie się do systemu Windows maszyny wirtualnej tooan usług domenowych Azure AD zarządzanej domeny](active-directory-ds-admin-guide-join-windows-vm.md)
* [Przyłącz do Red Hat Enterprise Linux maszyny wirtualnej tooan usług domenowych Azure AD zarządzanej domeny](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
