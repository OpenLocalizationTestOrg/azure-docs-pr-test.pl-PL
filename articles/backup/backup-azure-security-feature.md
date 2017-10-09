---
title: "aaaSecurity toohelp funkcje ochrony kopii zapasowych hybrydowych, korzystających z usługi Kopia zapasowa Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak funkcje bezpieczeństwa toouse w usłudze Kopia zapasowa Azure toomake kopiach zapasowych bardziej bezpieczne"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 47bc8423-0a08-4191-826d-3f52de0b4cb8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: pajosh
ms.openlocfilehash: 17a0f5e877f84af53c15062ec4a8df480383125e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-features-toohelp-protect-hybrid-backups-that-use-azure-backup"></a>Toohelp funkcje zabezpieczeń Chroń hybrydowego kopie zapasowe, korzystających z usługi Kopia zapasowa Azure
Coraz więcej problemów dotyczących problemów z zabezpieczeniami, takich jak złośliwego oprogramowania, ransomware i nieautoryzowanego dostępu. Te problemy zabezpieczeń może być kosztowne zarówno oszczędność pieniędzy i danych. tooguard przed takimi atakami, teraz kopia zapasowa Azure zapewnia bezpieczeństwo toohelp funkcje ochrony kopii zapasowych hybrydowego. W tym artykule opisano, jak tooenable i użyj funkcji, za pomocą agenta usług odzyskiwania Azure i serwer kopii zapasowej Azure. Te funkcje obejmują:

- **Zapobieganie**. Zawsze, gdy jest wykonywana krytycznej operacji, takich jak zmiana hasła dodawany jest dodatkową warstwę uwierzytelniania. Tej weryfikacji jest tooensure, że takie operacje mogą być wykonywane tylko przez użytkowników, którzy mają prawidłowe poświadczenia platformy Azure.
- **Alerty**. Przesyłane powiadomienia e-mail administratora subskrypcji toohello zawsze, gdy krytycznej operacji, takich jak usuwanie danych kopii zapasowej jest wykonywane. Ten adres e-mail gwarantuje, że użytkownik hello jest powiadamiany o szybko o takich działań.
- **Odzyskiwanie**. Usunięte dane kopii zapasowej jest przechowywany dla kolejnych 14 dni od daty hello hello usunięcia. Dzięki temu odzyskanie danych hello w danym okresie, więc nie ma bez utraty danych, nawet jeśli się stanie w przypadku ataków. Ponadto większa liczba punktów odzyskiwania minimalne są obsługiwane tooguard przed uszkodzone dane.

> [!NOTE]
> Funkcje zabezpieczeń nie można włączyć, korzystając z infrastruktury jako usługi (IaaS) kopii zapasowej maszyny Wirtualnej. Te funkcje nie są jeszcze dostępne dla kopii zapasowych maszyn wirtualnych IaaS, dlatego włączenie ich nie będzie miało żadnych skutków. Funkcje zabezpieczeń powinny być włączone, tylko wtedy, gdy używane są: <br/>
>  * **Agent usługi Kopia zapasowa Azure**. Wersja agenta minimalna 2.0.9052. Po włączeniu tych funkcji, należy uaktualnić toothis agenta wersji tooperform ważne operacje. <br/>
>  * **Serwer kopii zapasowej systemu Azure**. Minimalna kopia zapasowa Azure agenta w wersji 1 aktualizacji 2.0.9052 serwer kopii zapasowej Azure. <br/>
>  * **Program System Center Data Protection Manager**. Minimalna Azure Backup agent wersja 2.0.9052 z programu Data Protection Manager 2012 R2 UR12 lub UR2 2016 programu Data Protection Manager. <br/> 


> [!NOTE]
> Te funkcje są dostępne tylko dla magazynu usług odzyskiwania. Witaj wszystkie nowo utworzone magazyny usług odzyskiwania te funkcje są włączone domyślnie. Dla istniejących Magazyny usług odzyskiwania użytkowników, należy włączyć te funkcje przy użyciu kroków hello wspomnianego hello następujących sekcji. Po hello, które funkcje są włączone mają one zastosowanie komputery agenta usług odzyskiwania hello tooall wystąpienia serwera usługi Kopia zapasowa Azure i zarejestrowanych w magazynie hello serwerów programu Data Protection Manager. Włączenie tego ustawienia to działanie jednorazowe i tych funkcji nie można wyłączyć po ich włączeniem.
>

