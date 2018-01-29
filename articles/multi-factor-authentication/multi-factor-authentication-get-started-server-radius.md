---
title: "Uwierzytelnianie usługi RADIUS i serwer usługi Azure MFA | Microsoft Docs"
description: "Ta strona dotyczy usługi Azure Multi-Factor Authentication i zawiera wskazówki pomocne we wdrażaniu uwierzytelniania usługi RADIUS i serwera usługi Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.assetid: f4ba0fb2-2be9-477e-9bea-04c7340c8bce
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/25/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 07b242699e016550c82f491c1678c6dbc9f7234d
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="integrate-radius-authentication-with-azure-multi-factor-authentication-server"></a>Integrowanie uwierzytelniania usługi RADIUS z serwerem usługi Azure Multi-Factor Authentication

RADIUS jest standardowym protokołem, który umożliwia akceptowanie i przetwarzanie żądań uwierzytelniania. Serwer usługi Azure Multi-Factor Authentication może działać jako serwer RADIUS. Wstaw go między klientem RADIUS (urządzeniem sieci VPN) i celem uwierzytelniania, aby dodać weryfikację dwuetapową. Celem uwierzytelniania może być usługa Active Directory, katalog LDAP lub inny serwer RADIUS. Aby możliwe było działanie usługi Azure Multi-Factor Authentication (MFA), serwer usługi Azure MFA musi zostać skonfigurowany pod kątem komunikacji zarówno z serwerami klientów, jak i obiektem docelowym uwierzytelniania. Serwer usługi Azure MFA odbiera żądania od klienta usługi RADIUS, przeprowadza walidację poświadczeń względem obiektu docelowego uwierzytelniania, dodaje usługę Azure Multi-Factor Authentication i wysyła odpowiedź do klienta usługi RADIUS. Żądanie uwierzytelniania powiedzie się tylko w przypadku pomyślnego przebiegu zarówno uwierzytelniania podstawowego, jak i uwierzytelniania usługi Azure Multi-Factor Authentication.

> [!NOTE]
> Gdy serwer usługi MFA działa jako serwer usługi RADIUS, obsługuje tylko protokoły usługi RADIUS: PAP (protokół uwierzytelniania haseł) i MSCHAPv2 (protokół uwierzytelniania typu Challenge Handshake firmy Microsoft).  Inne protokoły, np. protokół uwierzytelniania rozszerzonego (EAP, Extensible Authentication Protocol), mogą być używane, jeśli serwer usługi MFA działa jako serwer proxy usługi RADIUS połączony z innym serwerem usługi RADIUS, który obsługuje taki protokół.
>
> W tej konfiguracji jednokierunkowe tokeny SMS i OATH nie działają, ponieważ serwer usługi MFA nie może zainicjować pomyślnej odpowiedzi na żądanie usługi RADIUS przy użyciu alternatywnych protokołów.

