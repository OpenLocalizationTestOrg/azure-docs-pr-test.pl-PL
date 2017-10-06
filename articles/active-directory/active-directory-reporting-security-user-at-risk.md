---
title: "aaaUsers oflagowane zagrożenia zabezpieczeń raportu w portalu usługi Azure Active Directory hello | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat użytkowników hello oflagowane zagrożenia zabezpieczeń raportu w portalu usługi Azure Active Directory hello"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a>Użytkownicy oflagowani zagrożenia zabezpieczeń raportu w portalu usługi Azure Active Directory hello

Z raportami zabezpieczeń hello w hello Azure Active Directory (Azure AD) możesz uzyskać wgląd w prawdopodobieństwo hello kont użytkowników z naruszonymi zabezpieczeniami w danym środowisku. 

Usługa Azure Active Directory wykryje podejrzanych działań, które są powiązane tooyour kont użytkowników. Dla każdej wykrytej akcji jest tworzony wpis nazywany *zdarzeniem o podwyższonym ryzyku*. Aby uzyskać więcej informacji, zobacz [Zdarzenia o podwyższonym ryzyku w usłudze Azure Active Directory](active-directory-identity-protection-risk-events.md). 

Witaj wykrył, że zdarzenia o podwyższonym ryzyku są używane toocalculate:

- **Ryzykowne logowania** -ryzykowne logowanie jest wskaźnik prób logowania, które mogły zostać wykonane przez osobę, która nie jest właścicielem uzasadnionych hello konta użytkownika. Aby uzyskać więcej informacji, zobacz [Ryzykowne logowania](active-directory-identityprotection.md#risky-sign-ins). 

- **Użytkownicy oflagowani w związku z ryzykiem** — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone. Aby uzyskać więcej informacji, zobacz [Użytkownicy oflagowani w związku z ryzykiem](active-directory-identityprotection.md#users-flagged-for-risk).  

W portalu Azure hello, można znaleźć zabezpieczeń hello raport dotyczący hello **usługi Azure Active Directory** bloku w hello **zabezpieczeń** sekcji.  

![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>Jakie licencji usługi Azure AD potrzebujesz tooaccess raport zabezpieczeń?  

Wszystkie wersje usługi Azure Active Directory zapewniają dostęp do raportów użytkowników oflagowanych w związku z ryzykiem.  
Jednak hello poziom szczegółowości raportu różni się między wersjami hello: 

- W hello **wersje usługi Azure Active Directory wolnego i Basic**, otrzymasz listę użytkowników z ustawioną flagą ryzyka. 

- Witaj **Azure Active Directory Premium 1** edition rozszerza tego modelu, należy również włączyć tooexamine niektóre hello podstawowy zdarzenia ryzyka, które zostały wykryte dla każdego raportu. 

- Hello **Azure Active Directory Premium 2** edition zapewnia hello bardziej szczegółowe informacje o wszystkich zdarzeniach ryzyka podstawowej i umożliwia tooconfigure zasady zabezpieczeń, które automatycznie odpowiadać tooconfigured ryzyka poziomy.



## <a name="azure-active-directory-free-and-basic-edition"></a>Azure Active Directory — wersja Bezpłatna i Podstawowa

Użytkownicy Hello oflagowane ryzyka raportu w wersji bezpłatnej i podstawowa usługi Azure Active Directory hello udostępnia listę kont użytkowników, które zostały naruszone. 


![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/03.png)

Wybór użytkownika zostanie otwarty blok danych użytkownikowi hello.
Dla użytkowników, którzy są narażeni na ataki można sprawdzić hello użytkownika logowania historii i zresetuj hasło hello, jeśli to konieczne.

![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/46.png)


To okno dialogowe oferuje opcję:

- Pobierz raport hello

- Wyszukiwania użytkowników

![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a>Azure Active Directory — wersje Premium

Użytkownicy Hello oflagowane ryzyka raportu w wersji premium hello Azure Active Directory umożliwia:

- [Lista kont użytkowników](active-directory-identityprotection.md#users-flagged-for-risk), których bezpieczeństwo mogło zostać naruszone 

- Zagregowane informacje o hello [ryzyka typów zdarzeń](active-directory-identity-protection-risk-events.md) zostały wykryte

- Opcja toodownload hello raportu

- Opcja tooconfigure [zasady korygowania ryzyka użytkownika](active-directory-identityprotection.md#user-risk-security-policy)  


![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/71.png)

Po wybraniu użytkownika jest dla niego wyświetlany szczegółowy widok raportu, który umożliwia wykonanie następujących czynności:

- Wyświetl wszystkie sesje logowania hello otwarte

- Resetowanie hasła użytkownika hello

- Odrzucanie wszystkich zdarzeń.

- Zbadaj zdarzenia zgłoszone ryzyka dla hello użytkownika. 


![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/324.png)


tooinvestigate zdarzenia ryzyka, wybierz jeden z hello listy tooopen hello **szczegóły** bloku dla tego zdarzenia ryzyka. Na powitania **szczegóły** bloku masz hello opcja tooeither [ręcznie zamknąć zdarzenie ryzyka](active-directory-identityprotection.md#closing-risk-events-manually) lub ponownym uaktywnieniem zdarzeń ryzyka ręcznie zamknięty. 


![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a>Następne kroki

- Aby uzyskać więcej informacji na temat ochrony tożsamości w usłudze Azure Active Directory, zobacz [Ochrona tożsamości w usłudze Azure Active Directory](active-directory-identityprotection.md).

