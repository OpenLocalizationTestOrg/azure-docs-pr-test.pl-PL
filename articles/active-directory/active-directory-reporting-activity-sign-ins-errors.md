---
title: "kody błędów raport aktywności aaaSign w portalu usługi Azure Active Directory hello | Dokumentacja firmy Microsoft"
description: "Dokumentacja dotycząca kodów błędów w raportach działań związanych z logowaniem."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: a0ca5b706bfeb0c7ce669712468a083a394712b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-report-error-codes-in-hello-azure-active-directory-portal"></a>Kody błędów raport aktywności logowania w portalu usługi Azure Active Directory hello

Hello informacje podane w raporcie logowania użytkownika hello możesz znaleźć odpowiedzi tooquestions, takich jak:

- Kto logował się za pomocą usługi Azure Active Directory?
- Do których aplikacji logowali się użytkownicy?
- Które operacje logowania zakończyły się błędem i dlaczego?

Ten błąd hello list temat kodów i hello opisy pokrewne. 

## <a name="how-can-i-display-failed-sign-ins"></a>Jak mogę wyświetlić nieudane operacje logowania? 

Pierwszy wpis punktu tooall logowania działań dane są  **[logowania](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)**  w hello **działania** sekcji **usługi Azure Active**.


![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins-errors/61.png "Działania związane z logowaniem")


W raporcie logowań można wyświetlić wszystkie nieudane logowania, wybierając wartość **Niepowodzenie** w obszarze **Stan logowania**.


![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins-errors/06.png "Działania związane z logowaniem")

Kliknięcie elementu na liście hello wyświetlane, otwiera hello **szczegóły aktywności: logowania** bloku. Ten widok udostępnia wszystkie szczegóły hello śledzonych w usłudze Azure Active Directory o logowania, w tym hello **kod błędu logowania** i **Przyczyna niepowodzenia**.

![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins-errors/05.png "Działania związane z logowaniem")


Hello toousing alternatywnych danych logowania hello tooaccess portalu Azure, można również użyć hello [interfejsem API raportowania](active-directory-reporting-api-getting-started-azure-portal.md).


Witaj Poniższa sekcja umożliwia pełny przegląd wszystkich możliwych błędów i hello związane z opisami. 

## <a name="error-codes"></a>Kody błędów

