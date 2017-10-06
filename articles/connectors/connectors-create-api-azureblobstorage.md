---
title: "Witaj aaaAdd magazynu obiektów blob Azure łącznika w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Rozpoczęcie pracy i skonfigurować łącznik magazynu obiektów blob platformy Azure hello w aplikacji logiki"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a>Użyj łącznika magazynu obiektów blob platformy Azure hello w aplikacji logiki
Użyj hello Azure Blob magazynu łącznika tooupload aktualizacji, Pobierz i usuwanie obiektów blob na koncie magazynu, w całości mieści się w aplikacji logiki.  

Z magazynu obiektów blob platformy Azure możesz:

* Tworzenie przepływu pracy przez przekazanie nowych projektów lub pobieranie plików, które zostały niedawno zaktualizowane.
* Użyj akcji tooget pliku metadanych, usuń plik, kopiowania plików i inne. Na przykład po zaktualizowaniu narzędzie Azure witryny sieci web (wyzwalacz) zaktualizować pliku w magazynie obiektów blob (działanie). 

W tym temacie pokazano, jak toouse hello obiektu blob magazynu łącznika w aplikacji logiki.

toolearn więcej informacji na temat aplikacji logiki, zobacz [co to jest logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

toolearn więcej informacji na temat aplikacji logiki, zobacz [co to jest logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooazure-blob-storage"></a>Połącz tooAzure magazynu obiektów blob
Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw utworzyć *połączenia* toohello usługi. Połączenie stanowi połączenie między aplikacji logiki i innej usługi. Na przykład tooconnect tooa konta magazynu, należy najpierw utworzyć magazynu obiektów blob *połączenia*. toocreate połączenie, wprowadź poświadczenia hello tooaccess hello usługi, którą jest nawiązywane zwykle jest używana. Dlatego z usługą Azure storage, należy wprowadzić hello poświadczenia tooyour konta toocreate hello połączenia z magazynem. 

#### <a name="create-hello-connection"></a>Utwórz połączenie hello
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a>Użyć wyzwalacza
Ten łącznik nie ma żadnych wyzwalaczy. Użyj innych wyzwalaczy toostart hello aplikacji logiki, takie jak wyzwalacz cyklu wyzwalacza HTTP elementu Webhook, wyzwalaczy dostępny z innych łączników i inne. [Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) przykładowego.

## <a name="use-an-action"></a>Za pomocą akcji
Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji.

1. Wybierz znak plus hello. Zobacz kilka opcji: **Dodaj akcję**, **Dodaj warunek**, lub jeden z hello **więcej** opcje.
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. Wybierz **Dodaj akcję**.
3. W polu tekstowym hello wpisz "blob" tooget listę wszystkich hello dostępne akcje.
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. W tym przykładzie wybierz **AzureBlob - Get metadanych pliku przy użyciu ścieżki**. Jeśli połączenie już istnieje, a następnie wybierz hello **...** (Pokaż selektora) przycisk tooselect pliku.
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    Jeśli zostanie wyświetlony monit o informacje o połączeniu hello, wprowadź hello szczegóły toocreate hello połączenia. [Utwórz połączenie hello](connectors-create-api-azureblobstorage.md#create-the-connection) w tym temacie opisano te właściwości. 
   
   > [!NOTE]
   > W tym przykładzie uzyskujemy hello metadane pliku. toosee hello metadanych, Dodaj inną akcję, która tworzy nowy plik przy użyciu innego łącznika. Na przykład dodać akcję OneDrive, która tworzy nowy plik "test" na podstawie hello metadanych. 


5. **Zapisz** zmiany (lewym górnym rogu paska narzędzi hello). Aplikację logiki jest zapisywana i automatycznie włączone.

> [!TIP]
> [Eksplorator usługi Storage](http://storageexplorer.com/) to doskonałe narzędzie Zarządzanie zbyt wiele kont magazynu.

## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/azureblobconnector/). 

## <a name="next-steps"></a>Następne kroki
[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md). Eksploruj hello innych dostępnych łączników w aplikacjach logiki w naszym [listy interfejsów API](apis-list.md).

