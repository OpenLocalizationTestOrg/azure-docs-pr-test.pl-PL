---
title: Znane sieci w klasycznym portalu Azure | Dokumentacja firmy Microsoft
description: "Konfigurując znane sieci, można uniknąć o adresy IP, które są własnością organizacji objętych ins logowania z wielu lokalizacji geograficznych i ins logowania z adresów IP z raportami podejrzanych działań."
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
ms.openlocfilehash: e4d51d1d2f09fca34d749879e21d49f785eac35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="known-networks"></a>Znane sieci

> [!div class="op_single_selector"]
> * [Klasyczna witryna Azure Portal](active-directory-known-networks.md)
> * [Witryna Azure Portal](active-directory-known-networks-azure-portal.md)
> 
> 


Dostęp do usługi Azure Active Directory i raporty użycia umożliwia wgląd we integralności i bezpieczeństwa katalogu organizacji. Dzięki tym informacjom administratora katalogu można lepiej określić, gdzie może znajdować się możliwe zagrożenia bezpieczeństwa, tak aby ich odpowiednio zaplanować ich eliminowania.

Możliwe jest który "*logowania z wielu lokalizacji geograficznych*"i"*logowania z adresów IP z podejrzaną aktywność*" raporty niepoprawnie Flaga adresy IP, które są rzeczywiście należących do użytkownika organizacja. 

Dzieje się tak na przykład, gdy: 

* Użytkownik w Twojej Boston office zalogował się zdalnie na centrum danych w sieci San Francisco uruchamia raportu "Logowania z wielu lokalizacji geograficznych" 
* Organizacji próbie logowania z wyzwalaczy niepoprawne hasło "Logowania z adresów IP z podejrzaną aktywność" raportu 

Aby uniknąć tych przypadkach generowania mylących raporty dotyczące zabezpieczeń, należy dodać znane zakresów adresów IP do listy publicznego adresu IP w organizacji.    

### <a name="to-add-your-organizations-public-ip-address-ranges-perform-the-following-steps"></a>Aby dodać organizacji zakresy publicznych adresów IP, wykonaj następujące czynności:

1. Logowanie do [portalu zarządzania Azure](https://manage.windowsazure.com).

2. W okienku po lewej stronie kliknij **usługi Active Directory**. 

    ![Znane sieci](./media/active-directory-known-networks/known-netwoks-01.png)

3. W **katalogu** , a następnie wybierz katalog.

4. W menu u góry kliknij **Konfiguruj**. 

    ![Znane sieci](./media/active-directory-known-networks/known-netwoks-02.png)

5. Na karcie Konfigurowanie przejdź do **Twojego zakresy organizacji publicznych adresów IP** 

    ![Znane sieci](./media/active-directory-known-networks/known-netwoks-03.png)

6. Kliknij przycisk **Dodawanie zakresów adresów IP znane**.

7. Dodaj zakresy adresów w wyświetlonym oknie dialogowym, a następnie kliknij przycisk wyboru, gdy wszystko będzie gotowe. 

    ![Znane sieci](./media/active-directory-known-networks/known-netwoks-04.png)

**Dodatkowe zasoby:**

* [Wyświetlanie raportów dostępu i użycia](active-directory-view-access-usage-reports.md)
* [Logowania z adresów IP związanych z podejrzanymi działaniami](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [Logowania z wielu lokalizacji geograficznych](active-directory-reporting-sign-ins-from-multiple-geographies.md)

