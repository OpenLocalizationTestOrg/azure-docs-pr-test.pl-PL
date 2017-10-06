---
title: "atrybuty usługi synchronizacji aaaAzure AD Connect w tle | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak działa atrybuty cienia w usługi synchronizacji programu Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1b8665e7488c6078b655f8a3e35519145bacd898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a>Atrybuty cienia Usługa synchronizacji Azure AD Connect
Większość atrybutów są reprezentowane hello takie same jak w usłudze Azure AD jako znajdują się w lokalnej usługi Active Directory. Niektóre atrybuty mają niektóre specjalnej obsługi, a wartość atrybutu hello w usłudze Azure AD może być inna niż Azure AD Connect synchronizuje.

## <a name="introducing-shadow-attributes"></a>Wprowadzenie do atrybutów w tle
Niektóre atrybuty mają dwa oświadczenia w usłudze Azure AD. Zarówno wartość lokalne powitania i obliczonej wartości są przechowywane. Te atrybuty dodatkowe są nazywane atrybuty cienia. Witaj dwa atrybuty najczęściej której występuje ten problem są **userPrincipalName** i **proxyAddress**. Hello zmiany w wartościach atrybutów się stanie, gdy znajdują się wartości tych atrybutów reprezentujących domeny z systemem innym niż zweryfikowane. Ale hello aparatu synchronizacji w Connect odczytuje hello wartości w atrybucie tle hello to jego względem, atrybut hello zostało potwierdzone przez usługę Azure AD.

Użytkownik nie widzi hello tle atrybutów przy użyciu hello Azure portalu lub przy użyciu programu PowerShell. Ale opis hello koncepcji pomaga możesz tootroubleshoot niektórych scenariuszy w przypadku, gdy atrybut hello ma różne wartości lokalnej i w chmurze hello.

toobetter zrozumienie zachowania hello, Szukaj w tym przykładzie z firmy Fabrikam:  
![Domeny](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
Mają one wielu sufiksów nazw UPN w usłudze Active Directory ich lokalnych, ale tylko jeden zweryfikowane.

### <a name="userprincipalname"></a>userPrincipalName
Jeśli użytkownik ma następujące wartości atrybutów w domenie z systemem innym niż zweryfikowane hello:

| Atrybut | Wartość |
| --- | --- |
| userPrincipalName lokalnymi | lee.sperry@fabrikam.com |
| Azure AD shadowUserPrincipalName | lee.sperry@fabrikam.com |
| UserPrincipalName usługi Azure AD | lee.sperry@fabrikam.onmicrosoft.com |

Atrybut userPrincipalName Hello jest hello wartość wyświetlana po użyciu programu PowerShell.

Ponieważ wartość atrybutu rzeczywistego lokalnymi hello są przechowywane w usłudze Azure AD po zweryfikowaniu domeny fabrikam.com hello, usługi Azure AD aktualizuje atrybut userPrincipalName hello hello wartość z zakresu od hello shadowUserPrincipalName. Nie masz toosynchronize jakiekolwiek zmiany z usługi Azure AD Connect dla tych toobe wartości zaktualizowane.

### <a name="proxyaddresses"></a>proxyAddresses
powitalne tego samego procesu dla tylko tym zweryfikowanych domen występuje także dla proxyAddresses, ale niektóre dodatkowe logiki. Sprawdź, czy Hello zweryfikowanych domen odbywa się tylko dla skrzynek pocztowych użytkowników. Użytkownik z włączoną obsługą poczty lub skontaktuj się z reprezentuje użytkownika w innej organizacji programu Exchange i można dodać wartości w obiektach toothese proxyAddresses.

W przypadku skrzynek pocztowych użytkownika lokalnie lub w usłudze Exchange Online są wyświetlane tylko wartości zweryfikowanych domen. Go może wyglądać następująco:

| Atrybut | Wartość |
| --- | --- |
| proxyAddresses lokalnymi | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| ProxyAddresses usługi Exchange Online | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

W takim przypadku  **smtp:abbie.spencer@fabrikam.com**  został usunięty, ponieważ nie został zweryfikowany tej domeny. Exchange również został dodany, ale  **SIP:abbie.spencer@fabrikamonline.com** . Firma Fabrikam nie został użyty Lync/Skype lokalnej, ale usługi Azure AD i usługi Exchange Online przygotować.

Ta logikę proxyAddresses jest określony tooas **ProxyCalc**. ProxyCalc została wywołana z każdej zmiany na koncie użytkownika po:

- przypisano użytkownika Hello plan usługi, która obejmuje usługę Exchange Online, nawet jeśli użytkownik hello nie został licencji na program Exchange. Na przykład jeśli jest przypisany użytkownik hello hello SKU E3 pakietu Office, ale tylko przypisano usługi SharePoint Online. Dotyczy to nawet jeśli skrzynki pocztowej jest nadal lokalnymi.
- Witaj msExchRecipientTypeDetails atrybut ma wartość.
- Wprowadzone zmiany tooproxyAddresses lub userPrincipalName.

ProxyCalc może potrwać kilka tooprocess czas zmiany na koncie użytkownika i nie jest równocześnie z procesu eksportu hello Azure AD Connect.

> [!NOTE]
> Witaj logiki ProxyCalc ma pewne dodatkowe zachowania dla zaawansowanych scenariuszy, które nie zostały opisane w tym temacie. W tym temacie została podana dla Ciebie toounderstand hello zachowania i zarządzania dokumentami nie całą logikę wewnętrznego.

### <a name="quarantined-attribute-values"></a>Atrybuty poddane kwarantannie
Atrybuty cienia są również używane w przypadku zduplikowanymi wartościami atrybutów. Aby uzyskać więcej informacji, zobacz [odporności zduplikowany atrybut](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="see-also"></a>Zobacz też
* [Synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
