---
title: "aaaConfigure projekt usługi w chmurze Azure z programem Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure platformy Azure w chmurze projekt usługi w programie Visual Studio, w zależności od wymagań dla tego projektu."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a>Konfigurowanie projektu usługi w chmurze platformy Azure przy użyciu programu Visual Studio
Projekt usługi w chmurze platformy Azure, można skonfigurować w zależności od wymagań dla tego projektu. Można ustawić właściwości hello projektu dla hello następujące kategorie:

- **Publikowanie tooAzure usługi chmury** — można ustawić właściwości toomake się upewnić, że istniejące tooAzure wdrożone usługi chmury nie jest przypadkowo usunięte.
- **Uruchomić ani debugować usługi w chmurze na komputerze lokalnym hello** — możesz wybrać toouse konfiguracji usługi i wskazuje, czy emulatora magazynu Azure hello toostart.
- **Sprawdzanie poprawności pakietu usług chmury po utworzeniu** — można określić tootreat wszystkie ostrzeżenia jako błędy, dzięki czemu można zapewnić tym pakiecie usługi chmury hello wdraża bez żadnych problemów. 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a>Kroki tooconfigure projekt usługi w chmurze Azure
1. Otwarcia lub utworzenia projektu usługi w chmurze w programie Visual Studio

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz z menu kontekstowego hello **właściwości**.
   
1. Na stronie właściwości projektu hello, wybierz hello **programowanie** kartę.

    ![Menu Właściwości projektu](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. Ustaw **Monituj przed usunięciem istniejącego wdrożenia** za**True**. To ustawienie pomaga tooensure nie przypadkowo usuwaj istniejącego wdrożenia na platformie Azure

1. Wybierz hello potrzeby **konfiguracji usługi** tooindicate konfigurację usługi, która ma toouse podczas uruchamiania lub debugowania usługi w chmurze lokalnie. Aby uzyskać więcej informacji na temat toomodify z konfiguracją usługi roli, zobacz [jak tooconfigure hello ról platformy Azure w chmurze usługi z programem Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).

1. Ustaw **emulatora magazynu Start Azure** za**True** toostart hello emulatora magazynu Azure podczas uruchamiania lub debugowania usługi w chmurze lokalnie.

1. Ustaw **Traktuj ostrzeżenia jako błędy** za**True** toomake się, że nie można opublikować, jeśli występują błędy sprawdzania poprawności pakietu.

1. Ustaw **korzystania z portów projektu sieci web** za**True** toomake się, że roli sieci web używany hello sam każdy port czasu rozpoczyna się lokalnie w usługach IIS Express.

1. Z hello narzędzi Visual Studio, wybierz **zapisać**.

## <a name="next-steps"></a>Następne kroki
- [Konfigurowanie projektu platformy Azure przy użyciu wielu konfiguracji usługi](vs-azure-tools-multiple-services-project-configurations.md)

