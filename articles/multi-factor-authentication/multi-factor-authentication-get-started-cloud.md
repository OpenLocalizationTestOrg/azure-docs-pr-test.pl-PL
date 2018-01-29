---
title: "Wprowadzenie do usługi Azure MFA w chmurze | Microsoft Docs"
description: "Ta strona dotyczy usługi Microsoft Azure Multi-Factor Authentication i zawiera informacje umożliwiające rozpoczęcie korzystania z usługi Azure MFA w chmurze."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: richagi
ms.assetid: 6b2e6549-1a26-4666-9c4a-cbe5d64c4e66
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/24/2017
ms.author: joflore
ms.openlocfilehash: b7c82dc6f09b147651d999a831c657864fa59134
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/04/2018
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-the-cloud"></a>Wprowadzenie do usługi Azure Multi-Factor Authentication w chmurze
W tym artykule opisano, jak rozpocząć korzystanie z usługi Azure Multi-Factor Authentication w chmurze.

> [!NOTE]
> Poniższa dokumentacja zawiera informacje dotyczące umożliwiania użytkownikom korzystania z **witryny Azure Portal**. Jeśli szukasz informacji na temat konfigurowania usługi Azure Multi-Factor Authentication dla użytkowników usługi O365, zobacz temat [Konfigurowanie usługi Multi-Factor Authentication dla usługi Office 365](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US).

![Usługa MFA w chmurze](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a>Wymagania wstępne
[Utworzenie konta na potrzeby subskrypcji platformy Azure](https://azure.microsoft.com/pricing/free-trial/) — jeśli nie masz jeszcze subskrypcji platformy Azure, musisz utworzyć konto. Jeśli dopiero zaczynasz pracę i używasz usługi Azure MFA, możesz skorzystać z subskrypcji wersji próbnej.

## <a name="enable-azure-multi-factor-authentication"></a>Włączanie usługi Azure Multi-Factor Authentication
Dopóki użytkownicy będą mieli licencje obejmujące usługę Azure Multi-Factor Authentication, do jej włączenia nie będzie wymagane wykonanie żadnych czynności. Możliwe jest rozpoczęcie wymagania weryfikacji dwuetapowej dla indywidualnych użytkowników. Licencje, które umożliwiają włączenie usługi Azure MFA, to:
- Azure Multi-Factor Authentication
- Usługa Azure Active Directory Premium
- Enterprise Mobility + Security

Jeśli nie masz żadnej z tych trzech licencji ani nie masz wystarczającej liczby licencji, aby obejmowały wszystkich użytkowników, to też nie stanowi problemu. Konieczne jest tylko wykonanie dodatkowego kroku w celu [utworzenia dostawcy usługi Multi-Factor Authentication](multi-factor-authentication-get-started-auth-provider.md) w katalogu.

## <a name="turn-on-two-step-verification-for-users"></a>Włączanie weryfikacji dwuetapowej dla użytkowników

Wykonaj jedną z procedur wymienionych w temacie [How to require two-step verification for a user or group (Jak wymagać weryfikacji dwuetapowej użytkownika lub grupy)](multi-factor-authentication-get-started-user-states.md), aby rozpocząć korzystanie z usługi Azure MFA. Weryfikację dwuetapową możesz wymusić dla wszystkich logowań lub utworzyć zasady dostępu warunkowego, które wymuszają weryfikację dwuetapową tylko wtedy, gdy jest to pożądane.

## <a name="next-steps"></a>Następne kroki
Po skonfigurowaniu usługi Azure Multi-Factor Authentication w chmurze można przystąpić do konfigurowania wdrożenia. Aby uzyskać bardziej szczegółowe informacje, zobacz temat [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) (Konfigurowanie usługi Azure Multi-Factor Authentication).

