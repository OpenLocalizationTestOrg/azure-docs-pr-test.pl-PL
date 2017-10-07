---
title: "aaaGet uruchomione usługi Azure MFA w chmurze hello | Dokumentacja firmy Microsoft"
description: "Jest to hello Microsoft Azure Multi-Factor authentication strony, opisujące, jak tooget pracę z usługą Azure MFA w chmurze hello."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 6b2e6549-1a26-4666-9c4a-cbe5d64c4e66
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/24/2017
ms.author: kgremban
ms.openlocfilehash: a4aaf44bf08d96f2baad155072fdd6e0e727ce8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-hello-cloud"></a>Wprowadzenie do korzystania z usługi Azure Multi-Factor Authentication w chmurze hello
W tym artykule przedstawiono sposób uruchamiania przy użyciu usługi Azure Multi-Factor Authentication w chmurze hello tooget.

> [!NOTE]
> Hello Poniższa dokumentacja zawiera informacje na temat sposobu hello tooenable użytkowników przy użyciu **klasycznego portalu Azure**. Jeśli szukasz informacji na temat tooset zapasowej Azure Multi-Factor Authentication dla użytkowników usługi Office 365, zobacz [skonfigurować usługę Multi-Factor authentication dla usługi Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)

![Uwierzytelniania MFA w chmurze hello](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a>Wymagania wstępne
[Załóż subskrypcji platformy Azure](https://azure.microsoft.com/pricing/free-trial/) — Jeśli nie masz już subskrypcję platformy Azure, należy dla jednej toosign w górę. Jeśli dopiero zaczynasz pracę i używasz usługi Azure MFA, możesz skorzystać z subskrypcji wersji próbnej.

## <a name="enable-azure-multi-factor-authentication"></a>Włączanie usługi Azure Multi-Factor Authentication
Tak długo, jak użytkownicy mają licencje, które obejmują usługi Azure Multi-Factor Authentication, nie ma nic konieczność tooturn toodo na usługę Azure MFA. Możliwe jest rozpoczęcie wymagania weryfikacji dwuetapowej dla indywidualnych użytkowników. licencje Hello, które umożliwiają usługi Azure MFA są:
- Azure Multi-Factor Authentication
- Usługa Azure Active Directory Premium
- Enterprise Mobility + Security

Jeśli nie masz żadnego z tych trzech licencji lub nie ma wystarczającej liczby licencji toocover wszystkich użytkowników, które ok zbyt. Wystarczy toodo dodatkowego kroku i [Tworzenie dostawcy uwierzytelniania wieloskładnikowego](multi-factor-authentication-get-started-auth-provider.md) w katalogu.

## <a name="turn-on-two-step-verification-for-users"></a>Włączanie weryfikacji dwuetapowej dla użytkowników

Jedną z procedur hello na liście [jak toorequire weryfikacji dwuetapowej dla użytkownika lub grupy](multi-factor-authentication-get-started-user-states.md) toostart przy użyciu usługi Azure MFA. Możesz wybrać tooenforce weryfikacji dwuetapowej dla wszystkich logowania lub weryfikacji dwuetapowej toorequire zasady dostępu warunkowego można utworzyć tylko wtedy, gdy ma znaczenia, tooyou.

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy mają skonfigurowane uwierzytelnianie wieloskładnikowe Azure w chmurze hello, można skonfigurować i skonfigurować wdrożenie. Aby uzyskać bardziej szczegółowe informacje, zobacz temat [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) (Konfigurowanie usługi Azure Multi-Factor Authentication).

