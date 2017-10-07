---
title: Integracja aaaManage konta artefaktu metadanych - Azure Logic Apps | Dokumentacja firmy Microsoft
description: "Dodawanie lub pobrać artefaktu metadanych z konta integracji dla usługi Azure Logic Apps"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8de71bffa9f9975d5409716b2208fa6c3a9545d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a>Zarządzanie artefaktu metadanych w konta integracji dla usługi logic apps

Można zdefiniować niestandardowych metadanych dla artefaktów na kontach integracji i pobrać metadane w czasie wykonywania dla aplikacji logiki. Na przykład można określić metadanych artefaktów, takich jak partnerów, umów, schematów i map — wszystkie sklepu metadanych za pomocą pary klucz wartość. Obecnie usługa artefaktów nie można utworzyć metadanych za pośrednictwem interfejsu użytkownika, ale za pomocą interfejsów API REST toocreate metadanych. metadane tooadd podczas tworzenia lub wybierz partnera, umowy lub schematu w hello portalu Azure, wybierz **edycji w formacie JSON**. tooretrieve artefaktu metadanych w aplikacjach logiki, można użyć funkcji wyszukiwania artefaktu kont integracji hello.

## <a name="add-metadata-tooartifacts-in-integration-accounts"></a>Dodatek tooartifacts metadanych konta integracji

1. Utwórz [konta integracji](logic-apps-enterprise-integration-create-integration-account.md).

2. Na przykład dodać konto artefaktu tooyour integracji, [partnera](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [umowy](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), lub [schematu](logic-apps-enterprise-integration-schemas.md).

3.  Wybierz artefakt hello, wybierz **edycji w formacie JSON**i wprowadź szczegóły metadanych.

    ![Wprowadź metadanych](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a>Pobieranie metadanych z artefaktów dla usługi logic apps

1. Utwórz [aplikacji logiki](logic-apps-create-a-logic-app.md).

2. Utwórz [łącza z Twojego konta integracji tooyour aplikacji logiki](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app). 

3. W Projektancie aplikacji logiki, dodać wyzwalacza, takich jak *żądania* lub *HTTP* tooyour aplikacji logiki.

4.  Wybierz **następnego kroku** > **Dodaj akcję**. Wyszukaj *integracji* , można znaleźć, a następnie wybierz **konta integracji — wyszukiwanie artefaktu konta integracji**.

    ![Wybierz wyszukiwanie artefaktu konta integracji](media/logic-apps-enterprise-integration-metadata/image2.png)

5. Wybierz hello **typu artefaktu**i podaj hello **nazwa artefaktu**.

    ![Wybierz typ artefaktu i określ nazwę artefaktów](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a>Przykład: Pobrać partnera metadanych

Metadane partnera ma `routingUrl` szczegóły:

![Znajdź partnera z metadanych "routingURL"](media/logic-apps-enterprise-integration-metadata/image6.png)

1. W aplikacji logiki, Dodaj Twój wyzwalacz **konta integracji — wyszukiwanie artefaktu konta integracji** akcji dla swojego partnera i **HTTP**.

    ![Dodawanie wyzwalacza, artefaktu wyszukiwania i aplikacji logiki tooyour "HTTP"](media/logic-apps-enterprise-integration-metadata/image4.png)

2. Witaj tooretrieve identyfikatora URI, przejdź tooCode widoku aplikacji logiki. Definicję aplikacji logiki powinna wyglądać następująco:

    ![Wyszukiwanie wyszukiwania](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a>Następne kroki
* [Dowiedz się więcej na temat umów](logic-apps-enterprise-integration-agreements.md "więcej informacji na temat umowy integracji dla przedsiębiorstw")  
