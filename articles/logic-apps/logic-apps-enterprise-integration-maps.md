---
title: "aaaTransform XML przy użyciu map XSLT - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Dodaj XSLT mapy tootransform danych XML przy użyciu usługi Azure Logic Apps i hello pakiet integracyjny dla przedsiębiorstw"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a>Dodaj mapy dla transformacji danych XML

Używa integracji przedsiębiorstwa mapuje dane XML tootransform między formatami. Mapa jest dokument XML, definiujący hello dane w dokumencie, który powinien zostać przekształcone w innym formacie. 

## <a name="why-use-maps"></a>Dlaczego warto używać mapy?

Załóżmy, że regularnie B2B zamówień lub faktur od klienta, który używa hello YYYMMDD format daty. Jednak w organizacji, można przechowywać daty w formacie MMDDYYY hello. Można użyć mapy zbyt*przekształcenie* format daty YYYMMDD hello na powitania MMDDYYY przed przekazaniem szczegółów zamówienia lub faktury hello działania bazy danych klienta.

## <a name="how-do-i-create-a-map"></a>Jak utworzyć mapę?

Możesz utworzyć projektów BizTalk integracji z hello [pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw hello") dla programu Visual Studio 2015. Następnie można utworzyć pliku Mapa integracji programu, który pozwala wizualnie mapy elementów między dwoma plikami schematu XML. Po utworzeniu tego projektu należy dokument XSLT.

## <a name="how-do-i-add-a-map"></a>Jak dodać mapy?

1. Hello portalu Azure, wybierz **Przeglądaj**.

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. W polu wyszukiwania filtr hello, wprowadź **integracji**, a następnie wybierz pozycję **konta integracji** z listy wyników hello.

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. Wybierz konto integracji hello miejscu tooadd hello mapy.

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Wybierz hello **mapy** kafelka.

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. Po otwarciu bloku mapy hello wybierz **Dodaj**.

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. Wprowadź **nazwa** mapy. Mapa hello tooupload plików, wybierz ikonę folderu powitania po prawej stronie powitania hello **mapy** pola tekstowego. Po zakończeniu procesu przekazywania hello wybierz **OK**.

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. Po Azure dodaje hello mapy tooyour integracji konta, zostanie wyświetlony komunikat na ekranie, który pokazuje, czy plik mapy dodano lub nie. Po ten komunikat zostanie wyświetlony, wybierz hello **mapy** Kafelek, aby wyświetlić hello nowo dodany mapy.

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a>Jak edytować mapy?

Musisz przekazać nowy plik mapy z hello żądanych zmian. Można najpierw pobrać hello mapy do edycji.

tooupload nowej mapy, który zastępuje hello istniejącej mapy, wykonaj następujące kroki.

1. Wybierz hello **mapy** kafelka.

2. Po otwarciu bloku mapy hello wybierz hello mapy, które mają tooedit.

3. Na powitania **mapy** bloku, wybierz **aktualizacji**.

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. Selektor plików hello, wybierz plik mapy hello czy tooupload, a następnie wybierz **Otwórz**.

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a>Jak toodelete mapy?

1. Wybierz hello **mapy** kafelka.

2. Po otwarciu bloku mapy hello Wybierz mapę hello ma toodelete.

3. Wybierz **usunąć**.

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. Upewnij się, że chcesz toodelete hello mapy.

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a>Następne kroki
* [Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw")  
* [Dowiedz się więcej na temat umów](../logic-apps/logic-apps-enterprise-integration-agreements.md "więcej informacji na temat umowy integracji dla przedsiębiorstw")  
* [Dowiedz się więcej o transformacji](logic-apps-enterprise-integration-transform.md "Dowiedz się więcej o przedsiębiorstwie transformacje integracji")  

