---
title: "Azure Active Directory Domain Services: Włącz ograniczone delegowanie protokołu kerberos | Dokumentacja firmy Microsoft"
description: "Włącz ograniczone delegowanie protokołu kerberos w domenach zarządzanych usług domenowych Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d32547c8018dd1f99c992e95a01d2711d460a261
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-kerberos-constrained-delegation-kcd-on-a-managed-domain"></a>Skonfiguruj ograniczone delegowanie protokołu kerberos (KCD) do domeny zarządzanej
Wiele aplikacji potrzebne zasoby tooaccess w kontekście hello hello użytkownika. Usługa Active Directory obsługuje mechanizm delegowania protokołu Kerberos, co umożliwia przypadek użycia wywołuje. Ponadto można ograniczyć delegowania tak, aby tylko określonych zasobów można uzyskać w kontekście hello hello użytkownika. Azure domen zarządzanych w usługach domenowych AD różnią się od tradycyjnych domen usługi Active Directory, ponieważ są one bardziej bezpieczny sposób zablokowana.

W tym artykule opisano, jak tooconfigure kerberos ograniczonego delegowania w domenie zarządzanej usług domenowych Azure AD.

## <a name="kerberos-constrained-delegation-kcd"></a>Ograniczone delegowanie protokołu Kerberos (KCD)
Delegowanie protokołu Kerberos umożliwia tooimpersonate konta innego zasoby podmiotu zabezpieczeń (na przykład użytkownik) tooaccess zabezpieczeń. Należy wziąć pod uwagę aplikacji sieci web, który uzyskuje dostęp do sieci web zaplecza interfejsu API w kontekście hello użytkownika. W tym przykładzie hello aplikacji sieci web (uruchomione w kontekście konta usługi lub konto komputera/urządzenia hello) personifikuje hello użytkownika podczas uzyskiwania dostępu do zasobów hello (zaplecza interfejsu API sieci web). Delegowanie protokołu Kerberos jest niebezpieczne, ponieważ nie ogranicza hello, do których dostęp hello zasobów personifikacji konta w kontekście hello hello użytkownika.

Ograniczone delegowanie protokołu Kerberos (KCD) ogranicza powitalne usług/zasoby toowhich hello określony serwer może działać w imieniu hello użytkownika. Tradycyjne KCD wymaga tooconfigure uprawnienia administratora domeny konta domeny dla usługi i ogranicza hello konta tooa pojedynczej domeny.

Tradycyjny KCD ma również kilka problemów związanych z nim. W starszych systemach operacyjnych, w którym administrator domeny hello skonfigurowane usługi hello administrator usługi hello miał nie tooknow wygodny sposób, które usługi frontonu delegowane toohello usług zasobów są jego własnością. A usługa frontonu, którą mógł delegować do usługi zasobów tooa potencjalny punkt ataku. Jeśli takie naruszenie nastąpi naruszenie serwera udostępniającego usługę frontonu i był skonfigurowany toodelegate tooresource usług, hello zasobów usługi również mogły zostać naruszone.

> [!NOTE]
> W domenie zarządzanej usług domenowych Azure AD nie masz uprawnienia administratora domeny. W związku z tym **KCD tradycyjnych nie można skonfigurować w domenie zarządzanej**. Użyj KCD oparte na zasobach, zgodnie z opisem w tym artykule. Ten mechanizm również jest bardziej bezpieczne.
>
>

## <a name="resource-based-kerberos-constrained-delegation"></a>Oparte na zasobach ograniczonego delegowania protokołu kerberos
W systemie Windows Server 2012 R2 i Windows Server 2012 hello możliwości tooconfigure ograniczonego delegowania dla usługi hello została przeniesiona z administratora usługi toohello hello domeny administratora. Dzięki temu administrator usług zaplecza hello można akceptować lub odrzucać usługi frontonu. Ten model jest nazywany **kerberos oparte na zasobach ograniczonego delegowania**.

Oparte na zasobach KCD została skonfigurowana przy użyciu programu PowerShell. Za pomocą hello Set-ADComputer lub polecenia cmdlet Set-ADUser, w zależności od tego, czy hello personifikacji konta jest konto komputera lub konto serwisu konta użytkownika.

### <a name="configure-resource-based-kcd-for-a-computer-account-on-a-managed-domain"></a>Skonfiguruj oparte na zasobach KCD dla konta komputera do domeny zarządzanej
Założono, że masz aplikację sieci web uruchomiony na komputerze hello "contoso100-webapp.contoso100.com". Musi on tooaccess hello zasobów (interfejsu API sieci web uruchomiony na "contoso100-api.contoso100.com") w kontekście hello użytkownicy domeny. Oto, jak należy skonfigurować oparte na zasobach KCD dla tego scenariusza.

```
$ImpersonatingAccount = Get-ADComputer -Identity contoso100-webapp.contoso100.com
Set-ADComputer contoso100-api.contoso100.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

### <a name="configure-resource-based-kcd-for-a-user-account-on-a-managed-domain"></a>Skonfiguruj oparte na zasobach KCD dla konta użytkownika w domenie zarządzanej
Przykładowa aplikacja sieci web uruchomiona jako konto usługi "appsvc" i musi (interfejsu API sieci web uruchomiona jako konto usługi - "backendsvc") zasobu hello tooaccess w kontekście hello użytkowników domeny. Oto, jak należy skonfigurować oparte na zasobach KCD dla tego scenariusza.

```
$ImpersonatingAccount = Get-ADUser -Identity appsvc
Set-ADUser backendsvc -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

## <a name="related-content"></a>Powiązana zawartość
* [Usługi domenowe AD Azure - Przewodnik wprowadzający](active-directory-ds-getting-started.md)
* [Omówienie delegowania ograniczonego protokołu Kerberos](https://technet.microsoft.com/library/jj553400.aspx)
