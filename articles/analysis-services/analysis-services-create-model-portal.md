---
title: "aaaCreate modelu tabelarycznego przy użyciu narzędzia Projektant sieci Web Azure Analysis Services hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate modelu tabelarycznego usług Azure Analysis Services przy użyciu hello Projektant stron sieci Web w portalu Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a>Tworzenie modelu w portalu Azure

Funkcja Hello Azure Analysis Services web projektanta (wersja zapoznawcza) w portalu Azure zapewnia toocreate szybka i łatwa metoda i Edytuj modele tabelaryczne i zapytania modelu danych bezpośrednio w przeglądarce. 

Należy pamiętać, Projektant hello jest **Podgląd**. Gdy nowych funkcji jest dodawany cały czas hello, w wersji zapoznawczej, funkcje są ograniczone. Do bardziej zaawansowanego modelu programowania i testowania jest najlepszym toouse programu Visual Studio (SSDT) i SQL Server Management Studio (SSMS).

## <a name="prerequisites"></a>Wymagania wstępne

- Serwer usług Azure Analysis Services na powitania warstwy standardowa lub dewelopera. Nowe modele utworzone przy użyciu narzędzia Projektant sieci Web hello są zapytania bezpośredniego, obsługiwane tylko przez te warstwy.
- Baza danych SQL Azure, Magazyn danych SQL Azure lub pliku Power BI Desktop (pbix) jako źródła danych. Nowe modele utworzone na podstawie obsługi plików bazy danych SQL Azure, Magazyn danych SQL Azure, Oracle i Teradata Power BI Desktop źródeł danych.
- Konto programu SQL Server i hasła do łączenia tooAzure źródeł danych bazy danych SQL lub magazyn danych SQL Azure.

## <a name="toocreate-a-new-tabular-model"></a>toocreate nowego modelu tabelarycznego

1. Znajdujących się na serwerze **omówienie** bloku > **Projektant stron sieci Web**, kliknij przycisk **Otwórz**.

    ![Tworzenie modelu w portalu Azure](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. W **Projektant stron sieci Web** > **modele**, kliknij przycisk **+ Dodaj**.

    ![Tworzenie modelu w portalu Azure](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. W **nowy model**, wpisz nazwę modelu, a następnie wybierz źródło danych.

    ![Okno dialogowe nowego modelu w portalu Azure](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. W **Connect**, wprowadź właściwości połączenia hello. Nazwa użytkownika i hasło musi być kontem programu SQL Server.

     ![Połącz okna dialogowego w portalu Azure](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. W **tabele i widoki**wybierz hello tooinclude tabele w modelu, a następnie kliknij przycisk **Utwórz**. Automatycznie tworzyć relacji między tabelami w pary kluczy.

     ![Wybierz tabele i widoki](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

Nowy model zostanie wyświetlona w przeglądarce. W tym miejscu można wykonywać następujące czynności:   

- Zapytania danych modelu, przeciągając projektanta zapytań toohello pól i dodawanie filtrów.
- Utwórz nowe miary w tabelach.
- Edytowanie metadanych modelu przy użyciu edytora json hello.
- Otwórz hello modelu w programie Visual Studio (SSDT), Power BI Desktop lub programu Excel.

![Wybierz tabele i widoki](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> Podczas edytowania metadanych modelu lub utworzyć nowe miary w przeglądarce, model tooyour te zmiany są zapisywane na platformie Azure. Jeśli pracujesz także do modelu w SSDT, Power BI Desktop lub programu Excel, modelu można uzyskać zsynchronizowane.


## <a name="next-steps"></a>Następne kroki 
[Zarządzanie ról bazy danych i użytkowników](analysis-services-database-users.md)  
[Łączenie z programem Excel](analysis-services-connect-excel.md)  


