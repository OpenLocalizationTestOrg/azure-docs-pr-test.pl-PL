---
title: wprowadzenie do programu Microsoft Power BI Embedded aaaGet
description: "Usługa Power BI Embedded — dodawanie interaktywnych raportów usługi Power BI do aplikacji analizy biznesowej"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a>Wprowadzenie do usługi Microsoft Power BI Embedded

**Power BI Embedded** jest usługą platformy Azure z tym tooadd deweloperzy aplikacji umożliwia raporty interakcyjne usługi Power BI do własnych aplikacji. **Power BI Embedded** Zaloguj współpracuje z istniejącymi aplikacjami bez konieczności one lub zmiana hello użytkowników.

Zasoby dla **Microsoft Power BI Embedded** za pośrednictwem hello [API Azure ARM](https://msdn.microsoft.com/library/mt712306.aspx). W tym przypadku jest udostępnianie zasobów hello **kolekcji obszarów roboczych usługi Power BI**.

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a>Tworzenie kolekcji obszarów roboczych

A **kolekcji obszarów roboczych** jest hello najwyższego poziomu zasobem platformy Azure i kontenerem zawartości hello, która zostanie osadzona w aplikacji. **Kolekcję obszarów roboczych** można utworzyć na dwa sposoby:

* Ręcznie przy użyciu hello portalu Azure
* Programowo przy użyciu hello interfejsów API usługi Azure Resource Manager (ARM)

Przejdźmy hello kroki toobuild **kolekcji obszarów roboczych** przy użyciu hello portalu Azure.

1. Otwórz witrynę **Azure Portal**: [http://portal.azure.com](http://portal.azure.com) i zaloguj się.
2. Kliknij przycisk **+ nowy** na powitania górnym panelu.
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. W obszarze **Dane i analizy** kliknij opcję **Power BI Embedded**.
4. Na powitania **bloku kolekcji obszarów roboczych**, wprowadź hello wymagane informacje. Aby poznać **ceny**, zobacz [Usługa Power BI Embedded — cennik](http://go.microsoft.com/fwlink/?LinkID=760527).
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. Kliknij przycisk **Utwórz**.

Witaj **kolekcji obszarów roboczych** potrwa kilka chwil tooprovision. Po zakończeniu spowoduje przekierowanie toohello **bloku kolekcji obszarów roboczych**.

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

Witaj **blok tworzenia** informacjami hello należy toocall hello interfejsów API służących do tworzenia obszarów roboczych i wdrażania toothem zawartości.

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a>Wyświetlanie kluczy dostępu interfejsu API usługi Power BI

Jeden z hello najważniejsze elementy toocall informacje potrzebne hello API REST usługi Power BI są hello **klucze dostępu**. Są one używane toogenerate hello **tokenów aplikacji** , które są używane tooauthenticate żądań interfejsu API. tooview Twojego **klucze dostępu**, kliknij przycisk **klucze dostępu** na powitania **bloku ustawienia**. Aby uzyskać więcej informacji o **tokenach aplikacji**, zobacz [Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded](power-bi-embedded-app-token-flow.md).

   ![](media/power-bi-embedded-get-started/access-keys.png)

Zauważysz, że masz dwa klucze.

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

Skopiuj te klucze i przechowuj je bezpiecznie w aplikacji. Jest bardzo ważne, aby traktować te klucze jak hasła, ponieważ będzie zapewniają dostęp do tooall hello zawartości w Twojej **kolekcji obszarów roboczych**.

Chociaż wyświetlane są dwa klucze, w określonym czasie potrzebny jest tylko jeden. Witaj drugi klucz jest dostarczany, więc można okresowo generować ponownie klucze bez przerywania dostępu toohello usługi.

Teraz, gdy masz wystąpienie usługi Power BI dla danej aplikacji oraz **klucze dostępu**, możesz zaimportować raport do aplikacji. Przed dowiesz się, jak tooimport, a raport, hello następnej sekcji opisano tworzenie tooembed zestawów danych i raportów usługi Power BI do aplikacji.

## <a name="working-with-workspaces"></a>Praca z obszarami roboczymi

Po utworzeniu kolekcji obszaru roboczego, konieczne będzie toocreate obszaru roboczego, który będzie zawierać raporty i zestawy danych programu. toocreate obszaru roboczego, konieczne będzie toouse hello [interfejsu API REST Worksapce Post](https://msdn.microsoft.com/library/azure/mt711503.aspx).

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a>Utwórz tooembed zestawów danych i raportów usługi Power BI do aplikacji za pomocą Power BI Desktop

Teraz, gdy masz utworzone wystąpienie usługi Power BI dla aplikacji i mieć **klucze dostępu**, konieczne będzie toocreate hello usługi Power BI z zestawów danych i raportów, które mają tooembed. Zestawy danych i raporty można tworzyć za pomocą programu **Power BI Desktop**. Możesz pobrać program [Power BI Desktop za darmo](https://go.microsoft.com/fwlink/?LinkId=521662). Lub, tooquickly rozpocząć pracę, możesz pobrać hello [Retail Analysis próbki PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).

> [!NOTE]
> więcej informacji na temat toolearn toouse **Power BI Desktop**, zobacz [wprowadzenie Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).

Z **Power BI Desktop**, Połącz źródła danych tooyour importując kopię danych hello do **Power BI Desktop** lub bezpośrednio łącząc toohello danych źródła przy użyciu **DirectQuery**.

Poniżej przedstawiono różnice hello przy użyciu **importu** i **DirectQuery**.

| Import | Tryb DirectQuery |
| --- | --- |
| Tabele, kolumny, *i dane* są importowane lub kopiowane do programu **Power BI Desktop**. Podczas pracy nad wizualizacjami program **Power BI Desktop** kopii danych hello zapytań. toosee wszelkie zmiany danych podstawowych toohello wystąpił, należy odświeżyć lub zaimportować pełny bieżący zestaw danych ponownie. |Tylko *tabele i kolumny* są importowane lub kopiowane do programu **Power BI Desktop**. Podczas pracy nad wizualizacjami program **Power BI Desktop** zapytania hello źródła danych, co oznacza zawsze wyświetlana bieżące dane. |

Aby uzyskać więcej informacji o źródle danych tooa łączącego zobacz [źródła danych tooa Connect](power-bi-embedded-connect-datasource.md).

Po zapisaniu pracy w programie **Power BI Desktop** tworzony jest plik PBIX. Ten plik zawiera raport. Ponadto po zaimportowaniu hello danych plik PBIX zawiera pełen zestaw hello lub jeśli używasz **DirectQuery**, hello plik PBIX zawiera tylko schemat zestawu danych. Programowe wdrażanie hello PBIX do obszaru roboczego przy użyciu hello [API Import usługi Power BI](https://msdn.microsoft.com/library/mt711504.aspx).

> [!NOTE]
> **Power BI Embedded** ma dodatkowe interfejsy API toochange powitania serwera i bazy danych, czy zestaw danych wskazuje zestaw tooand poświadczenia konta usługi hello zestawu danych będzie używać tooconnect tooyour w bazie danych. Zobacz artykuły dotyczące operacji [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) i [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).

## <a name="create-power-bi-datasets-and-reports-using-apis"></a>Tworzenie zestawów danych i raportów usługi Power BI za pomocą interfejsów API

### <a name="datsets"></a>Zestawy danych

Można utworzyć zestawy danych w usłudze Power BI Embedded przy użyciu hello interfejsu API REST. Następnie można wypchnąć dane do własnego zestawu danych. Dzięki temu toowork z danymi bez konieczności hello programu Power BI Desktop. Aby uzyskać więcej informacji, zobacz: [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx) (Wysyłanie zestawów danych za pomocą żądania POST).

### <a name="reports"></a>Raporty

Można utworzyć raport z zestawu danych bezpośrednio w aplikacji przy użyciu hello JavaScript API. Aby uzyskać więcej informacji, zobacz [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Tworzenie nowego raportu z zestawu danych w usłudze Power BI Embedded).

## <a name="see-also"></a>Zobacz też

[Rozpoczęcie pracy z przykładem](power-bi-embedded-get-started-sample.md)  
[Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Embed a report](power-bi-embedded-embed-report.md) (Osadzanie raportu)  
[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Tworzenie nowego raportu z zestawu danych w usłudze Power BI Embedded) 
[Save reports](power-bi-embedded-save-reports.md) (Zapisywanie raportów)  
[Program Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Przykład osadzania skryptu JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Masz więcej pytań? [Spróbuj hello Power BI społeczności](http://community.powerbi.com/)

