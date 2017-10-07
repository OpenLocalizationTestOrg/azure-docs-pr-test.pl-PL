---
title: aaaAzure AD Connect i Federacji | Dokumentacja firmy Microsoft
description: "Ta strona jest hello centralną lokalizację dla wszystkich dokumentację dotyczącą operacji usług AD FS, które używają usługi Azure AD Connect."
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: f9107cf5-0131-499a-9edf-616bf3afef4d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: anandy
ms.openlocfilehash: dc70206eee2296c2320712ef2ade48ccebcc912d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-and-federation"></a>Program Azure AD Connect a federacja
Azure umożliwia połączenia usługi Active Directory (Azure AD), konfigurowanie federacji z lokalnej usługi Active Directory Federation Services (AD FS) i Azure AD. Z federacyjnego logowania można włączyć toosign użytkowników w usługach AD na podstawie tooAzure ich hasłami lokalnymi--i, znajduje się w sieci firmowej hello, bez konieczności tooenter ponownie swoje hasła. Przy użyciu opcji federacyjnego hello z usługami AD FS, można wdrażać nowej instalacji usług AD FS, lub można określić istniejącą instalację w farmie programu Windows Server 2012 R2.

Ten temat jest hello macierzystego dla informacji o funkcji związanych z federacyjnych Azure AD Connect. Zawiera także łącza tooall Tematy pokrewne. Dla łącza tooAzure AD Connect, zobacz [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

## <a name="azure-ad-connect-federation-topics"></a>Azure AD Connect: tematy federacyjnych
| Temat | Co obejmuje i kiedy tooread go |
|:--- |:--- |
| **Azure AD Connect użytkownika opcje logowania** | |
| [Zrozumienie opcje logowania użytkowników](active-directory-aadconnect-user-signin.md) |Poznaj różne opcje logowania użytkowników i ich wpływ na środowisko użytkownika hello Azure logowania. |
| **Instalowanie usług AD FS przy użyciu usługi Azure AD Connect** | |
| [Wymagania wstępne](active-directory-aadconnect-get-started-custom.md#ad-fs-configuration-pre-requisites) |Zobacz wymagania wstępne hello do pomyślnej instalacji usług AD FS za pomocą usługi Azure AD Connect. |
| [Konfigurowanie farmy usług AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs) |Instalowanie nowej farmy usług AD FS przy użyciu usługi Azure AD Connect. |
| [Utworzenie federacji z usługą Azure AD przy użyciu alternatywnego Identyfikatora logowania](active-directory-aadconnect-federation-management.md#alternateid) | Konfigurowanie Federacji przy użyciu alternatywnego Identyfikatora logowania  |
| **Modyfikowanie hello AD FS konfiguracji** | |
| [Napraw hello zaufania](active-directory-aadconnect-federation-management.md#repairthetrust) |Napraw hello bieżącego zaufania między lokalnymi usług AD FS i Office 365/Azure. |
| [Dodawanie nowego serwera usług AD FS](active-directory-aadconnect-federation-management.md#addadfsserver) |Po wstępnej instalacji, rozwiń węzeł farmy usług AD FS jest dodatkowy serwer usług AD FS. |
| [Dodaj nowy serwer AD FS WAP](active-directory-aadconnect-federation-management.md#addwapserver) |Rozwiń węzeł farmy usług AD FS jest dodatkowy serwer Proxy aplikacji sieci Web (WAP) po wstępnej instalacji. |
| [Dodaj nową domenę federacyjnych](active-directory-aadconnect-federation-management.md#addfeddomain) |Dodaj inny toobe domeny Sfederowanych z usługą Azure AD. |
| [Certyfikat SSL hello aktualizacji](active-directory-aadconnectfed-ssl-update.md)| Zaktualizuj hello certyfikat protokołu SSL dla farmy usług AD FS. |
| **Inna konfiguracja federacyjna** | |
| [Federowanie wielu wystąpień usługi Azure AD przy użyciu jednego wystąpienia usług AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md) | Federację wielu usługi Azure AD z jednym farmy usług AD FS| 
| [Dodać logo firmy/ilustracji](active-directory-aadconnect-federation-management.md#customlogo) |Zmodyfikuj hello logowania, określając hello niestandardowe logo, które jest wyświetlany na stronie powitania AD FS logowania. |
| [Dodaj opis logowania](active-directory-aadconnect-federation-management.md#addsignindescription) |Zmień hello opisu logowania na stronę logowania w hello usług AD FS. |
| [Modyfikowanie reguł oświadczeń usług AD FS](active-directory-aadconnect-federation-management.md#modclaims) |Modyfikowanie lub dodawanie reguł oświadczeń w usługach AD FS, który odpowiada konfiguracji synchronizacji tooAzure AD Connect. |


## <a name="additional-resources"></a>Dodatkowe zasoby
* [Federowania dwie usługi Azure AD z jednym usług AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md)
* [Wdrażanie usług AD FS w systemie Azure](active-directory-aadconnect-azure-adfs.md)
* [Wysokiej dostępności geograficznej między AD FS wdrożenia na platformie Azure z usługą Azure Traffic Manager](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)
