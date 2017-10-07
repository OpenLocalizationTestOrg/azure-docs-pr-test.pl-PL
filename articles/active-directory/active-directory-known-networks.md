---
title: aaaKnown sieci w hello klasycznego portalu Azure | Dokumentacja firmy Microsoft
description: "Konfigurując znane sieci, można uniknąć o adresy IP, które są własnością organizacji objęte hello dodatki logowania z wielu lokalizacji geograficznych i ins logowania z adresów IP z raportami podejrzanych działań."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a>Znane sieci

> [!div class="op_single_selector"]
> * [Klasyczna witryna Azure Portal](active-directory-known-networks.md)
> * [Witryna Azure Portal](active-directory-known-networks-azure-portal.md)
> 
> 


Umożliwia dostęp do usługi Azure Active Directory i użycia raporty toogain widoczność hello integralności i bezpieczeństwa w katalogu organizacji. Dzięki tym informacjom administratora katalogu można lepiej określić, gdzie może znajdować się możliwe zagrożenia bezpieczeństwa, tak aby ich odpowiednio zaplanować toomitigate te zagrożenia.

Możliwe, że Witaj "*logowania z wielu lokalizacji geograficznych*"i"*logowania z adresów IP z podejrzaną aktywność*" raporty niepoprawnie Flaga adresy IP, które są rzeczywiście należących do użytkownika organizacja. 

Dzieje się tak na przykład, gdy: 

* Użytkownik w biurze Boston zalogował się zdalnie centrum danych tooyour hello wyzwalaczy Poznań "Ins logowania z wielu lokalizacji geograficznych" raportu 
* Użytkownik z organizacji podejmuje toosign na z hello wyzwalaczy niepoprawne hasło "Ins logowania z adresów IP związanych z podejrzanymi działaniami" raport 

tooprevent tych przypadkach zabezpieczeń mylących Generowanie raportów, należy dodać znane listę adresów IP zakresów toohello publicznego adresu IP w organizacji.    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a>tooadd z zakresów w organizacji publicznego adresu IP, wykonaj następujące kroki hello:

1. Logowania jednokrotnego toohello [portalu zarządzania Azure](https://manage.windowsazure.com).

2. W okienku po lewej stronie powitania kliknij **usługi Active Directory**. 

    ![Znane sieci](./media/active-directory-known-networks/known-netwoks-01.png)

3. W hello **katalogu** , a następnie wybierz katalog.

4. W menu hello na górze hello, kliknij przycisk **Konfiguruj**. 

    ![Znane sieci](./media/active-directory-known-networks/known-netwoks-02.png)

5. Na karcie Konfigurowanie hello Przejdź zbyt**Twojego zakresy organizacji publicznych adresów IP** 

    ![Znane sieci](./media/active-directory-known-networks/known-netwoks-03.png)

6. Kliknij przycisk **Dodawanie zakresów adresów IP znane**.

7. Dodaj zakresy adresów w pojawi się okno dialogowe hello, a następnie kliknij przycisk wyboru hello, gdy wszystko będzie gotowe. 

    ![Znane sieci](./media/active-directory-known-networks/known-netwoks-04.png)

**Dodatkowe zasoby:**

* [Wyświetlanie raportów dostępu i użycia](active-directory-view-access-usage-reports.md)
* [Logowania z adresów IP związanych z podejrzanymi działaniami](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [Logowania z wielu lokalizacji geograficznych](active-directory-reporting-sign-ins-from-multiple-geographies.md)

