---
title: "Raport dotyczący ryzykownych logowań w portalu usługi Azure Active Directory | Microsoft Docs"
description: "Dowiedz się więcej o raporcie dotyczącym ryzykownych logowań w portalu usługi Azure Active Directory"
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
ms.openlocfilehash: 45a6f63bd920c9a70c25b8dfae084ea030256cf4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="risky-sign-ins-report-in-the-azure-active-directory-portal"></a>Raport dotyczący ryzykownych logowań w portalu usługi Azure Active Directory

Dzięki raportom o zabezpieczeniach w usłudze Azure Active Directory (Azure AD) możesz uzyskać wgląd w prawdopodobieństwo naruszenia bezpieczeństwa kont użytkowników w środowisku. 

Usługa Azure AD wykrywa podejrzane akcje powiązane z kontami użytkowników. Dla każdej wykrytej akcji jest tworzony wpis nazywany *zdarzeniem o podwyższonym ryzyku*. Aby uzyskać więcej informacji, zobacz [Zdarzenia o podwyższonym ryzyku w usłudze Azure Active Directory](active-directory-identity-protection-risk-events.md). 

Za pomocą wykrytych zdarzeń o podwyższonym ryzyku obliczane są:

- **Ryzykowne logowania** — ryzykowne logowanie jest wskaźnikiem próby logowania, które mogło zostać wykonane przez osobę, która nie jest prawowitym właścicielem konta użytkownika. Aby uzyskać więcej informacji, zobacz [Ryzykowne logowania](active-directory-identityprotection.md#risky-sign-ins). 

- **Użytkownicy oflagowani w związku z ryzykiem** — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone. Aby uzyskać więcej informacji, zobacz [Użytkownicy oflagowani w związku z ryzykiem](active-directory-identityprotection.md#users-flagged-for-risk).  

W witrynie [Azure Portal](https://portal.azure.com) raporty dotyczące zabezpieczeń można znaleźć w bloku **Azure Active Directory** w sekcji **Zabezpieczenia**. 

![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-to-access-a-security-report"></a>Jaka licencja usługi Azure AD jest wymagana w celu uzyskania dostępu do raportu zabezpieczeń?  

Wszystkie wersje usługi Azure Active Directory zapewniają dostęp do raportów ryzykownych logowań.  
Jednak poziom szczegółowości raportu zależy od wersji: 

- W **usłudze Azure Active Directory w wersji Bezpłatna i Podstawowa** masz już dostęp do listy ryzykownych logowań. 

- Wersja **Azure Active Directory Premium 1** rozszerza ten model, umożliwiając również badanie niektórych podstawowych zdarzeń związanych z ryzykiem, które uwzględniono w poszczególnych raportach. 

- Wersja **Azure Active Directory Premium 2** oferuje najbardziej szczegółowe informacje na temat wszystkich zdarzeń o podwyższonym ryzyku i umożliwia konfigurowanie zasad zabezpieczeń, które automatycznie reagują na wystąpienie skonfigurowanych poziomów ryzyka.



## <a name="azure-active-directory-free-and-basic-edition"></a>Azure Active Directory — wersja Bezpłatna i Podstawowa

Usługa Azure Active Directory w wersji Bezpłatna i Podstawowa zapewnia listę wykrytych ryzykownych logowań dla użytkowników. W tym raporcie znajdują się następujące informacje:

- **Użytkownik** — nazwa użytkownika użyta podczas logowania
- **IP** — adres IP urządzenia, którego użyto do nawiązania połączenia z usługą Azure Active Directory
- **Lokalizacja** — lokalizacja, z której nawiązano połączenie z usługą Azure Active Directory
- **Godzina logowania** — godzina, o której przeprowadzono logowanie
- **Stan** — stan logowania


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/01.png)

Na podstawie badania ryzykownego logowania możesz przekazać usłudze Azure Active Directory swoją reakcję w postaci następujących akcji:

- Rozwiąż
- Oznacz jako wynik fałszywie dodatni
- Zignoruj
- Uaktywnij ponownie

![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/21.png)

Aby uzyskać więcej informacji, zobacz [Ręczne zamykanie zdarzeń o podwyższonym ryzyku](active-directory-identityprotection.md#closing-risk-events-manually).

Ten raport oferuje opcję:

- Wyszukiwania zasobów
- Pobierania danych raportu


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a>Azure Active Directory — wersje Premium

Raport dotyczący ryzykownych logowań w usłudze Azure Active Directory w wersjach Premium zawiera następujące elementy:

- Zagregowane informacje o wykrytych [typach zdarzeń o podwyższonym ryzyku](active-directory-identity-protection-risk-events.md)

- Opcja pobrania raportu


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/456.png)


Po wybraniu zdarzenia o podwyższonym ryzyku jest dla niego wyświetlany szczegółowy widok raportu, który umożliwia wykonanie następujących czynności:

- Skonfigurowanie [zasad podejmowania działań naprawczych dotyczących ryzyka związanego z użytkownikiem](active-directory-identityprotection.md#user-risk-security-policy).  

- Przeglądanie i wykrywanie osi czasu dla zdarzenia o podwyższonym ryzyku.  

- Przeglądanie listy użytkowników, dla których wykryto konkretne zdarzenie o podwyższonym ryzyku.

- [Ręczne zamykanie zdarzeń o podwyższonym ryzyku](active-directory-identityprotection.md#closing-risk-events-manually) lub ponowne aktywowanie ręcznie zamkniętych zdarzeń o podwyższonym ryzyku. 


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/457.png)

Po wybraniu użytkownika jest dla niego wyświetlany szczegółowy widok raportu, który umożliwia wykonanie następujących czynności:

- Otwieranie widoku wszystkich logowań.

- Resetowanie hasła użytkownika.

- Odrzucanie wszystkich zdarzeń.

- Badanie zgłoszonych zdarzeń o podwyższonym ryzyku dla użytkownika. 


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/324.png)


Aby zbadać zdarzenie o podwyższonym ryzyku, wybierz je z listy.  
Spowoduje to otwarcie bloku **Szczegóły** dla tego zdarzenia o podwyższonym ryzyku. W bloku **Szczegóły** jest opcja [ręcznego zamknięcia zdarzenia o podwyższonym ryzyku](active-directory-identityprotection.md#closing-risk-events-manually) lub ponownego aktywowania ręcznie zamkniętego zdarzenia o podwyższonym ryzyku. 


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a>Następne kroki

- Aby uzyskać więcej informacji na temat ochrony tożsamości w usłudze Azure Active Directory, zobacz [Ochrona tożsamości w usłudze Azure Active Directory](active-directory-identityprotection.md).

