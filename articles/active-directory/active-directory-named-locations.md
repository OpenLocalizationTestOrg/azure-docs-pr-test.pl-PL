---
title: "lokalizacje aaaNamed w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Konfigurując o nazwie lokalizacji, możesz uniknąć IP adresów, które są własnością organizacji wygenerować fałszywych alarmów dla lokalizacji tooatypical niemożliwa podróż hello ryzyka typ zdarzenia."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a>Nazwane lokalizacje w usłudze Azure Active Directory

Z hello o nazwie lokalizacji funkcji usługi Azure Active Directory można opisać zaufanych zakresów adresów IP w Twojej organizacji. W danym środowisku, można użyć nazwane lokalizacje w kontekście hello wykrywanie hello [ryzyka zdarzenia](active-directory-reporting-risk-events.md). Witaj pomaga zmniejszyć hello liczbę fałszywych alarmów zgłoszone dla hello *lokalizacje tooatypical niemożliwa podróż* ryzyka typ zdarzenia. 

## <a name="configuration"></a>Konfiguracja

tooconfigure lokalizacji o nazwie:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) jako administrator globalny.

2. W okienku po lewej stronie powitania kliknij **usługi Azure Active Directory**.

    ![Hello Azure Active Directory łącze w okienku po lewej stronie powitania](./media/active-directory-named-locations/01.png)

3. Na powitania **usługi Azure Active Directory** bloku w hello **zabezpieczeń** kliknij **dostępu warunkowego**.

    ![Witaj polecenie dostępu warunkowego](./media/active-directory-named-locations/05.png)


4. Na powitania **dostępu warunkowego** bloku w hello **Zarządzaj** kliknij **o nazwie lokalizacje**.

    ![Witaj polecenia lokalizacji o nazwie](./media/active-directory-named-locations/06.png)


5. Na powitania **o nazwie lokalizacje** bloku, kliknij przycisk **nową lokalizację**.

    ![Witaj nowe polecenie lokalizacji](./media/active-directory-named-locations/07.png)


6. Na powitania **nowy** bloku hello następujące:

    ![Nowy blok Hello](./media/active-directory-named-locations/08.png)

    a. W hello **nazwa** wpisz nazwę dla nazwanego lokalizacji.

    b. W hello **zakresów IP** wpisz zakres adresów IP. zakres adresów IP Hello musi toobe w hello *Bezklasowego routingu międzydomenowego* formacie (CIDR).  

    c. Kliknij przycisk **Utwórz**.



## <a name="what-you-should-know"></a>Co należy wiedzieć

**Aktualizacje zbiorcze**: tworzenia lub aktualizowania nazwane lokalizacje aktualizacji zbiorczej można przekazać lub pobrania pliku CSV hello zakresów adresów IP. Przekazanie dodaje zakresów IP hello hello pliku toohello listy zamiast zastępowanie hello listy.

![Witaj, przekazywanie i pobieranie łącza](./media/active-directory-named-locations/09.png)


**Ograniczenia**: można określić maksymalnie 60 nazwane lokalizacje, z jedną tooeach zakresu przypisanego adresu IP z nich. Jeśli masz tylko jedną lokalizację o nazwie skonfigurowane dla niego można zdefiniować się too500 zakresów adresów IP.


## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat zdarzeń o podwyższonym ryzyku, zobacz [zdarzenia o podwyższonym ryzyku usługi Azure Active Directory](active-directory-reporting-risk-events.md).

