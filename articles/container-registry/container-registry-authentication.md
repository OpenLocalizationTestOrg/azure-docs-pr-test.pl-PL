---
title: aaaAuthenticate z rejestru kontenera platformy Azure | Dokumentacja firmy Microsoft
description: "Jak toolog tooan rejestru kontenera platformy Azure przy użyciu usługi Azure Active Directory usługi podmiot zabezpieczeń lub konto administratora"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a>Uwierzytelniania za pomocą prywatnego rejestru kontenera Docker
toowork z obrazami kontenera w rejestrze kontenera platformy Azure, możesz Zaloguj się za pomocą hello `docker login` polecenia. Możesz zalogować się przy użyciu  **[nazwy głównej usługi Azure Active Directory](../active-directory/active-directory-application-objects.md)**  specyficznych rejestru lub **konto administratora**. Ten artykuł zawiera szczegółowe informacje o tych tożsamości.



## <a name="service-principal"></a>Nazwy głównej usługi

Możesz [przypisać nazwy głównej usługi](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour rejestru i użyć jej do uwierzytelniania podstawowego Docker. Przy użyciu nazwy głównej usługi jest zalecane w przypadku większości scenariuszy. Podaj identyfikator aplikacji hello i hasło toohello główna usługi hello `docker login` polecenia, jak pokazano w hello poniższy przykład:

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Po zalogowaniu, Docker buforuje poświadczeń hello, więc nie trzeba identyfikator tooremember hello aplikacji.

> [!TIP]
> Jeśli chcesz, można ponownie wygenerować hasła hello nazwy głównej usługi uruchamiając hello `az ad sp reset-credentials` polecenia.
>


Zezwalaj na nazwy główne usług [dostępu opartej na rolach](../active-directory/role-based-access-control-configure.md) tooa rejestru. Dostępne role są:
  * Czytnik (dostęp tylko ściągania).
  * Współautor (ściągania i wypychania).
  * Właściciel (ściągania, wypychania i przypisz role tooother użytkowników).

Dostęp anonimowy nie jest dostępna w rejestrach kontenera platformy Azure. Obrazy publiczne można użyć [Centrum Docker](https://docs.docker.com/docker-hub/).

Można przypisać wiele podmiotów usługi rejestru tooa, dzięki czemu można toodefine dostępu dla różnych użytkowników lub aplikacji. Nazwy główne usług również włączyć łączność "bezobsługowe" klucza rejestru tooa deweloperem lub DevOps scenariuszy, takich jak hello następujące przykłady:

  * Kontener wdrożenia z systemów tooorchestration rejestru, w tym DC/OS, Docker Swarm i Kubernetes. Można również umieścić toorelated rejestrów kontenera usług Azure takich jak [usługi kontenera](../container-service/index.yml), [usługi aplikacji](../app-service/index.md), [partii](../batch/index.md), [sieci szkieletowej usług](/azure/service-fabric/)i inne.

  * Ciągłej integracji i wdrażania rozwiązań (np. programu Visual Studio Team Services lub Wpięć) tworzące kontener obrazów i wypychanie ich tooa rejestru.





## <a name="admin-account"></a>Konto administratora
Z każdym rejestru utworzone konto administratora pobiera tworzone automatycznie. Domyślnie konto hello jest wyłączone, ale można ją włączyć i zarządzać nimi poświadczeń hello, na przykład za pomocą hello [portal](container-registry-get-started-portal.md#manage-registry-settings) lub przy użyciu hello [poleceń Azure CLI 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials). Każde konto administratora jest udostępniane z dwóch haseł, które może być generowany ponownie. dwa hasła Hello pozwalają toomaintain połączeń toohello rejestru za pomocą jednego hasła podczas ponownego generowania hello inne hasło. Jeśli konto hello jest włączone, można przekazać hello nazwy użytkownika i toohello albo hasło `docker login` polecenia dla uwierzytelniania podstawowego toohello rejestru. Na przykład:

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> konto administratora Hello jest przeznaczony do rejestru hello tooaccess pojedynczego użytkownika, głównie do celów testowych. Nie jest zalecane poświadczeń konta administratora hello tooshare wśród innych użytkowników. Wszyscy użytkownicy są wyświetlane jako rejestru toohello jednego użytkownika. Zmiana lub wyłączenie tego konta spowoduje wyłączenie dostępu do rejestru dla wszystkich użytkowników, którzy używają hello poświadczeń.
>


### <a name="next-steps"></a>Następne kroki
* [Wypychanie pierwszy obraz przy użyciu interfejsu wiersza polecenia Docker hello](container-registry-get-started-docker-cli.md).
* Aby uzyskać więcej informacji na temat uwierzytelniania w wersji zapoznawczej rejestru kontenera hello Zobacz hello [wpis w blogu](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).
