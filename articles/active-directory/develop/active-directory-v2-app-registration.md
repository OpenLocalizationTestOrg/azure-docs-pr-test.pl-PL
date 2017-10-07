---
title: "aaaRegister aplikacji z punktem końcowym v2.0 hello Azure AD przy użyciu portalu hello | Dokumentacja firmy Microsoft"
description: "Jak usługi przy użyciu punktu końcowego v2.0 hello tooregister aplikacji z firmą Microsoft za włączanie logowania i uzyskiwania dostępu do firmy Microsoft"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a>Jak tooregister aplikacji z punktem końcowym v2.0 hello
toobuild aplikację, która akceptuje zarówno zarządzanych kont usług, jak i usługi Azure AD logowanie, musisz najpierw tooregister aplikacji z firmą Microsoft.  W tej chwili nie być możliwe toouse wszelkie istniejące aplikacje mogą wiązać Ciebie z usługi Azure AD lub MSA — należy toocreate brand nową.

> [!NOTE]
> Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez hello punktu końcowego v2.0.  toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a>Odwiedź portal rejestracji aplikacji Microsoft hello
Przede wszystkim za Przejdź najpierw -[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).  Jest to nowy portal rejestracji aplikacji, gdzie zarządzalnych aplikacji firmy Microsoft.

Zaloguj się przy użyciu albo osobistego lub służbowe konto Microsoft.  Jeśli nie masz albo utworzyć nowe konto osobiste. Teraz, nie potrwa długo — poczekamy tutaj.

Zrobić? Powinny teraz można patrzy listę aplikacji firmy Microsoft, który jest prawdopodobnie puste.  Ta funkcja pozwala zmienić.

Kliknij przycisk **Dodaj aplikację**i nadaj mu nazwę.  Hello portal przypisze globalnie unikatowy identyfikator aplikacji, który będzie potrzebny później w kodzie aplikacji.  Jeśli aplikacja zawiera składnik po stronie serwera wymaga tokenów dostępu dla wywołania interfejsów API (wziąć pod uwagę: Office, Azure lub własnego interfejsu API sieci web), należy toocreate **klucz tajny aplikacji** również w tym miejscu.

Następnie dodaj hello platformy, które będą korzystać z aplikacji.

* W przypadku aplikacji sieci web, podaj **identyfikator URI przekierowania** wysyłania komunikatów do logowania.
* Dla aplikacji mobilnych skopiuj domyślny hello przekierowania uri utworzony automatycznie.

Opcjonalnie można dostosować hello wygląd i działanie strony logowania w hello profilu.  Upewnij się, że tooclick **zapisać** przed kontynuowaniem.

> [!NOTE]
> Po utworzeniu aplikacji przy użyciu [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), hello aplikacja zostanie zarejestrowana w dzierżawie macierzystego hello hello konta Użyj toosign hello portalu.  Oznacza to, że nie można zarejestrować aplikację w dzierżawie usługi Azure AD za pomocą osobistego konta Microsoft.  Jeśli jawnie tooregister aplikacji w szczególności dzierżawy, zaloguj się przy użyciu konta, które pierwotnie utworzone w tej dzierżawie.
> 
> 

## <a name="build-a-quick-start-app"></a>Tworzenie aplikacji szybki start
Teraz, gdy masz aplikacji firmy Microsoft, można wykonać jedną z naszych samouczków szybkiego startu v2.0.  Poniżej przedstawiono kilka zaleceń:

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

