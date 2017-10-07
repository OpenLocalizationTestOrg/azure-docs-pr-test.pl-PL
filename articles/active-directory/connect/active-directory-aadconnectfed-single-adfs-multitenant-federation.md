---
title: "aaaFederating wielu usługi Azure AD z jednym usług AD FS | Dokumentacja firmy Microsoft"
description: "W tym dokumencie przedstawiono sposób toofederate wielu usługi Azure AD z jednym usług AD FS."
keywords: federate, ADFS, AD FS, multiple tenants, single AD FS, one ADFS, multi-tenant federation, multi-forest adfs, aad connect, federation, cross-tenant federation
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 442192896b3b13f7bf9388396cd3769e194329d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a>Federowanie wielu wystąpień usługi Azure AD przy użyciu jednego wystąpienia usługi AD FS

Pojedyncza farma usługi AD FS o wysokiej dostępności może federować wiele lasów, jeśli istnieje między nimi dwukierunkowa relacja zaufania. Wiele lasów może lub nie może odpowiadać toohello usługi Azure Active Directory. Ten artykuł zawiera instrukcje jak tooconfigure federacji między pojedynczego wdrożenia usług AD FS i więcej niż jeden lasach toodifferent tej synchronizacji usługi Azure AD.

![Federacja wielu dzierżaw z jedną usługą AD FS](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> W tym scenariuszu nie jest obsługiwane zapisywanie zwrotne urządzeń ani automatyczne dołączanie urządzeń.

> [!NOTE]
> Azure AD Connect nie może być federacyjnego tooconfigure używane w tym scenariuszu, jak Azure AD Connect można skonfigurować Federacji domen w jednej usłudze Azure AD.

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a>Kroki umożliwiające federowanie usługi AD FS z wieloma usługami Azure AD

Należy rozważyć domeny contoso.com w usłudze Azure Active Directory contoso.onmicrosoft.com już jest Sfederowane przy użyciu hello usług AD FS lokalnie zainstalowane w środowisku usługi Active Directory lokalnymi contoso.com. Fabrikam.com to domena w usłudze Azure Active Directory fabrikam.onmicrosoft.com.

##<a name="step-1-establish-a-two-way-trust"></a>Krok 1. Ustanów dwukierunkową relację zaufania
 
Usługi AD FS w użytkownicy mogli tooauthenticate toobe contoso.com fabrikam.com potrzeby dwukierunkową relację zaufania między contoso.com i fabrikam.com. Wykonaj wytyczne hello na tym [artykułu](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello dwukierunkowe zaufanie.
 
##<a name="step-2-modify-contosocom-federation-settings"></a>Krok 2. Zmodyfikuj ustawienia federacji domeny contoso.com 
 
Witaj wystawca domyślne ustawiony tooAD pojedynczej domeny federacyjnej FS jest "http://ADFSServiceFQDN/adfs/services/trust", na przykład "http://fs.contoso.com/adfs/services/trust". Usługa Azure Active Directory wymaga unikatowego wystawcy dla każdej domeny federacyjnej. Ponieważ hello tej samej usługi AD FS będzie toofederate dwie domeny, wartości wystawcy hello musi toobe zmodyfikować tak, aby jest unikatowa dla każdej domeny usług AD FS federates w usłudze Azure Active Directory. 
 
Na serwerze hello usług AD FS Otwórz program Azure AD PowerShell i wykonaj hello następujące kroki:
 
Połącz toohello usługi Azure Active Directory zawierającą hello domeny contoso.com Connect MsolService hello federacyjnego ustawienia aktualizacji dla domeny contoso.com Update MsolFederatedDomain - DomainName contoso.com — SupportMultipleDomain
 
Wystawca w ustawienia Federacji domen hello zostaną zmienione za "http://contoso.com/adfs/services/trust" i wystawiania oświadczenia, reguła zostanie dodany do hello Azure AD zaufania jednostki uzależnionej tooissue hello poprawną wartość issuerId oparta na powitania sufiks nazwy UPN.
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a>Krok 3. Sfederuj domenę fabrikam.com z usługą AD FS
 
W programie Azure AD powershell sesja wykonać hello następujące kroki: Połącz tooAzure usługi Active Directory zawiera hello fabrikam.com domeny

    Connect-MsolService
Konwertuj toofederated domeny fabrikam.com zarządzane hello:

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
Witaj powyżej operacji będzie Federację hello fabrikam.com domeny z hello tej samej usługi AD FS. Ustawienia domeny hello można sprawdzić, za pomocą Get MsolDomainFederationSettings dla obu domen.

## <a name="next-steps"></a>Następne kroki
[Łączenie usługi Active Directory z usługą Azure Active Directory](active-directory-aadconnect.md)
