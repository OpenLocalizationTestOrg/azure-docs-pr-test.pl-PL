---
title: Uwierzytelnianie systemu Windows i serwer Azure MFA | Microsoft Docs
description: "Ta strona jest poświęcona usłudze Azure Multi-Factor Authentication i zawiera informacje pomocne podczas wdrażania uwierzytelniania systemu Windows i korzystania z serwera usługi Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: joflore
ms.reviewer: richagi
ms.custom: it-pro
ms.openlocfilehash: ae4503425d139c31d810f4bcf940b03357ed933a
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a>Uwierzytelnianie systemu Windows i serwer usługi Azure Multi-Factor Authentication
Sekcja Uwierzytelnianie systemu Windows w ramach serwera Azure Multi-Factor Authentication umożliwia włączenie i skonfigurowanie uwierzytelniania systemu Windows dla aplikacji. Przed skonfigurowaniem uwierzytelniania systemu Windows weź pod uwagę kwestie wymienione na poniższej liście:

* Aby usługi terminalowe zaczęły działać, po konfiguracji należy ponownie uruchomić usługę Azure Multi-Factor Authentication.
* Jeśli zaznaczono opcję „Wymagaj dopasowania użytkownika usługi Azure Multi-Factor Authentication”, a nazwy użytkownika nie ma na liście, zalogowanie się na komputerze po ponownym rozruchu nie będzie możliwe.
* To, czy adresy IP są zaufane, zależy od tego, czy aplikacja może uwierzytelnić adres IP klienta. Obecnie są obsługiwane wyłącznie usługi terminalowe.  

> [!NOTE]
> Ta funkcja nie jest obsługiwana w kontekście zabezpieczania sesji usług terminalowych w systemie Windows Server 2012 R2.

## <a name="to-secure-an-application-with-windows-authentication-use-the-following-procedure"></a>Do zabezpieczenia aplikacji z użyciem uwierzytelniania systemu Windows należy zastosować następującą procedurę.
1. Kliknij ikonę uwierzytelniania systemu Windows na serwerze usługi Azure Multi-Factor Authentication.
   ![Uwierzytelnianie systemu Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)
2. Zaznacz pole wyboru **Włącz uwierzytelnianie systemu Windows**. Domyślnie to pole nie jest zaznaczone.
3. Na karcie Aplikacje administrator może skonfigurować co najmniej jedną aplikację na potrzeby uwierzytelniania systemu Windows.
4. Wybierz serwer lub aplikację — określ, czy serwer lub aplikacja są włączone. Kliknij przycisk **OK**.
5. Kliknij pozycję **Dodaj...**
6. Na karcie Zaufane adresy IP można pominąć sesje uwierzytelniania usługi Azure Multi-Factor Authentication dla sesji systemu Windows z określonych adresów IP. Na przykład: jeśli pracownicy korzystają z aplikacji zarówno w biurze, jak i w domu, można wybrać taką konfigurację, aby nie musieli oni odbierać połączeń z usługi Azure Multi-Factor Authentication, przebywając w biurze. W tym celu należy określić podsieć biura jako wpis z zaufanymi adresami IP.
7. Kliknij pozycję **Dodaj...**
8. Wybierz opcję **Pojedynczy adres IP**, jeśli chcesz pominąć pojedynczy adres IP.
9. Wybierz opcję **Zakres adresów IP**, aby pominąć cały zakres adresów IP. Na przykład: 10.63.193.1–10.63.193.100.
10. Wybierz opcję **Podsieć**, aby określić zakres adresów IP, korzystając z notacji podsieci. Wprowadź początkowy adres IP podsieci i wybierz odpowiednią maskę sieci z listy rozwijanej.
11. Kliknij przycisk **OK**.

## <a name="next-steps"></a>Następne kroki

- [Konfigurowanie urządzeń VPN innych firm dla serwera Azure MFA](multi-factor-authentication-advanced-vpn-configurations.md)

- [Augment your existing authentication infrastructure with the NPS extension for Azure MFA](multi-factor-authentication-nps-extension.md) (Rozszerzanie istniejącej infrastruktury uwierzytelniania za pomocą rozszerzenia serwera NPS dla usługi Azure MFA)
