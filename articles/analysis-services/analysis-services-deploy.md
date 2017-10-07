---
title: "aaaDeploy tooAzure usług Analysis Services przy użyciu narzędzi SSDT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy tooan modelu tabelarycznego Azure Analysis Services serwera za pomocą narzędzi SSDT."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a>Wdrażanie modelu w programie SSDT
Po utworzeniu serwera w ramach subskrypcji platformy Azure, wszystko jest gotowe toodeploy tooit bazy danych modelu tabelarycznego. Można użyć programu SQL Server Data Tools (SSDT) toobuild i Wdróż projekt modelu tabelarycznego, nad którymi pracuje. 

## <a name="prerequisites"></a>Wymagania wstępne
Rozpoczęto tooget, potrzebne są:

* **Serwer usług Analysis Services** na platformie Azure. toolearn więcej, zobacz [Tworzenie serwera usług Azure Analysis Services](analysis-services-create-server.md).
* **Projekt modelu tabelarycznego** SSDT lub istniejącego modelu tabelarycznego na powitania 1200 lub wyższym poziomie zgodności. Nie wiesz, jak go utworzyć? Spróbuj hello [samouczek sprzedaży modelowania tabelarycznym Adventure Works Internet](https://msdn.microsoft.com/library/hh231691.aspx).
* **Brama lokalna** — Jeśli co najmniej jedno źródło danych lokalnych w sieci organizacji, należy tooinstall [bramy danych lokalnych](analysis-services-gateway.md). Brama Hello jest niezbędne, tooyour danych źródeł tooprocess i odświeżania danych lokalnych w modelu hello połączenia z serwerem w chmurze hello.

> [!TIP]
> Przed wdrożeniem, upewnij się, że można przetwarzać hello dane w tabelach. W programie SSDT kliknij opcje **Model** > **Przetwarzaj** > **Przetwarzaj wszystko**. Jeśli przetwarzanie zakończy się niepowodzeniem, wdrożenie nie jest możliwe.
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a>toodeploy modelu tabelarycznego z narzędzi SSDT

1. Przed wdrożeniem, potrzebna jest nazwa serwera hello tooget. W **portalu Azure** > serwera > **omówienie** > **nazwy serwera**, nazwę serwera na powitania kopiowania.
   
    ![Pobieranie nazwy serwera z systemu Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. Programu SSDT > **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello > **właściwości**. Następnie w **wdrożenia** > **serwera** Wklej hello nazwy serwera.   
   
    ![Wklejanie nazwy serwera we właściwościach serwera wdrażania](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy **Właściwości**, a następnie kliknij przycisk **Wdróż**. Zostanie wyświetlony monit o toosign w tooAzure może być.
   
    ![Wdrażanie tooserver](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    Stan wdrożenia pojawia się w oknie danych wyjściowych zarówno hello i wdrażania.
   
    ![Stan wdrożenia](./media/analysis-services-deploy/aas-deploy-status.png)

To wszystko jest tooit!


## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli wdrożenie zakończy się niepowodzeniem, wdrażając metadanych, prawdopodobnie ponieważ SSDT nie może nawiązać połączenia tooyour serwera. Upewnij się, że możesz połączyć tooyour serwera przy użyciu narzędzia SSMS. Upewnij się, że hello właściwość serwera wdrażania projektu hello jest poprawna.

Jeśli wdrożenie zakończy się niepowodzeniem dla tabeli, prawdopodobnie ponieważ serwer nie może nawiązać połączenia tooa źródła danych. Jeśli źródło danych jest lokalnie w sieci organizacji, należy się tooinstall [bramy danych lokalnych](analysis-services-gateway.md).

## <a name="next-steps"></a>Następne kroki
Teraz, gdy masz serwer tooyour wdrożonym modelu tabelarycznego wszystko jest gotowe tooconnect tooit. Możesz [tooit Uzyskuj dostęp do narzędzia SSMS](analysis-services-manage.md) toomanage go. I będzie możliwe [połączyć za pomocą narzędzia klienta tooit](analysis-services-connect.md) , takie jak usługi Power BI, Power BI Desktop lub programu Excel i rozpoczęcia tworzenia raportów.

