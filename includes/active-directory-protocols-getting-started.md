---
title: "aaaAzure AD Omówienie protokołu .NET | Dokumentacja firmy Microsoft"
description: "Jak toouse HTTP wiadomości tooauthorize dostęp do aplikacji tooweb i interfejsów API sieci web w dzierżawie przy użyciu usługi Azure AD."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/21/2016
ms.author: priyamo
ms.openlocfilehash: 5bd54af028c445afd3f35d67d47d7c84b476c757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## Rejestrowanie aplikacji w dzierżawie usługi AD
Najpierw należy tooregister aplikację z dzierżawą usługi Azure Active Directory (Azure AD). To będzie podać identyfikator aplikacji dla aplikacji, a także włączyć tooreceive tokenów.

* Zaloguj się toohello [Azure Portal](https://portal.azure.com).
* Wybierz dzierżawy usługi Azure AD, klikając na Twoim koncie w hello prawym górnym rogu strony hello.
* W okienku nawigacji po lewej stronie powitania kliknij **usługi Azure Active Directory**.
* Kliknij pozycję **Rejestracje aplikacji**, a następnie kliknij pozycję **Dodaj**.
* Postępuj zgodnie z monitami hello i utworzyć nową aplikację. Na potrzeby tego samouczka nie ma znaczenia, czy jest to aplikacja sieci Web, czy aplikacja natywna, ale jeśli chcesz zapoznać się z konkretnymi przykładami dla aplikacji sieci Web lub aplikacji natywnych, zobacz nasze [przewodniki szybkiego startu](../articles/active-directory/develop/active-directory-developers-guide.md).
  * W przypadku aplikacji sieci Web, podaj hello **adres URL logowania** czyli hello podstawowy adres URL aplikacji, w którym użytkownicy mogą rejestrować w np. `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Dla natywnych aplikacji, podaj **identyfikator URI przekierowania**, które usługi Azure AD będzie używać tooreturn odpowiedzi tokenu. Wprowadź aplikację tooyour określonej wartości. np.`http://MyFirstAADApp`
* Po zakończeniu rejestracji usługi Azure AD będzie przypisany aplikacji unikatowego identyfikatora klienckiego, hello identyfikator aplikacji. Ta wartość będzie potrzebny w kolejnych sekcjach hello, dlatego skopiuj go ze strony aplikacji hello.
