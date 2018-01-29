---
title: "Rejestracja subskrypcji platformy Azure w rozwiązaniu Azure Cost Management | Microsoft Docs"
description: "Zarejestruj się w usłudze Azure Cost Management firmy Cloudyn przy użyciu subskrypcji platformy Azure."
services: cost-management
keywords: 
author: bandersmsft
ms.author: banders
ms.date: 10/11/2017
ms.topic: quickstart
ms.custom: mvc
ms.service: cost-management
manager: carmonm
ms.openlocfilehash: 4fed181a004ba6a5ea35dcbe1366e7d48342c96d
ms.sourcegitcommit: d03907a25fb7f22bec6a33c9c91b877897e96197
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/12/2017
---
# <a name="register-an-individual-azure-subscription-and-view-cost-data"></a>Rejestrowanie indywidualnej subskrypcji platformy Azure i wyświetlanie informacji o koszcie

Do rejestrowania w usłudze Azure Cost Management firmy Cloudyn służy subskrypcja platformy Azure. Rejestracja zapewnia dostęp do portalu firmy Cloudyn. W tym przewodniku Szybki start opisano szczegółowo proces rejestracji niezbędny do utworzenia subskrypcji wersji próbnej rozwiązania Cloudyn i zalogowania w portalu Cloudyn. Przedstawiono w nim także, jak od razu rozpocząć wyświetlanie danych kosztów.

## <a name="log-in-to-azure"></a>Zaloguj się do platformy Azure.

- Zaloguj się w witrynie Azure Portal pod adresem http://portal.azure.com.

## <a name="create-a-trial-registration"></a>Tworzenie rejestracji wersji próbnej

1. W witrynie Azure Portal kliknij pozycję **Zarządzanie kosztami i rozliczenia** na liście usług.
2. W obszarze **Przegląd** kliknij pozycję **Zarządzanie kosztami**  
    ![Strona Zarządzanie kosztami](./media/quick-register-azure-sub/cost-mgt-billing-service.png)
3. Na stronie **Zarządzanie kosztami** kliknij pozycję **Przejdź do zarządzania kosztami**, aby otworzyć stronę rejestracji rozwiązania Cloudyn w nowym oknie.
4. Na stronie rejestracji wersji próbnej rozwiązania Cloudyn wpisz nazwę swojej firmy i wybierz pozycję **Azure Individual Subscription Owner** (Posiadacz indywidualnej subskrypcji platformy Azure), a następnie kliknij przycisk **Next** (Dalej). Nazwa konta i identyfikator dzierżawy są automatycznie dodawane do formularza.  
    ![rejestracja wersji próbnej](./media/quick-register-azure-sub/trial-reg-ind.png)
5. Wybierz wartość **Offer ID - Name** (Identyfikator oferty —Nazwa) skojarzoną z Twoją subskrypcją. Jeśli nie masz pewności co do identyfikatora stawki dla swojej subskrypcji, możesz sprawdzić rachunek za platformę Azure i wyszukać pozycję **Offer ID** (Identyfikator oferty).
6. Zaakceptuj warunki użytkowania, zweryfikuj swoje informacje i kliknij przycisk **Next** (Dalej).
7. Na stronie **Gather additional data** (Zbierz dodatkowe dane) kliknij przycisk **Next** (Dalej), aby autoryzować rozwiązanie Cloudyn do zbierania danych zasobów platformy Azure. Te dane obejmują dane dotyczące użycia, wydajności, rozliczeń i tagów z Twoich subskrypcji.  
    ![zbieranie dodatkowych danych](./media/quick-register-azure-sub/gather-additional.png)
8. Przeglądarka przeniesie Cię do strony logowania w usłudze Cloudyn. Zaloguj się przy użyciu poświadczeń subskrypcji platformy Azure.
9. Kliknij pozycję **Go to Cloudyn** (Przejdź do rozwiązania Cloudyn), aby otworzyć portal Cloudyn, a następnie na stronie **Accounts Management** (Zarządzanie kontami) powinny zostać wyświetlone dane Twojego konta subskrypcji platformy Azure.  
    ![Zarządzanie kontami](./media/quick-register-azure-sub/accounts-mgt.png)

Aby wyświetlić wideo z samouczkiem dotyczącym rejestrowania subskrypcji platformy Azure, zobacz [Finding your Directory GUID and Rate ID for use in Azure Cost Management by Cloudyn](https://youtu.be/PaRjnyaNGMI) (Wyszukiwanie identyfikatora GUID katalogu i identyfikatora stawki do korzystania z rozwiązaniem Azure Cost Management firmy Cloudyn).

[!INCLUDE [cost-management-create-account-view-data](../../includes/cost-management-create-account-view-data.md)]

## <a name="next-steps"></a>Następne kroki

W tym przewodniku Szybki start opisano rejestrację w usłudze Cost Management przy użyciu danych subskrypcji platformy Azure. Przedstawiono także logowanie się do portalu Cloudyn i rozpoczęcie wyświetlania danych kosztów. Aby dowiedzieć się więcej na temat usługi Azure Cost Management firmy Cloudyn, przejdź do samouczka usługi Cost Management.

> [!div class="nextstepaction"]
> [Przeglądanie użycia i kosztów](./tutorial-review-usage.md)
