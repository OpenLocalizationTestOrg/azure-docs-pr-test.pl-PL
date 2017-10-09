---
title: "aaaRisky raport logowania w portalu usługi Azure Active Directory hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello raportu ryzykowne logowania w portalu usługi Azure Active Directory hello"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a>Raport ryzykowne logowania w portalu usługi Azure Active Directory hello

Z hello raporty dotyczące zabezpieczeń w usłudze Azure Active Directory (Azure AD) można uzyskać wgląd w prawdopodobieństwo hello kont użytkowników ze złamanymi zabezpieczeniami w danym środowisku. 

Usługi Azure AD wykrycia podejrzanych działań, które są powiązane tooyour kont użytkowników. Dla każdej wykrytej akcji jest tworzony wpis nazywany *zdarzeniem o podwyższonym ryzyku*. Aby uzyskać więcej informacji, zobacz [Zdarzenia o podwyższonym ryzyku w usłudze Azure Active Directory](active-directory-identity-protection-risk-events.md). 

Witaj wykrył, że zdarzenia o podwyższonym ryzyku są używane toocalculate:

- **Ryzykowne logowania** -ryzykowne logowanie jest wskaźnik prób logowania, które mogły zostać wykonane przez osobę, która nie jest właścicielem uzasadnionych hello konta użytkownika. Aby uzyskać więcej informacji, zobacz [Ryzykowne logowania](active-directory-identityprotection.md#risky-sign-ins). 

- **Użytkownicy oflagowani w związku z ryzykiem** — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone. Aby uzyskać więcej informacji, zobacz [Użytkownicy oflagowani w związku z ryzykiem](active-directory-identityprotection.md#users-flagged-for-risk).  

W [hello portalu Azure](https://portal.azure.com), można znaleźć zabezpieczeń hello raport dotyczący hello **usługi Azure Active Directory** bloku w hello **zabezpieczeń** sekcji. 

![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>Jakie licencji usługi Azure AD potrzebujesz tooaccess raport zabezpieczeń?  

Wszystkie wersje usługi Azure Active Directory zapewniają dostęp do raportów ryzykownych logowań.  
Jednak hello poziom szczegółowości raportu różni się między wersjami hello: 

- W hello **wersje usługi Azure Active Directory wolnego i Basic**, już uzyskać listę ryzykowne logowania. 

- Witaj **Azure Active Directory Premium 1** edition rozszerza tego modelu, należy również włączyć tooexamine niektóre hello podstawowy zdarzenia ryzyka, które zostały wykryte dla każdego raportu. 

- Witaj **Azure Active Directory Premium 2** edition udostępnia program hello najbardziej szczegółowe informacje o wszystkich zdarzeniach ryzyka podstawowej i pozwala także tooconfigure zasady zabezpieczeń, które automatycznie odpowiadać tooconfigured poziomów ryzyka.



## <a name="azure-active-directory-free-and-basic-edition"></a>Azure Active Directory — wersja Bezpłatna i Podstawowa

wersje podstawowe i Hello Azure Active Directory wolnego Podaj listę ryzykowne sesje logowania, które zostały wykryte dla użytkowników. W tym raporcie znajdują się następujące informacje:

- **Użytkownik** — Witaj nazwa hello użytkownika, który był używany podczas operacji logowania hello
- **IP** — Witaj adres IP urządzenia hello, który był używany tooconnect tooAzure usługi Active Directory
- **Lokalizacja** — lokalizacja hello używana tooAzure tooconnect usługi Active Directory
- **Czas logowania** — czas hello podczas logowania hello została wykonana
- **Stan** — Witaj stan logowania hello


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/01.png)

W oparciu o badaniu z hello ryzykowne logowania, można podać tooAzure opinii usługi Active Directory w postaci hello następujące akcje:

- Rozwiąż
- Oznacz jako wynik fałszywie dodatni
- Zignoruj
- Uaktywnij ponownie

![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/21.png)

Aby uzyskać więcej informacji, zobacz [Ręczne zamykanie zdarzeń o podwyższonym ryzyku](active-directory-identityprotection.md#closing-risk-events-manually).

Ten raport oferuje opcję:

- Wyszukiwania zasobów
- Pobierz dane raportu hello


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a>Azure Active Directory — wersje Premium

Witaj ryzykowne logowania raportu w wersji premium hello Azure Active Directory umożliwia:

- Zagregowane informacje o hello [ryzyka typów zdarzeń](active-directory-identity-protection-risk-events.md) zostały wykryte

- Opcja toodownload hello raportu


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/456.png)


Po wybraniu zdarzenia o podwyższonym ryzyku jest dla niego wyświetlany szczegółowy widok raportu, który umożliwia wykonanie następujących czynności:

- Opcja tooconfigure [zasady korygowania ryzyka użytkownika](active-directory-identityprotection.md#user-risk-security-policy)  

- Przejrzyj oś czasu wykrywania hello hello ryzyka zdarzeń  

- Przeglądanie listy użytkowników, dla których wykryto konkretne zdarzenie o podwyższonym ryzyku.

- [Ręczne zamykanie zdarzeń o podwyższonym ryzyku](active-directory-identityprotection.md#closing-risk-events-manually) lub ponowne aktywowanie ręcznie zamkniętych zdarzeń o podwyższonym ryzyku. 


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/457.png)

Po wybraniu użytkownika jest dla niego wyświetlany szczegółowy widok raportu, który umożliwia wykonanie następujących czynności:

- Wyświetl wszystkie sesje logowania hello otwarte

- Resetowanie hasła użytkownika hello

- Odrzucanie wszystkich zdarzeń.

- Zbadaj zdarzenia zgłoszone ryzyka dla hello użytkownika. 


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/324.png)


tooinvestigate zdarzenia ryzyka, wybierz z listy hello.  
Spowoduje to otwarcie hello **szczegóły** bloku dla tego zdarzenia ryzyka. Na powitania **szczegóły** bloku masz hello opcja tooeither [ręcznie zamknąć zdarzenie ryzyka](active-directory-identityprotection.md#closing-risk-events-manually) lub ponownym uaktywnieniem zdarzeń ryzyka ręcznie zamknięty. 


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a>Następne kroki

- Aby uzyskać więcej informacji na temat ochrony tożsamości w usłudze Azure Active Directory, zobacz [Ochrona tożsamości w usłudze Azure Active Directory](active-directory-identityprotection.md).

