---
title: "Synchronizacja programu Azure AD Connect: zmiana konfiguracji domyślnej hello | Dokumentacja firmy Microsoft"
description: "Zawiera najlepsze rozwiązania do zmiany hello domyślnej konfiguracji synchronizacji usługi Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7638a031-1635-4942-94c3-fce8f09eed5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: aa05e935edd02c49c3c3fdc198b854f50327847c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-best-practices-for-changing-hello-default-configuration"></a>Synchronizacja programu Azure AD Connect: najlepsze rozwiązania dotyczące zmieniania konfiguracji domyślnej hello
Celem tego tematu Hello jest toodescribe obsługiwane i nieobsługiwane zmiany tooAzure AD Connect synchronizacji.

utworzone przez program Azure AD Connect konfiguracji Hello działa "jest" dla większości środowisk, które synchronizują lokalnymi usługi Active Directory z usługą Azure AD. Jednak w niektórych przypadkach jest konieczne tooapply konieczne pewne zmiany tooa konfiguracji toosatisfy określonego lub wymagań.

## <a name="changes-toohello-service-account"></a>Konto usługi toohello zmiany
Synchronizacja programu Azure AD Connect jest uruchomiony na koncie usługi tworzone przez Kreatora instalacji hello. To konto usługi ma hello szyfrowania kluczy toohello bazy danych używanej przez synchronizacji. Jest tworzona przy użyciu hasła długi 127 znaków i hello hasło jest ustawiane toonot wygaśnie.

* Jest **nieobsługiwany** toochange lub zresetować hasła hello hello konta usługi. Dzięki temu niszczy hello kluczy szyfrowania i hello usługi nie jest możliwe tooaccess hello w bazie danych i nie jest możliwe toostart.

## <a name="changes-toohello-scheduler"></a>Zmiany toohello harmonogramu
Począwszy od wersji hello z kompilacji 1.1 (luty 2016) można skonfigurować hello [harmonogramu](active-directory-aadconnectsync-feature-scheduler.md) toohave synchronizacji inny cykl niż domyślne hello 30 minut.

## <a name="changes-toosynchronization-rules"></a>Reguły tooSynchronization zmiany
Kreator instalacji Hello udostępnia konfigurację, w której powinien toowork dla hello najbardziej typowych scenariuszy. W razie potrzeby toomake zmiany toohello konfiguracji, należy wykonać te reguły toostill ma obsługiwanej konfiguracji.

* Możesz [zmienić przepływów atrybutów](active-directory-aadconnectsync-change-the-configuration.md#other-common-attribute-flow-changes) Jeśli przepływy atrybutów bezpośredniego domyślne hello nie są odpowiednie dla Twojej organizacji.
* Jeśli chcesz zbyt[nie przepływu atrybutu](active-directory-aadconnectsync-change-the-configuration.md#do-not-flow-an-attribute) i usuń wszelkie istniejący atrybut wartości w usłudze Azure AD, wówczas należy toocreate regułę dla tego scenariusza.
* [Wyłącz niechciane regułę synchronizacji](#disable-an-unwanted-sync-rule) zamiast usuwania. Usunięto regułę zostaje odtworzone podczas uaktualniania.
* zbyt[zmienić regułę out-of-box](#change-an-out-of-box-rule), należy utworzyć kopię hello oryginalnej reguły i wyłączyć hello out-of-box reguły. Hello Edytor reguł synchronizacji monity i pomaga.
* Eksportowanie reguł niestandardowych za pomocą hello Edytor reguł synchronizacji. Edytor Hello umożliwia za pomocą skryptu programu PowerShell, można użyć tooeasily utwórz je ponownie w przypadku odzyskiwania po awarii.

> [!WARNING]
> reguły synchronizacji out-of-box Hello mają odcisk palca. Jeśli wprowadzisz zmiany toothese reguły, hello odcisk palca nie jest zgodne. Możesz mieć problemy w przyszłości hello podczas próby tooapply nową wersję programu Azure AD Connect. Tylko należy sposób hello zmiany, które opisano w tym artykule.

### <a name="disable-an-unwanted-sync-rule"></a>Wyłącz niechciane reguły synchronizacji
Nie należy usuwać regułę synchronizacji out-of-box. Zostanie utworzona ponownie podczas uaktualniania dalej.

W niektórych przypadkach Kreator instalacji hello ma wyprodukowanych konfiguracji, który nie działa dla topologii. Na przykład jeśli topologią lasu zasobów dla konta, ale masz rozszerzonej hello schematu w lesie konta hello ze schematem Exchange hello, reguł dla programu Exchange są tworzone dla lasu kont hello i hello lasu zasobów. W takim przypadku należy toodisable hello reguły synchronizacji dla programu Exchange.

![Reguła synchronizacji wyłączone](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/exchangedisabledrule.png)

Na rysunku powyżej hello Kreator instalacji hello znalazł starego schematu Exchange 2003 w lesie konta hello. To rozszerzenie schematu został dodany przed wprowadzeniem hello lasu zasobów w środowisku firmy. tooensure żadnych atrybutów z hello starego implementacji programu Exchange są synchronizowane, powinny być wyłączone reguły synchronizacji hello, jak pokazano.

### <a name="change-an-out-of-box-rule"></a>Zmień reguły out-of-box
Hello czas tylko należy zmienić regułę out-of-box jest, gdy będziesz potrzebować toochange hello sprzężenia reguły. Toochange przepływ atrybutów, należy należy utworzyć regułę synchronizacji z wyższy priorytet niż zasady out-of-box hello. Witaj tylko reguły należy praktycznie tooclone jest reguła hello **w z usługi Active Directory — użytkownik przyłączyć**. Można zastąpić wszystkie reguły z regułą wyższy priorytet.

Toomake zmiany tooan out-of-box regułę, należy należy wprowadzić kopię hello out-of-box reguły i wyłączyć hello oryginalnej reguły. Następnie należy hello zmiany toohello sklonowany reguły. Hello Edytor reguł synchronizacji korzystającą z tych kroków. Po otwarciu regułę out-of-box prezentowany to okno dialogowe:  
![Ostrzeżenie poza reguły pola](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/warningoutofboxrule.png)

Wybierz **tak** toocreate kopię hello reguły. Reguła sklonowany Hello następnie jest otwarty.  
![Sklonowany reguły](./media/active-directory-aadconnectsync-best-practices-changing-default-configuration/clonedrule.png)

Na tej reguły sklonowany wprowadź wszelkie niezbędne zmiany tooscope, sprzężenia i przekształcenia.

## <a name="next-steps"></a>Następne kroki
**Tematy poglądowe**

* [Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji](active-directory-aadconnectsync-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
