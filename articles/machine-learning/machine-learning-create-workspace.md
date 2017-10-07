---
title: "aaaCreate obszaru roboczego usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Jak toocreate obszaru roboczego dla usługi Azure Machine Learning Studio"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a>Tworzenie obszaru roboczego usługi Azure Machine Learning i zarządzanie nim
W tym menu łączy tootopics, które opisują sposób tooset się hello różnych środowiskach nauki danych przez hello Cortana Analytics procesu (CAP).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

toouse Azure Machine Learning Studio, należy toohave obszaru roboczego uczenia maszynowego. Ten obszar roboczy zawiera narzędzia hello należy toocreate, zarządzania i publikowania eksperymentów.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a>toocreate obszaru roboczego
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/)

    > [!NOTE]
    > toosign w i tworzenie obszaru roboczego, należy toobe administratorem subskrypcji platformy Azure. 
    >
    > 

2. Kliknij przycisk **+ nowy**

3. Wybierz **analizy i analiza**, kliknij przycisk **obszaru roboczego uczenia maszyny**, następnie kliknij przycisk **Utwórz**

4. Wprowadź informacje obszaru roboczego

    - Witaj *nazwa obszaru roboczego* może być aktywne too260 znaków, nie kończy się spacją. Witaj, nazwa nie może zawierać następujących znaków:`< > * % & : \ ? + /`
    - Witaj *plan usługi sieci web* możesz wybrać (lub Utwórz), wraz z hello skojarzone *warstwy cenowej* wybrać, jest używany w przypadku wdrożenia usługi sieci web z obszaru roboczego.

    ![Tworzenie nowego obszaru roboczego](media/machine-learning-create-workspace/create-new-workspace.png)

5. Kliknij przycisk **Utwórz**

Po wdrożeniu hello obszaru roboczego można otworzyć go w usłudze Machine Learning Studio.

1. Przeglądaj tooMachine Learning Studio w [https://studio.azureml.net/](https://studio.azureml.net/).

2. Wybierz obszar roboczy w hello prawej górnym rogu.

    ![Wybierz obszar roboczy](media/machine-learning-create-workspace/open-workspace.png)

3. Kliknij przycisk **eksperymenty**.

    ![Otwórz eksperymenty](media/machine-learning-create-workspace/my-experiments.png)

Informacje o zarządzaniu obszaru roboczego, zobacz [Zarządzanie obszarem roboczym usługi Azure Machine Learning](machine-learning-manage-workspace.md).
Jeśli napotkasz problem podczas tworzenia obszaru roboczego, zobacz [przewodnik rozwiązywania problemów: tworzenie i łączenie obszaru roboczego uczenia maszynowego tooa](machine-learning-troubleshooting-creating-ml-workspace.md).


## <a name="sharing-an-azure-machine-learning-workspace"></a>Udostępnianie obszaru roboczego uczenia maszynowego Azure
Po utworzeniu obszaru roboczego uczenia maszynowego można zaprosić użytkowników tooyour obszaru roboczego tooshare dostępu tooyour roboczym i wszystkie jego eksperymentów, zestawy danych, notesy itp. Można dodać użytkowników, w jednym z dwóch ról:

* **Użytkownik** -użytkownika obszar roboczy można utworzyć, Otwórz, zmodyfikuj i Usuń eksperymentów, zestawy danych itp., w obszarze roboczym hello.
* **Właściciel** — poprosić właściciela i usuwać użytkowników w obszarze roboczym hello toowhat dodanie użytkownika mogą wykonywać.

> [!NOTE]
> konto administratora Hello tworzy hello obszaru roboczego jest automatycznie dodawany toohello obszaru roboczego jako właściciela obszaru roboczego. Jednak innych administratorów lub użytkowników w tej subskrypcji nie są automatycznie udzielony dostęp roboczym toohello — należy tooinvite je jawnie.
> 
> 

### <a name="tooshare-a-workspace"></a>tooshare obszaru roboczego

1. Zaloguj się tooMachine Learning Studio w [https://studio.azureml.net/Home](https://studio.azureml.net/Home)

2. W lewym panelu powitania kliknij **ustawienia**

3. Kliknij przycisk hello **użytkowników** kartę

4. Kliknij przycisk **ZAPROSIĆ użytkowników więcej** u dołu hello hello strony

    ![Ustawienia Studio](media/machine-learning-create-workspace/settings.png)

5. Wprowadź co najmniej jeden adres e-mail. Hello wymaga prawidłowego konta Microsoft lub konta organizacyjnego (z usługą Azure Active Directory).

6. Wybierz, czy użytkownicy hello tooadd jako właściciela lub użytkowników.

7. Kliknij przycisk hello **OK** przycisk znacznika wyboru.

Każdy użytkownik dodawany otrzymają wiadomość e-mail z instrukcjami dotyczącymi sposobu toosign w toohello udostępniony obszar roboczy.

> [!NOTE]
> Dla toodeploy stanie toobe użytkowników lub zarządzania usługami sieci web, w tym obszarze roboczym, muszą być współautora lub administratora w hello subskrypcji platformy Azure. 



