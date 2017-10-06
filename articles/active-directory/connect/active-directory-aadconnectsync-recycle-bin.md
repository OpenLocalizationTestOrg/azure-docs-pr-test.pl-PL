---
title: "Synchronizacja programu Azure AD Connect: Włączanie Kosza AD | Dokumentacja firmy Microsoft"
description: "W tym temacie zaleca się używanie hello funkcji Kosz usługi AD z programem Azure AD Connect."
services: active-directory
keywords: "Kosz usługi AD, przypadkowego usunięcia, zakotwiczenie źródła"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a>Synchronizacja programu Azure AD Connect: Włączanie Kosza usługi AD
Zaleca się włączenie funkcji Kosza hello AD dla katalogów Active lokalnych, które są synchronizowane tooAzure AD. 

Jeśli przypadkowo usunięto lokalnego obiektu użytkownika usługi Active Directory i przywracania go za pomocą funkcji hello Azure AD przywraca hello odpowiedni obiekt użytkownika usługi Azure AD.  Informacje dotyczące funkcji Kosza hello AD, można znaleźć w temacie tooarticle [omówienie scenariusza dla Przywracanie usunięte obiekty usługi Active Directory](https://technet.microsoft.com/library/dd379542.aspx).

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a>Korzyści hello AD włączania Kosza
Ta funkcja pomaga z przywracaniem obiekty użytkownika usługi Azure AD, wykonując następujące hello:

* Jeśli przypadkowo usunięto lokalnego obiektu użytkownika AD, hello odpowiedni obiekt użytkownika usługi Azure AD zostaną usunięte w hello następnego cyklu synchronizacji. Domyślnie usługi Azure AD przechowuje obiekt użytkownika usługi Azure AD hello usunięte w stanie usunięte nietrwale przez 30 dni.

* Jeśli masz lokalnej włączona funkcja Kosz usługi AD, można przywrócić usunięty hello lokalnymi obiektu użytkownika usługi Active Directory bez modyfikowania jej wartość zakotwiczenie źródła. Gdy hello odzyskane lokalnymi obiektu użytkownika usługi Active Directory jest zsynchronizowany tooAzure AD, Azure AD spowoduje przywrócenie hello odpowiadającego wszystkie usunięte nietrwale obiektu użytkownika w usłudze Azure AD. Informacje o atrybut zakotwiczenia źródła można znaleźć tooarticle [Azure AD Connect: zagadnienia dotyczące projektowania](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).

* Jeśli nie masz lokalnego AD Odtwórz włączona funkcja Bin, może być wymagane toocreate AD obiektu tooreplace hello usuniętego obiektu user. Jeśli usługi Azure AD Connect synchronizacji usługi skonfigurowanego toouse generowanych przez system AD atrybutu (na przykład ObjectGuid) dla atrybutu zakotwiczenia źródła hello, hello nowo utworzony obiekt użytkownika usługi Active Directory zostanie nie ma hello tę samą wartość zakotwiczenie źródła jako hello usunięty obiekt użytkownika usługi Active Directory. Gdy hello nowo utworzony obiekt użytkownika usługi Active Directory jest synchronizowane tooAzure AD, Azure AD tworzy nowy obiekt użytkownika usługi Azure AD zamiast Przywracanie obiektu user hello wszystkie usunięte nietrwale usługi Azure AD.

> [!NOTE]
> Domyślnie usługi Azure AD przechowuje usunięte obiekty użytkownika usługi Azure AD w stanie usunięte nietrwale przez 30 dni, zanim zostaną trwale usunięte. Jednak Administratorzy może przyspieszyć hello usuwanie tych obiektów. Po hello obiekty zostaną trwale usunięte, nie mogą zostać odzyskane, nawet jeśli lokalne się, że włączono funkcję Kosz usługi AD.



## <a name="next-steps"></a>Następne kroki
**Tematy poglądowe**

* [Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji](active-directory-aadconnectsync-whatis.md)

* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
