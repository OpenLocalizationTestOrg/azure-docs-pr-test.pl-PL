---
title: "Rozwiązywanie problemów z: Tworzenie i łączenie obszaru roboczego uczenia maszynowego tooa | Dokumentacja firmy Microsoft"
description: "Rozwiązania typowych problemów z tworzeniem i łączenie obszaru roboczego uczenia maszynowego Azure tooan"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a>Przewodnik rozwiązywania problemów: tworzenie i łączenie tooan obszaru roboczego uczenia maszynowego
Ten przewodnik zawiera temat rozwiązań dla niektórych często spotykanych problemów podczas konfigurowania obszarów roboczych usługi Azure Machine Learning.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a>Właściciela obszaru roboczego
tooopen obszaru roboczego w usłudze Machine Learning Studio, musi być zalogowany toohello Account Microsoft użyć obszaru roboczego hello toocreate lub należy tooreceive zaproszenia od hello właściciela toojoin hello roboczym. Z portalu Azure, którymi można zarządzać hello hello obszaru roboczego, w tym hello możliwości tooconfigure dostępu.

Aby uzyskać więcej informacji na temat zarządzania obszaru roboczego, zobacz [Zarządzanie obszarem roboczym usługi Azure Machine Learning].

[Zarządzanie obszarem roboczym usługi Azure Machine Learning]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a>Dozwolonych regionów
Usługa Machine Learning jest obecnie dostępna w ograniczonej liczbie regionów. Jeśli subskrypcja nie zawiera jeden z tych regionów, może zostać wyświetlony komunikat błędu Witaj, "Masz żadnych subskrypcji w hello dozwolone regiony."

toorequest, który region można dodać subskrypcji tooyour, Utwórz nowe żądanie pomocy technicznej firmy Microsoft z hello portalu Azure, wybierz **rozliczeń** jako typ problemu hello i wykonaj hello monituje toosubmit Twojego żądania.

## <a name="storage-account"></a>Konto magazynu
Witaj usługi Machine Learning musi toostore konta magazynu danych. Można użyć istniejącego konta magazynu, lub można utworzyć nowe konto magazynu podczas tworzenia obszaru roboczego uczenia maszynowego nowe hello (Jeśli masz toocreate przydziału nowego konta magazynu).

Po utworzeniu obszaru roboczego uczenia maszynowego nowe hello tooMachine Learning Studio można zaloguj przy użyciu konta Microsoft hello używanych toocreate hello roboczym. Jeśli wystąpią komunikat o błędzie hello "Obszaru roboczego nie została odnaleziona" (podobne toohello po zrzut ekranu), użyj hello następujące kroki toodelete pliki cookie przeglądarki.

![Nie można odnaleźć obszaru roboczego][screen3]

**pliki cookie przeglądarki toodelete**

1. Jeśli używasz programu Internet Explorer, kliknij przycisk hello **narzędzia** w prawym górnym rogu hello i wybrać **Opcje internetowe**.  

![Opcje internetowe][screen4]

2. W obszarze hello **ogólne** , kliknij pozycję **usunąć...**

![Karta Ogólne][screen5]

3. W hello **usuwanie historii przeglądania** okna dialogowego upewnij się, **pliki cookie i dane witryn sieci Web** jest zaznaczone, a następnie kliknij przycisk **usunąć**.

![Usuń pliki cookie][screen6]

Po usunięciu plików cookie hello ponowne uruchomienie hello przeglądarki, a następnie przejdź toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) strony. Gdy zostanie wyświetlony monit o nazwę użytkownika i hasło, wprowadź hello tego samego konta Microsoft użyty toocreate hello roboczym.

## <a name="comments"></a>Komentarze

Naszym celem jest toomake hello środowiska usługi Machine Learning jako bezproblemowe, jak to możliwe. Opublikuj uwagi i problemy na powitania [forum usługi Azure Machine Learning](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp nam będą one lepsze.

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
