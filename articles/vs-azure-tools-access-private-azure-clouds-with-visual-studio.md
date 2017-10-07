---
title: aaaAccessing prywatnej chmury Azure z programem Visual Studio | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak Chmura prywatna tooaccess zasobów za pomocą programu Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: kraigb
ms.openlocfilehash: 5cfd6439afdcf98c6f7d7f29ab6c4256ed02533a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a>Uzyskiwanie dostępu do chmur prywatnych Azure z programem Visual Studio
Domyślnie program Visual Studio obsługuje punkty końcowe REST chmury publicznej Azure. W tym temacie dowiesz się, jak toouse Twojego Chmura prywatna firmy tooaccess certyfikatu — i interakcję z — Witaj chmury prywatnej w programie Visual Studio.

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a>tooaccess prywatnej Azure w chmurze w programie Visual Studio
1. W hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885) hello chmury prywatnej, Pobierz swój plik ustawień publikowania, lub skontaktuj się z administratorem dla pliku ustawień publikowania. W publicznej wersji hello Azure, hello toodownload łącze jest [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/). (hello pobrany plik ma rozszerzenie `.publishsettings`)

1. Otwórz program Visual Studio

1. W **Eksploratora serwera**, kliknij prawym przyciskiem myszy hello **Azure** węzła i wybierz z menu kontekstowego hello, **zarządzanie i subskrypcje filtru**.
   
    ![Zarządzanie subskrypcjami polecenia](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. W hello **Zarządzanie subskrypcji platformy Microsoft Azure** okno dialogowe, wybierz opcję hello **certyfikaty** , a następnie wybierz **importu**.
   
    ![Importowanie certyfikatów Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. W hello **importu subskrypcji platformy Microsoft Azure** okno dialogowe, wybierz opcję **Przeglądaj**.

    ![Przeglądaj przycisk w oknie dialogowym Import subskrypcji platformy Microsoft Azure hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. W hello **Otwórz** okna dialogowego, toohello przeglądania katalogów, w przypadku, gdy zostanie zapisany hello ustawień publikowania pliku, wybierz opcję hello pliku, a następnie wybierz **Otwórz**.

    ![Wybierz plik ustawień publikowania hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. Gdy zwrócony toohello **importu subskrypcji platformy Microsoft Azure** okno dialogowe, wybierz **importu**.

    ![Plik ustawień publikowania hello importu](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    Witaj certyfikaty są zaimportowane z pliku ustawień publikowania hello do programu Visual Studio, a teraz pozwala na interakcję z zasobami w chmurze prywatnej.
   
## <a name="next-steps"></a>Następne kroki
- [Tooan publikowania usługi w chmurze Azure w programie Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- [Porady: pobieranie i importowanie publikowania ustawienia i informacje o subskrypcji](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)