## <a name="enable-security-features"></a>Funkcje zabezpieczeń
W przypadku tworzenia magazynu usług odzyskiwania, można użyć wszystkich funkcji zabezpieczeń hello. Jeśli pracujesz z istniejącego magazynu, włączyć funkcje zabezpieczeń, wykonaj następujące czynności:

1. Zaloguj się toohello portalu Azure przy użyciu poświadczeń platformy Azure.
2. Wybierz **Przeglądaj**i wpisz **usług odzyskiwania**.

    ![Opcja przeglądania portalu zrzut ekranu Azure](./media/backup-azure-security-feature/browse-to-rs-vaults.png) <br/>

    zostanie wyświetlona lista Hello Magazyny usług odzyskiwania. Z tej listy wybierz magazyn. Otwiera Hello wybranego magazynu z pulpitu nawigacyjnego.
3. Z listy hello elementów, który pojawia się w magazynie hello, w obszarze **ustawienia**, kliknij przycisk **właściwości**.

    ![Opcje magazynu zrzut ekranu usług odzyskiwania](./media/backup-azure-security-feature/vault-list-properties.png)
4. W obszarze **ustawienia zabezpieczeń**, kliknij przycisk **aktualizacji**.

    ![Zrzut ekranu usług odzyskiwania Magazyn właściwości](./media/backup-azure-security-feature/security-settings-update.png)

    Witaj aktualizacji łącze powoduje otwarcie hello **ustawienia zabezpieczeń** bloku, który zawiera podsumowanie funkcji hello i można je włączyć.
5. Z listy rozwijanej hello **zostały skonfigurowane uwierzytelnianie wieloskładnikowe Azure?**, wybierz tooconfirm wartość, jeśli włączono [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md). Jeśli jest włączona, zostanie wyświetlona prośba tooauthenticate z innego urządzenia (na przykład telefon komórkowy) podczas podpisywania w toohello portalu Azure.

   Podczas wykonywania krytycznej operacji w usłudze Kopia zapasowa, masz tooenter zabezpieczający numer PIN, dostępnych na powitania portalu Azure. Włączanie usługi Azure Multi-Factor Authentication dodaje warstwy zabezpieczeń. Tylko do autoryzowanych użytkowników z prawidłowymi poświadczeniami Azure i uwierzytelnieniu z drugiego urządzenia mogą uzyskiwać dostęp do hello portalu Azure.
6. Wybierz ustawienia zabezpieczeń toosave **włączyć** i kliknij przycisk **zapisać**. Możesz wybrać **włączyć** tylko po wybraniu wartości z hello **zostały skonfigurowane uwierzytelnianie wieloskładnikowe Azure?** listy hello poprzedniego kroku.

    ![Zrzut ekranu przedstawiający ustawienia zabezpieczeń](./media/backup-azure-security-feature/enable-security-settings-dpm-update.png)

## <a name="recover-deleted-backup-data"></a>Odzyskiwanie usuniętych danych kopii zapasowej
Kopia zapasowa przechowuje dodatkowe 14 dni usuniętych danych kopii zapasowej i nie powoduje jego usunięcia natychmiast, jeśli hello **kopii zapasowej Zatrzymaj z usuwania danych kopii zapasowej** operacja została wykonana. toorestore te dane w hello 14-dniowym okresie, wykonaj hello następujące kroki w zależności od tego, czego używasz:

Aby uzyskać **agenta usług odzyskiwania Azure** użytkowników:

