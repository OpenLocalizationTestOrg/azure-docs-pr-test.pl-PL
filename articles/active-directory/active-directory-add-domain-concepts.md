---
title: "Omówienie niestandardowych nazw domen w usłudze Azure Active Directory aaaConceptual | Dokumentacja firmy Microsoft"
description: "Wyjaśniono hello struktury koncepcyjny przy użyciu niestandardowych nazw domen w usłudze Azure Active directory, w tym federacyjnych dla rejestracji jednokrotnej"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fd0c5def-0da2-43af-81bc-76f4cfe86afd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 0a3454ae6b733a8a13a71925df3cc664063f388e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="conceptual-overview-of-custom-domain-names-in-azure-active-directory"></a>Poglądowe omówienie niestandardowych nazw domen w usłudze Azure Active Directory
Nazwa domeny może być identyfikator ważne w przypadku wielu zasobów katalogu w ramach:

* Użytkownik nazwy lub adresu e-mail użytkownika
* Witaj adres grupy
* Aplikacja Hello identyfikator URI dla aplikacji

Zasób w usłudze Azure Active Directory (Azure AD) może zawierać nazwy domeny, który jest już sprawdziła toobe należących do katalogu hello zawierającej hello zasobów. Tylko administrator globalny może wykonywać zadania zarządzania domeny w usłudze Azure AD.

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule. Aby uzyskać jak toomanage Twojego nazw domen w Centrum administracyjnym hello Azure AD, zobacz [Zarządzanie niestandardowych nazw domen w usłudze Azure Active Directory](active-directory-domains-manage-azure-portal.md).

Nazwy domen w usłudze Azure AD są globalnie unikatowe. Niestandardowej nazwy domeny mogą posłużyć tylko jeden dzierżawy usługi Azure AD w czasie. Jeśli jednego katalogu usługi Azure AD ma zweryfikować nazwę domeny, nie katalogu usługi Azure AD można sprawdzić lub użyć tej samej nazwy domeny.

## <a name="initial-and-custom-domain-names"></a>Nazwy domen początkowej i niestandardowych
Nazwa domeny, co w usłudze Azure AD jest początkową nazwę domeny lub niestandardowej nazwy domeny.

Co usługi Azure AD jest dostarczany z początkową nazwę domeny w hello formularza contoso.onmicrosoft.com. Ta nazwa trzeciego poziomu domeny, w tym przykładzie "contoso.onmicrosoft.com", został ustanowiony podczas hello katalog został utworzony, zazwyczaj przez administratora hello, który utworzył katalog hello. Witaj początkową nazwę domeny dla katalogu nie można zmienić ani usunąć. Hello początkową nazwę domeny, gdy funkcjonalnej, jest przeznaczony głównie toobe używane jako mechanizm bootstrapping do niestandardowej nazwy domeny jest sprawdzane.

W większości środowisk produkcyjnych katalog ma co najmniej jeden zweryfikowanej domeny niestandardowe, takie jak "contoso.com" i jest tej domeny niestandardowej, która jest widoczna tooend użytkowników. Niestandardowej nazwy domeny jest nazwą domeny, jest własnością i używane przez tę organizację, takich jak "contoso.com", do celów, takich jak hostingu swojej witryny sieci web. Ta nazwa domeny jest znanych tooemployees, ponieważ jest ona częścią hello nazwy użytkownika użyj toosign w sieci firmowej toohello lub toosend i pobrania poczty e-mail.

Przed mogą być używane przez usługę Azure AD, hello niestandardowa nazwa domeny musi być katalogiem tooyour dodany i zweryfikować.

## <a name="verified-and-unverified-domain-names"></a>Nazwy domeny zweryfikowane i niezweryfikowane
Witaj początkową nazwę domeny dla katalogu niejawnie jest oceniana jako zweryfikowane przez usługę Azure AD. Gdy administrator dodaje tooan nazwy domeny niestandardowej usługi Azure AD, jest początkowo w stanie niezweryfikowane. Usługi Azure AD nie zezwala na wszystkie toouse zasobów katalogu nazwa niezweryfikowanej domeny. Dzięki temu tylko jeden katalog można użyć nazwy określonej domeny, czy rzeczywiście że hello organizacji używa nazwy domeny hello jest właścicielem tej nazwy domeny.

