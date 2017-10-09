---
title: "aaaWindows uwierzytelniania i serwera usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Jest to strona uwierzytelnianie wieloskładnikowe Azure hello przydatnej Wdrażanie uwierzytelniania systemu Windows i serwera usługi Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a>Uwierzytelnianie systemu Windows i serwer usługi Azure Multi-Factor Authentication
Użyj sekcji uwierzytelnianie systemu Windows hello powitania serwera usługi Azure Multi-Factor Authentication tooenable i skonfiguruj uwierzytelnianie systemu Windows dla aplikacji. Przed skonfigurowaniem uwierzytelniania systemu Windows należy hello listy na uwadze następujące:

* Po zakończeniu instalacji uruchom ponownie hello Azure Multi-Factor Authentication dla usług terminalowych tootake efektu.
* Jeśli zaznaczono opcję "Wymagaj Azure Multi-Factor Authentication dopasowania użytkownika" i nie jest hello listy użytkowników, nie będzie możliwe toolog na powitania maszynę po ponownym rozruchu.
* Zaufanych adresów IP jest zależna od tego, czy aplikacja hello zapewniają powitania klienta IP z uwierzytelnianiem hello. Obecnie są obsługiwane wyłącznie usługi terminalowe.  

> [!NOTE]
> Ta funkcja nie jest obsługiwane toosecure usług terminalowych w systemie Windows Server 2012 R2.

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a>toosecure aplikacji przy użyciu uwierzytelniania systemu Windows hello użyj następującej procedury.
1. Kliknij ikonę uwierzytelnianie systemu Windows hello w powitania serwera usługi Azure Multi-Factor Authentication.
   ![Uwierzytelnianie systemu Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)
2. Sprawdź hello **włączyć uwierzytelnianie systemu Windows** wyboru. Domyślnie to pole nie jest zaznaczone.
3. Karta aplikacje Hello umożliwia tooconfigure administratora hello co najmniej jedna aplikacja uwierzytelniania systemu Windows.
4. Wybierz serwer lub aplikacja — Określ, czy aplikacja serwera hello jest włączona. Kliknij przycisk **OK**.
5. Kliknij pozycję **Dodaj...**
6. Karta zaufanych adresów IP Hello umożliwia tooskip sesji Azure Multi-Factor Authentication dla systemu Windows, pochodzących z określonych adresów IP. Na przykład jeśli pracownicy korzystają z aplikacji hello hello biurze i w domu, mogą zdecydujesz, że nie chcesz ich dzwonienie na telefony Azure Multi-Factor Authentication przy jednoczesnym hello pakietu office. W tym celu należy określić podsieć biura hello jako wpis zaufanych adresów IP.
7. Kliknij pozycję **Dodaj...**
8. Wybierz **pojedynczy adres IP** Jeśli chcesz tooskip pojedynczego adresu IP.
9. Wybierz **zakres adresów IP** Jeśli chcesz tooskip cały zakres adresów IP. Na przykład: 10.63.193.1–10.63.193.100.
10. Wybierz **podsieci** Jeśli chcesz toospecify zakres adresów IP przy użyciu notacji podsieci. Wprowadź początkowy IP podsieci hello i wybierz odpowiednią maskę sieciową hello z listy rozwijanej hello.
11. Kliknij przycisk **OK**.

## <a name="next-steps"></a>Następne kroki

- [Konfigurowanie urządzeń VPN innych firm dla serwera Azure MFA](multi-factor-authentication-advanced-vpn-configurations.md)

- [Rozszerzyć istniejącą infrastrukturę uwierzytelniania z powitania serwera NPS rozszerzenia dla usługi Azure MFA](multi-factor-authentication-nps-extension.md)
