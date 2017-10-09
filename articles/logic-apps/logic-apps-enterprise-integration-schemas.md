---
title: "aaaSchemas dla sprawdzanie poprawności kodu XML - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Sprawdzanie poprawności dokumentów XML za pomocą schematów dla usługi Azure Logic Apps i pakiet integracyjny dla przedsiębiorstw"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a>Walidacja danych XML o schematach dla usługi Azure Logic Apps i hello pakiet integracyjny dla przedsiębiorstw

Schematy potwierdzić, że dokumenty XML hello otrzymany są prawidłowe i hello oczekiwać dane w formacie wstępnie zdefiniowane. Schematy również pomóc sprawdzania poprawności komunikatów, które są wymieniane w scenariuszu B2B.

## <a name="add-a-schema"></a>Dodawanie schematu

1. Hello portalu Azure, wybierz **więcej usług**.

    ![Portalu Azure, "Więcej usług"](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. W polu wyszukiwania filtr hello, wprowadź **integracji**i wybierz **konta integracji** z listy wyników hello.

    ![Pole wyszukiwania filtru](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. Wybierz hello **konta integracji** miejscu tooadd hello schematu.

    ![Lista kont integracji](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. Wybierz hello **schematy** kafelka.

    ![Przykład integracji konta, "Schematy"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a>Dodaj plik schematu mniejszy niż 2 MB

1. W hello **schematy** bloku, który zostanie otwarty (od hello poprzednich krokach), wybierz **Dodaj**.

    ![Schematy bloku "Dodaj"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. Wprowadź nazwę schematu. Przekaż plik schematu hello wybierając hello folderu ikona dalej toohello **schematu** pole. Po zakończeniu procesu przekazywania hello wybierz **OK**.

    ![Zrzut ekranu przedstawiający "Dodaj Schema", z wyróżnioną pozycją "mały plik"](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a>Dodaj plik schematu większych niż 2 MB (up too8 maksymalnie MB)

Te kroki się różnić w zależności na poziomie dostępu do kontenera obiektów blob hello: **publicznego** lub **dostępu anonimowego**.

**toodetermine ten poziom dostępu**

1.  Otwórz **Eksploratora usługi Azure Storage**. 

2.  W obszarze **kontenerów obiektów Blob**, wybierz kontener obiektów blob hello ma. 

3.  Wybierz **zabezpieczeń**, **poziom dostępu**.

Jeśli poziom dostępu zabezpieczeń obiektu blob hello jest **publicznych**, wykonaj następujące kroki.

![Azure Eksploratora usługi Storage, "Kontenerów obiektów Blob", "Zabezpieczenia" i "Public" wyróżnione](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. Przekaż konta magazynu tooyour schematu hello i skopiuj hello identyfikatora URI.

    ![Konto magazynu o identyfikatorze URI wyróżnione](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. W **Dodaj schemat**, wybierz pozycję **plików o dużym**i podaj hello identyfikatora URI w hello **URI zawartości** pola tekstowego.

    ![Schematy przycisk "Dodaj" i "Dużych plików" wyróżnione](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

Jeśli poziom dostępu zabezpieczeń obiektu blob hello jest **dostępu anonimowego**, wykonaj następujące kroki.

![Azure Eksploratora usługi Storage, "Kontenerów obiektów Blob", "Zabezpieczenia" i "Brak dostępu anonimowego" wyróżnione](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. Przekaż konta magazynu tooyour schematu hello.

    ![Konto magazynu](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. Generowanie sygnatury dostępu współdzielonego dla hello schematu.

    ![Konto magazynu z wyróżnionym kartę sygnatur dostępu współdzielonego](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. W **Dodaj schemat**, wybierz pozycję **plików o dużym**i podaj identyfikator URI sygnatury dostępu współdzielonego hello w hello **URI zawartości** pola tekstowego.

    ![Schematy przycisk "Dodaj" i "Dużych plików" wyróżnione](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. W hello **schematy** blok konta integracji, nowo dodanego schemat powinien zostać wyświetlony.

    ![Konta integracji z "Schematy" i hello wyróżnione nowego schematu.](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a>Edytuj schematów

1. Wybierz hello **schematy** kafelka.

2. Po hello **schematy** zostanie otwarty blok, wybierz hello schematu, które mają tooedit.

3. Na powitania **schematy** bloku, wybierz **Edytuj**.

    ![Schematy bloku](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. Plik schematu hello wybierz, czy tooedit, a następnie wybierz **Otwórz**.

    ![Otwórz schematu pliku tooedit](media/logic-apps-enterprise-integration-schemas/edit-31.png)

Azure wskazuje a wiadomość hello schemat został pomyślnie przekazany.

## <a name="delete-schemas"></a>Usuwanie schematów

1. Wybierz hello **schematy** kafelka.

2. Po hello **schematy** zostanie otwarty blok, wybierz hello schematu ma toodelete.

3. Na powitania **schematy** bloku, wybierz **usunąć**.

    ![Schematy bloku](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. Wybierz pozycję tooconfirm, które mają toodelete hello wybrany schemat **tak**.

    ![Komunikat potwierdzający "Schematu delete"](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    W hello **schematy** bloku hello schematu listy odświeża i nie zawiera już hello schematu, który zostanie usunięty.

    ![Twoje konto, z wyróżnioną pozycją "schematy" integracji](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a>Następne kroki
* [Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw hello").  