Usługi Azure AD sprawdza własność nazwy domeny, wyszukując określonego wpisu w pliku strefy hello domeny name service (DNS) dla nazwy domeny hello. tooverify własność nazwy domeny, administrator pobiera wpis DNS hello z usługi Azure AD będzie szukać usługi Azure AD i dodają plik strefy DNS toohello wpis hello nazwy domeny. plik strefy DNS Hello jest obsługiwana przez hello rejestratora nazw domen dla tej domeny. tooverify kroki Hello domeny są wyświetlane w artykule hello [dodanie katalogu usługi Azure AD tooyour domeny niestandardowej](active-directory-add-domain.md).

Dodawanie pliku strefy toohello wpis DNS dla nazwy domeny hello nie ma wpływu na innych usług domenowych, takich jak adres e-mail lub Usługa hostingu sieci web.

## <a name="federated-and-managed-domain-names"></a>Nazwy domen federacyjnych i zarządzanie nimi
Niestandardowej nazwy domeny w usłudze Azure AD może być skonfigurowany toogive użytkowników logowania federacyjnego środowisko między lokalnymi usługi Active Directory i Azure AD. Skonfigurowanie domeny federacyjnej wymaga aktualizacji tooprivileged zasobów w usłudze Azure AD, a także tooyour usługi Active Directory systemu Windows Server. Konfigurowanie domeny federacyjnej musi zostać ukończone z usługi Azure AD Connect lub przy użyciu programu PowerShell. Nie można zainicjować federowania domeny niestandardowej z hello klasycznego portalu Azure. [Obejrzyj to toolearn wideo dotyczące konfigurowania usług AD FS dla użytkownika logują się przy użyciu usługi Azure AD Connect](http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect).

Domeny, które nie są federacyjnych są nazywane domen zarządzanych. Witaj domeny początkowej dla katalogu usługi Azure AD niejawnie jest szacowana jako domeny zarządzanej.

## <a name="primary-domain-names"></a>Nazwy domeny głównej
Witaj podstawowej nazwy domeny dla katalogu jest hello nazwy domeny, który jest wstępnie wybrane hello wartością domyślną dla części hello "domeny" hello nazwę użytkownika, gdy administrator tworzy nowego użytkownika w hello [portalu Azure](https://portal.azure.com/), lub innego portalu przykład portalu administracyjnego usługi Office 365 hello lub hello portalu Microsoft Intune. Katalog może mieć tylko jedną nazwę domeny głównej. Administrator może zmienić toobe nazwę domeny głównej hello zweryfikowanej domeny niestandardowej, która nie jest zintegrowany, ani toohello domeny początkowej.

## <a name="domain-names-in-azure-ad-and-other-microsoft-online-services"></a>Nazwy domen w usłudze Azure AD i innych usług Online firmy Microsoft
Należy zweryfikować nazwę domeny w usłudze Azure AD, zanim będzie można użyć innej usługi Online firmy Microsoft, takich jak Exchange Online, SharePoint Online i Intune. Inne usługi jest zwykle wymagają tooadd administratora wpisy DNS, które są toohello określonej usługi.

Własność tooverify mechanizmu własnej domeny korzysta z aplikacji sieci web platformy Azure. Należy zweryfikować domeny do użycia z usługą Azure AD, nawet wtedy, gdy wcześniej weryfikacji do użycia przez aplikację sieci web platformy Azure w ramach subskrypcji, która zależy od tej usługi Azure AD. Aplikacja sieci web platformy Azure można użyć nazwy domeny, która została zweryfikowana w innym katalogu z katalogu hello, która zabezpiecza hello aplikacji sieci web.

## <a name="managing-domain-names"></a>Zarządzanie nazwami domen
Można wykonać zadania zarządzania w domenie z hello klasycznego portalu Azure i programu PowerShell. Wiele zadań można wykonać przy użyciu interfejsu API Azure AD Graph hello.

* [Dodawanie i weryfikowanie niestandardowej nazwy domeny](active-directory-add-domain.md)
* [Zarządzanie domenami w hello klasycznego portalu Azure](active-directory-add-manage-domain-names.md)
* [Przy użyciu programu PowerShell toomanage domen w usłudze Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Przy użyciu nazwy domeny toomanage hello interfejsu API usługi Azure AD Graph w usłudze Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