![Uwierzytelnianie usługi Radius](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="add-a-radius-client"></a>Dodawanie klienta usługi RADIUS
Aby skonfigurować uwierzytelnianie usługi RADIUS, zainstaluj serwer usługi Azure Multi-Factor Authentication na serwerze z systemem Windows. Jeśli korzystasz ze środowiska usługi Active Directory, przyłącz serwer do domeny znajdującej się w sieci. Poniższa procedura umożliwia skonfigurowanie serwera usługi Azure Multi-Factor Authentication:

1. Na serwerze usługi Azure Multi-Factor Authentication kliknij ikonę Uwierzytelnianie usługi RADIUS w menu po lewej stronie.
2. Zaznacz pole wyboru **Włącz uwierzytelnianie usługi RADIUS**.
3. Na karcie Klienci zmień porty uwierzytelniania i ewidencjonowania aktywności, jeśli usługa Azure MFA RADIUS musi nasłuchiwać żądań usługi RADIUS na niestandardowych portach.
4. Kliknij pozycję **Dodaj**.
5. Wprowadź adres IP urządzenia/serwera, które będą uwierzytelniane na serwerze usługi Azure Multi-Factor Authentication, nazwę aplikacji (opcjonalnie) i wspólny klucz tajny.

  Nazwa aplikacji jest widoczna w raportach i może być wyświetlana w uwierzytelniających wiadomościach SMS lub wiadomościach uwierzytelniających aplikacji mobilnej.

  Wspólny klucz tajny musi być taki sam dla serwera usługi Azure Multi-Factor Authentication i urządzenia/serwera.

6. Zaznacz pole **Wymagaj dopasowania użytkownika usługi Multi-Factor Authentication**, jeśli wszyscy użytkownicy zostali zaimportowani na serwer i będą podlegać uwierzytelnianiu wieloskładnikowemu. Jeśli znaczna liczba użytkowników nie została jeszcze zaimportowana na serwer lub jest wykluczona z weryfikacji dwuetapowej, należy pozostawić to pole puste.
7. Zaznacz pole **Włącz rezerwowy token OATH**, jeśli chcesz używać kodów dostępu OATH z aplikacji mobilnych służących do weryfikacji jako metody rezerwowej.
8. Kliknij przycisk **OK**.

Powtarzaj kroki od 4 do 8, aby dodać tylu klientów usługi RADIUS, ilu potrzebujesz.

## <a name="configure-your-radius-client"></a>Konfigurowanie klienta usługi RADIUS

1. Kliknij kartę **Cel**.
2. Jeśli serwer usługi Azure MFA jest zainstalowany na serwerze przyłączonym do domeny w środowisku usługi Active Directory, wybierz domenę systemu Windows.
3. Jeśli użytkownicy mają być uwierzytelniani względem katalogu LDAP, wybierz pozycję **Powiązanie z protokołem LDAP**.

  Wybierz ikonę Integracja katalogu i zmień konfigurację protokołu LDAP na karcie Ustawienia, tak aby serwer mógł utworzyć powiązanie z katalogiem. Instrukcje dotyczące konfigurowania protokołu LDAP można znaleźć w [przewodniku po konfiguracji serwera proxy LDAP](multi-factor-authentication-get-started-server-ldap.md).

4. Jeśli użytkownicy mają być uwierzytelniani względem innego serwera RADIUS, wybierz co najmniej jeden serwer RADIUS.
5. Kliknij przycisk **Dodaj**, aby skonfigurować serwer, który będzie działał jako serwer proxy dla żądań usługi RADIUS przesyłanych przez serwer usługi Azure MFA.
6. W oknie dialogowym Dodawanie serwera usługi RADIUS wprowadź adres IP serwera RADIUS i wspólny klucz tajny.

  Wspólny klucz tajny musi być taki sam dla serwera usługi Azure Multi-Factor Authentication i serwera RADIUS. Zmień port uwierzytelniania i port ewidencjonowania aktywności, jeśli serwer RADIUS używa innych portów.

7. Kliknij przycisk **OK**.
8. Dodaj serwer usługi Azure MFA jako klienta RADIUS na drugim serwerze RADIUS, aby umożliwić mu przetwarzanie żądań dostępu wysyłanych z serwera usługi Azure MFA. Użyj tego samego wspólnego klucza tajnego, który został skonfigurowany na serwerze usługi Azure Multi-Factor Authentication.

Powtórz te kroki, aby dodać więcej serwerów RADIUS. Skonfiguruj kolejność ich wywoływania przez serwer usługi Azure MFA za pomocą przycisków **Przenieś w górę** i **Przenieś w dół**.

Pobieranie serwera usługi Azure Multi-Factor Authentication zakończyło się pomyślnie. Przy użyciu skonfigurowanych portów serwer nasłuchuje żądań dostępu usługi RADIUS pochodzących od skonfigurowanych klientów.   

## <a name="radius-client-configuration"></a>Konfiguracja klienta RADIUS
Aby skonfigurować klienta RADIUS, skorzystaj z następujących wskazówek:

* Skonfiguruj uwierzytelnianie urządzenia/serwera pod adresem IP serwera usługi Azure Multi-Factor Authentication (który działa jako serwer RADIUS) za pośrednictwem usługi RADIUS.
* Użyj tego samego wspólnego klucza tajnego, który został skonfigurowany wcześniej.
* Limit czasu usługi RADIUS ustaw na 30–60 sekund, aby zapewnić czas na przeprowadzenie walidacji poświadczeń użytkownika, przeprowadzenie weryfikacji dwuetapowej, odebranie odpowiedzi i przesłanie odpowiedzi na żądanie dostępu usługi RADIUS.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak [przeprowadzić integrację z uwierzytelnianiem RADIUS](multi-factor-authentication-nps-extension.md), jeśli korzystasz z usługi Azure Multi-Factor Authentication w chmurze. 