1. Jeśli komputer hello, których kopie zapasowe były wykonywane jest nadal dostępne, użyj [odzyskać dane toohello tej samej maszynie](backup-azure-restore-windows-server.md#use-instant-restore-to-recover-data-to-the-same-machine) w usług odzyskiwania Azure, toorecover z wszystkich hello stare punkty odzyskiwania.
2. Jeśli ten komputer jest niedostępny, użyj [odzyskiwanie tooan alternatywny maszyna](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) toouse innego tooget komputera usług odzyskiwania Azure tych danych.

Aby uzyskać **serwer kopii zapasowej Azure** użytkowników:

1. Jeśli serwer hello, których kopie zapasowe były wykonywane jest nadal dostępny, ponownie włączyć ochronę źródeł danych hello usunięte i użyj hello **odzyskać dane** funkcji toorecover z wszystkich hello stare punkty odzyskiwania.
2. Jeśli ten serwer jest niedostępny, użyj [odzyskać dane z innego serwera kopii zapasowej Azure](backup-azure-alternate-dpm-server.md) toouse innego serwera kopii zapasowej Azure wystąpienia tooget tych danych.

Aby uzyskać **programu Data Protection Manager** użytkowników:

1. Jeśli serwer hello, których kopie zapasowe były wykonywane jest nadal dostępny, ponownie włączyć ochronę źródeł danych hello usunięte i użyj hello **odzyskać dane** funkcji toorecover z wszystkich hello stare punkty odzyskiwania.
2. Jeśli ten serwer jest niedostępny, użyj [Dodaj zewnętrzny program DPM](backup-azure-alternate-dpm-server.md) toouse innego tooget serwera programu Data Protection Manager tych danych.

## <a name="prevent-attacks"></a>Zapobieganie atakom
Dodano kontroli toomake się, że tylko prawidłowych użytkowników można wykonywać różne operacje. Obejmują one dodanie dodatkowej warstwy uwierzytelniania i utrzymywanie zakres przechowywania minimalnej na potrzeby odzyskiwania.

### <a name="authentication-tooperform-critical-operations"></a>Ważne operacje tooperform uwierzytelniania
W ramach dodanie dodatkowej warstwy uwierzytelniania na ważne operacje, jest monitem tooenter zabezpieczający numer PIN podczas wykonywania **Zatrzymaj ochronę danych Delete** i **Zmień hasło** operacji .

tooreceive ten numer PIN:

1. Zaloguj się toohello portalu Azure.
2. Przeglądaj zbyt**magazyn usług odzyskiwania i** > **ustawienia** > **właściwości**.
3. W obszarze **kod PIN zabezpieczeń**, kliknij przycisk **Generuj**. Spowoduje to otwarcie bloku, który zawiera hello toobe kod PIN wprowadzony w interfejsie użytkownika agenta usług odzyskiwania Azure hello.
    Ten numer PIN jest prawidłowy tylko pięć minut, a następnie pobiera ona generowana automatycznie po upływie tego czasu.

### <a name="maintain-a-minimum-retention-range"></a>Obsługa zakresu przechowywania minimalnej
tooensure, że zawsze są prawidłową liczbę odzyskiwania punktów dostępnych, powitania po kontroli zostały dodane:

- Do przechowywania codziennie, co najmniej **siedmiu** ma się odbywać dni przechowywania.
- Do przechowywania co tydzień, co najmniej **cztery** ma się odbywać tygodni przechowywania.
- Miesięczne okresu przechowywania, co najmniej **trzy** ma się odbywać okresem przechowywania.
- Do przechowywania roczne, co najmniej **jeden** ma się odbywać roku przechowywania.

## <a name="notifications-for-critical-operations"></a>Powiadomienia dotyczące ważne operacje
Zwykle po wykonaniu operacji krytyczne Witaj, Administratorze subskrypcji jest wysyłana wiadomość e-mail z powiadomieniem o szczegółowe informacje dotyczące operacji hello. Można skonfigurować dodatkowe e-mail adresatów powiadomień za pomocą hello portalu Azure.

funkcje zabezpieczeń Hello wymienione w niniejszym artykule zapewniają mechanizmy obrony przed atakami ukierunkowanymi. Co więcej, jeśli wystąpi atak, te funkcje umożliwiają hello toorecover możliwości danych.

## <a name="troubleshooting-errors"></a>Rozwiązywanie problemów z błędami
| Operacja | Szczegóły błędu | Rozwiązanie |
| --- | --- | --- |
| Zmiana zasad |Nie można zmodyfikować Hello zasad tworzenia kopii zapasowej. Błąd: hello bieżąca operacja nie powiodła z powodu tooan wewnętrznego błędu usługi [0x29834]. Ponów operację powitania po pewnym czasie. Jeśli hello problem będzie się powtarzać, skontaktuj się z pomocą techniczną firmy Microsoft. |**Przyczyna:**<br/>Ten błąd jest dostarczany podczas ustawienia zabezpieczeń zostały włączone, spróbuj tooreduce zakres przechowywania, poniżej wartości minimalnej hello wymienione powyżej i znajdują się na nieobsługiwaną wersję (obsługiwane wersje są określone w pierwszym należy wziąć pod uwagę w tym artykule). <br/>**Zalecana akcja:**<br/> W takim przypadku należy ustawić okresu przechowywania powyżej hello co najmniej podanego okresu (siedem dni codziennie, czterech tygodni, przez co tydzień, trzy tygodnie, co miesiąc lub rok dla corocznej) tooproceed z zasady dotyczące aktualizacji. Opcjonalnie preferowane rozwiązanie byłoby tooupdate agenta kopii zapasowej, aktualizacji zabezpieczeń hello tooleverage serwera kopii zapasowej Azure i/lub pakietem zbiorczym aktualizacji programu DPM. |
| Zmień hasło |Zabezpieczenia wprowadzony numer PIN jest niepoprawny. (IDENTYFIKATOR: 100130) Podaj poprawne toocomplete kod PIN zabezpieczeń hello tej operacji. |**Przyczyna:**<br/> Ten błąd jest dostarczany podczas wprowadzania numeru PIN zabezpieczeń nieważny lub wygasły podczas wykonywania krytycznej operacji (jak zmienić hasło). <br/>**Zalecana akcja:**<br/> Operacja hello toocomplete, należy wprowadzić prawidłowy kod PIN zabezpieczeń. tooget hello numeru PIN, zaloguj się w portalu tooAzure i przejdź magazynu usług tooRecovery > Ustawienia > Właściwości > Generowanie kodu PIN zabezpieczeń. Użyj tego hasła toochange numeru PIN. |
| Zmień hasło |Operacja nie powiodła się. IDENTYFIKATOR: 120002 |**Przyczyna:**<br/>Ten błąd jest dostarczany, gdy ustawienia zabezpieczeń zostały włączone, spróbuj toochange hasło i znajdują się na nieobsługiwaną wersję (prawidłowe wersje określone w pierwszym należy wziąć pod uwagę w tym artykule).<br/>**Zalecana akcja:**<br/> toochange hasło, należy najpierw zaktualizować wersja agenta kopii zapasowej toominimum 2.0.9052 minimalne, kopia zapasowa Azure serwera toominimum update 1 i/lub toominimum DPM UR12 programu DPM 2012 R2 lub DPM UR2 2016 (poniżej łącza pobierania), wprowadź prawidłowy kod PIN zabezpieczeń. tooget hello numeru PIN, zaloguj się w portalu tooAzure i przejdź magazynu usług tooRecovery > Ustawienia > Właściwości > Generowanie kodu PIN zabezpieczeń. Użyj tego hasła toochange numeru PIN. |

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie do magazynu usług odzyskiwania Azure](backup-azure-vms-first-look-arm.md) tooenable te funkcje.
* [Pobierz najnowszą wersję hello agenta usług odzyskiwania Azure](http://aka.ms/azurebackup_agent) toohelp chronić komputery z systemem Windows i ochronę danych przed atakami.
* [Pobieranie hello najnowsze serwera kopii zapasowej Azure](https://aka.ms/latest_azurebackupserver) toohelp ochronę obciążeń i ochronę danych przed atakami.
* [Pobierz UR12 dla systemu System Center 2012 R2 Data Protection Manager](https://support.microsoft.com/help/3209592/update-rollup-12-for-system-center-2012-r2-data-protection-manager) lub [Pobierz UR2 dla programu System Center 2016 Data Protection Manager](https://support.microsoft.com/help/3209593/update-rollup-2-for-system-center-2016-data-protection-manager) toohelp ochronę obciążeń i ochronę danych przed atakami.