| Błąd| Opis |
| --- | --- |
| 50001| Nie można odnaleźć nazwy głównej usługi Hello o nazwie X w dzierżawie powitalnych o nazwie Y. Może to nastąpić, jeśli nie zainstalowano aplikacji hello przez administratora hello hello dzierżawcy. Lub podmiot zabezpieczeń zasobu nie został znaleziony w katalogu hello lub jest nieprawidłowy|
| 50008| Potwierdzenia języka SAML są brakujących ani źle skonfigurowanych w tokenie hello.|
| 50011| adres zwrotny Hello brakuje, niepoprawnie skonfigurowany lub nie odpowiada adresów odpowiedzi skonfigurowanych dla aplikacji hello.|
| 50053| Konto zostało zablokowane, ponieważ użytkownik próbował toosign w zbyt wiele razy przy użyciu niepoprawnego Identyfikatora użytkownika lub hasła.|
| 50054| Podczas uwierzytelniania użyto starego hasła.|
| 50055| Nieprawidłowe hasło — wprowadzono nieważne hasło.|
| 50057| Konto użytkownika zostało wyłączone.|
| 50058| Informacje o tożsamości użytkownika nie znajduje się między pod warunkiem lub poświadczenia użytkownika nie został znaleziony w dzierżawie wysłano dyskretnej żądanie logowania, ale żaden użytkownik nie jest zalogowany lub usługa została tooauthenticate hello użytkownika.|
| 50074| Wymagane jest silne uwierzytelnianie (dwuskładnikowe)|
| 50079| Użytkownik musi tooenroll dla drugiego składnika uwierzytelniania|
| 50126| Nieprawidłowa nazwa lub hasło użytkownika albo nieprawidłowa nazwa lub hasło użytkownika lokalnego.|
| 50131| Kod używany w przypadku różnych błędów dostępu warunkowego, Urządzenia Windows zły np. stanu, żądanie zablokowane należne działanie toosuspicious, zasady dostępu i zasad zabezpieczeń decyzji.|
| 50133| Sesja jest nieprawidłowa tooexpiration lub ostatnie zmiany hasła.|
| 50144| Ważność hasła użytkownika usługi Active Directory wygasła.|
| 65001| X aplikacji nie ma uprawnienia aplikacji tooaccess Y lub uprawnienie hello został odwołany. Lub hello użytkownik lub administrator nie zgodził aplikacji hello toouse przy użyciu Identyfikatora X. wysyłania żądania autoryzacji interakcyjne dla tego użytkownika i zasobów. Lub hello użytkownik lub administrator nie zgodził toouse hello aplikacji o identyfikatorze X. wysyłania tooact administratora dzierżawy tooyour autoryzacji żądania w imieniu aplikacji hello: Y dla zasobu: Z.|
| 65005| Aplikacja Hello wymagane listy dostępu do zasobów nie zawiera aplikacji wykrywalny przez zasób hello lub powitania klienta aplikacja zażądała tooresource dostępu, który nie został określony w jej listy dostępu do wymaganych zasobów lub usługi wykres zwrócił nieprawidłowy żądanie lub nie można odnaleźć zasobu.|
| 70001| Nie można odnaleźć aplikacji Hello o nazwie X w dzierżawie powitalnych o nazwie Y. To może wystąpić, jeśli nie zainstalowano aplikacji hello przez hello administrator dzierżawy hello lub przyzwolenie tooby każdy użytkownik w dzierżawie powitalnych. Prawdopodobnie została wysłana dzierżawy niewłaściwy toohello żądania uwierzytelniania.|
| 80001| Brak dostępnych agentów uwierzytelniania.|
| 80002| Upłynął limit czasu żądania weryfikacji hasła agenta uwierzytelniania.|
| 80003| Agent uwierzytelniania odebrał nieprawidłową odpowiedź.|
| 80004| W żądaniu logowania użyto nieprawidłowej głównej nazwy użytkownika (UPN).|
| 80005| Agent uwierzytelniania: wystąpił błąd.|
| 80007| Uwierzytelnianie agenta tooconnect tooActive katalogu.|
| 80010| Hasło toodecrypt Agent uwierzytelniania.|
| 81001| Bilet Kerberos użytkownika jest zbyt duży.|
| 81002| Użytkownik toovalidate biletu Kerberos.|
| 81003| Użytkownik toovalidate biletu Kerberos.|
| 81004| Próba uwierzytelniania Kerberos nie powiodła się.|
| 81008| Użytkownik toovalidate biletu Kerberos.|
| 81009| Użytkownik toovalidate biletu Kerberos.|
| 81010| Bezproblemowe logowanie Jednokrotne nie powiodło się, ponieważ biletu Kerberos hello użytkownika wygasło lub jest nieprawidłowy.|
| 81011| Obiekt użytkownika toofind na podstawie informacji biletu Kerberos hello użytkownika.|
| 81012| Hello użytkownika w trakcie toosign w tooAzure AD różni się od użytkownika hello w urządzeniu hello zalogowany.|
| 81013| Obiekt użytkownika toofind na podstawie informacji biletu Kerberos hello użytkownika.|
| 90014| Używany w przypadku różnych, jeśli nie występuje w poświadczeniu hello oczekiwanego pola.|
| 90093| Wykres zwrócił kod błędu niedozwolonych hello żądania.|



## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji, zobacz hello [logowania raporty aktywności w portalu usługi Azure Active Directory hello](active-directory-reporting-activity-sign-ins.md).

