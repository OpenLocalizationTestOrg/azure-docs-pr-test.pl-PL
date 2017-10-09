---
title: "aaaConfigure uwierzytelniania za pomocą usług Amazon Web Services | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocreate i sprawdzanie poprawności poświadczeń usług AWS dla elementów runbook w automatyzacji Azure zarządzanie zasobami usług AWS."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: uwierzytelnianie aws, konfigurowanie aws
ms.assetid: b6dde4bb-26ac-4876-9aa9-e586bed30d6b
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: 1e312df2422d9da3cd3331fe01aeaa3a43c8b9d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-amazon-web-services"></a>Uwierzytelnianie elementów Runbook w usłudze Amazon Web Services
Typowe zadania dotyczące zasobów w usłudze Amazon Web Services (AWS) można zautomatyzować za pomocą elementów Runbook usługi Azure Automation.  Wiele zadań w usłudze AWS można zautomatyzować przy użyciu elementów Runbook usługi Automation, podobnie jak za pomocą zasobów platformy Azure.  Wymagane są jedynie dwa elementy:

* Subskrypcja AWS i zestaw poświadczeń.  W szczególności klucz dostępu AWS i klucz tajny.  Aby uzyskać więcej informacji, przejrzyj artykuł hello [przy użyciu poświadczeń usług AWS](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html).
* Subskrypcja platformy Azure i konto w usłudze Automation.  Aby uzyskać więcej informacji na temat konfigurowania konta usługi Automatyzacja Azure, przejrzyj artykuł hello [skonfigurować Azure konta Uruchom jako](automation-sec-configure-azure-runas-account.md).  

tooauthenticate z usług AWS, należy określić zestaw usług AWS poświadczenia tooauthenticate elementy runbook uruchomione usługi Automatyzacja Azure. Jeśli masz już konto usługi Automatyzacja tworzone, i chcesz toouse tego tooauthenticate z usług AWS, może wykonać kroki hello w hello następujących sekcji.  Jeśli chcesz toodedicated konta dla elementów runbook dotyczących usług AWS zasobów, należy najpierw utworzyć nową [konto automatyzacji](automation-offering-get-started.md) (Pomiń hello opcja toocreate nazwy głównej usługi), a następnie wykonaj poniższe kroki hello.

## <a name="configure-automation-account"></a>Skonfiguruj konto usługi Automation
Dla usługi Automatyzacja Azure toocommunicate z usług AWS należy najpierw tooretrieve poświadczeń usług AWS i zapisać je jako zasoby w automatyzacji Azure.  Wykonaj hello, wykonaj czynności opisane w dokumencie usług AWS hello [Zarządzanie klucze dostępu dla konta usług AWS](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) toocreate hello klucz dostępu i skopiuj **identyfikator klucza dostępu** i **klucz tajny klucz dostępu** (opcjonalnie pobrać toostore Twojego pliku klucza go w bezpiecznym miejscu).

Po utworzeniu i skopiować klucze zabezpieczeń usług AWS należy toocreate zasobu poświadczeń z toosecurely konto usługi Automatyzacja Azure przechowywać je i odwoływać je z elementy runbook.  Wykonaj kroki hello w sekcji hello **toocreate nowe poświadczenie** w hello [poświadczeń zasoby w automatyzacji Azure](automation-credentials.md#to-create-a-new-credential-asset-with-the-azure-portal) artykuł, a następnie wprowadź hello następujących informacji:

1. W hello **nazwa** wprowadź **AWScred** lub odpowiednią wartość następujące standardy nazewnictwa.  
2. W hello **nazwy użytkownika** wpisz Twojej **identyfikator dostępu** i **klucz tajny klucz dostępu** w hello **hasło** i **Potwierdź hasło** pole.   

## <a name="next-steps"></a>Następne kroki
* Artykuł rozwiązania hello monitującymi [automatyzacji wdrażania maszyny Wirtualnej w ramach usług Amazon Web Services](automation-scenario-aws-deployment.md) toolearn jak toocreate tooautomate elementów runbook zadania w programie usług AWS.

