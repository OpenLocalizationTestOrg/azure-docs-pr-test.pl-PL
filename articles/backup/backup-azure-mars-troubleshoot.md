---
title: "Rozwiązywanie problemów z agenta kopii zapasowej systemu Azure | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z instalację i rejestrację agenta usługi Kopia zapasowa Azure"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shreeshd
editor: 
ms.assetid: 778c6ccf-3e57-4103-a022-367cc60c411a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/4/2017
ms.author: saurse;markgal;
ms.openlocfilehash: 52a32d61dd69110ace560fd1e52389140f322678
ms.sourcegitcommit: c87e036fe898318487ea8df31b13b328985ce0e1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/19/2017
---
# <a name="troubleshoot-azure-backup-agent-configuration-and-registration-issues"></a>Rozwiązywanie problemów dotyczących konfiguracji agenta usługi Kopia zapasowa Azure i problemy dotyczące rejestracji
## <a name="recommended-steps"></a>Zalecane czynności
Zapoznaj się z działania opisane w poniższych tabelach, aby naprawić błędy, które można napotkać podczas konfiguracji i rejestracji agenta usługi Kopia zapasowa Azure.

## <a name="invalid-vault-credentials-provided-the-file-is-either-corrupted-or-does-not-have-the-latest-credentials-associated-with-recovery-service"></a>Udostępniono nieprawidłowe poświadczenia magazynu. Plik jest uszkodzony lub jest nie ma najnowszych poświadczeń skojarzonych z usługą odzyskiwania.
| Szczegóły błędu | Możliwe przyczyny | Zalecane akcje |
| ---     | ---     | ---    |
| **Błąd** </br> *Udostępniono nieprawidłowe poświadczenia magazynu. Plik jest uszkodzony lub jest nie ma najnowszych poświadczeń skojarzonych z usługą odzyskiwania. (IDENTYFIKATOR: 34513)* | <ul><li> Poświadczenia magazynu są nieprawidłowe (to znaczy one zostały pobrane ponad 48 godzin przed upływem terminu rejestracji).<li>Azure Backup Agent nie jest w stanie pobrać plik tymczasowy w folderze Temp systemu Windows. <li>Poświadczenia magazynu znajdują się w lokalizacji sieciowej. <li>Protokołu TLS 1.0 jest wyłączona.<li> Skonfigurowany serwer proxy blokuje połączenia. <br> |  <ul><li>Pobranie nowych poświadczeń magazynu.<li>Przejdź do **Opcje internetowe** > **zabezpieczeń** > **Internet**. Następnie wybierz pozycję **Poziom niestandardowy**i przewiń plik, Pobierz sekcji. Następnie wybierz **włączyć**.<li>Może być również konieczne Dodaj witrynę do [Zaufane witryny](https://docs.microsoft.com/azure/backup/backup-try-azure-backup-in-10-mins#network-and-connectivity-requirements).<li>Zmień ustawienia, aby użyć serwera proxy. Następnie podaj serwer proxy szczegóły serwera. <li> Zgodny datę i godzinę z komputera.<li>Przejdź do C:/Windows/Temp i sprawdź, czy istnieją ponad 60 000 lub 65 000 plików z rozszerzeniem tmp. Jeśli istnieje, usuń te pliki.<li>Można to sprawdzić, uruchamiając SDP pakietu na serwerze. Jeśli zostanie wyświetlony komunikat o błędzie informujący, pobierania plików nie są dozwolone, jest bardzo prawdopodobne, że ma dużą liczbę plików w katalogu Temp-C:/Windows.<li>Upewnij się, że zainstalowano .NET framework 4.6.2. <li>Jeśli protokół TLS 1.0 zostało wyłączone z powodu zgodności PCI, odwołują się do tego [Rozwiązywanie problemów z strony](https://support.microsoft.com/help/4022913). <li>Jeśli masz oprogramowanie antywirusowe zainstalowane na serwerze, należy wyłączyć następujące pliki ze skanowania antywirusowego: <ul><li>CBengine.exe<li>CSC.exe, który jest powiązany z .NET Framework. Brak CSC.exe dla każdej wersji .NET, który jest zainstalowany na serwerze. Wyklucz pliki CSC.exe, które są powiązane z wszystkich wersji platformy .NET na tym serwerze. <li>Pliki tymczasowe lokalizacji pamięci podręcznej lub folderu. <br>*Domyślna lokalizacja dla pliki tymczasowe folder lub ścieżka lokalizacji pamięci podręcznej to C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch*.

## <a name="the-microsoft-azure-recovery-service-agent-was-unable-to-connect-to-microsoft-azure-backup"></a>Agent usług odzyskiwania Microsoft Azure nie może nawiązać połączenia z usługą kopia zapasowa Microsoft Azure

| Szczegóły błędu | Możliwe przyczyny | Zalecane akcje |
| ---     | ---     | ---    |
| **Błąd** </br><ol><li>*Agent usług odzyskiwania Microsoft Azure nie może nawiązać połączenia z usługą kopia zapasowa Microsoft Azure. (IDENTYFIKATOR: 100050) Sprawdź ustawienia sieciowe i upewnij się, że jesteś w stanie nawiązać połączenia z Internetem*<li>*Wymagane jest uwierzytelnianie serwera proxy (407)* |Serwer proxy blokuje połączenia. |  <ul><li>Przejdź do **Opcje internetowe** > **zabezpieczeń** > **Internet**. Następnie wybierz **Poziom niestandardowy** i przewiń plik, Pobierz sekcji. Wybierz pozycję **Włącz**.<li>Może być również konieczne Dodaj witrynę do [Zaufane witryny](https://docs.microsoft.com/azure/backup/backup-try-azure-backup-in-10-mins#network-and-connectivity-requirements).<li>Zmień ustawienia, aby użyć serwera proxy. Następnie podaj serwer proxy szczegóły serwera. <li>Jeśli masz oprogramowanie antywirusowe zainstalowane na serwerze, należy wyłączyć następujące pliki ze skanowania antywirusowego. <ul><li>CBEngine.exe (zamiast dpmra.exe).<li>CSC.exe (powiązanego z .NET Framework). Brak CSC.exe dla każdej wersji .NET, który jest zainstalowany na serwerze. Wyklucz pliki CSC.exe, które są powiązane z wszystkich wersji platformy .NET na tym serwerze. <li>Pliki tymczasowe lokalizacji pamięci podręcznej lub folderu. <br>*Domyślna lokalizacja dla pliki tymczasowe folder lub ścieżka lokalizacji pamięci podręcznej to C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch*.

## <a name="failed-to-set-the-encryption-key-for-secure-backups"></a>Nie można ustawić klucza szyfrowania bezpiecznego tworzenia kopii zapasowych

| Szczegóły błędu | Możliwe przyczyny | Zalecane akcje |
| ---     | ---     | ---    |      
| **Błąd** </br>*Nie można ustawić klucza szyfrowania bezpiecznego tworzenia kopii zapasowych. Bieżąca operacja nie powiodła się z powodu wewnętrznego błędu "Nieprawidłowa wejściowych błędu usługi". Spróbuj ponownie wykonać operację po pewnym czasie. Jeśli problem będzie się powtarzać, skontaktuj się z pomocą techniczną firmy Microsoft*. |Serwer jest już zarejestrowany w innym magazynie.| Wyrejestruj serwer z magazynu i Zarejestruj ponownie.

## <a name="the-activation-did-not-complete-successfully-the-current-operation-failed-due-to-an-internal-service-error-0x1fc07"></a>Aktywacja nie została pomyślnie ukończona. Bieżąca operacja nie powiodła się z powodu wewnętrznego błędu usługi [0x1FC07]

| Szczegóły błędu | Możliwe przyczyny | Zalecane akcje |
| ---     | ---     | ---    |          
| **Błąd** </br><ol><li>*Aktywacja nie została pomyślnie ukończona. Bieżąca operacja nie powiodła się z powodu wewnętrznego błędu usługi [0x1FC07]. Spróbuj ponownie wykonać operację po pewnym czasie. Jeśli problem będzie się powtarzać, skontaktuj się z pomocą techniczną firmy Microsoft* <li>*Błąd 34506. Hasło szyfrowania zapisane na tym komputerze nie jest poprawnie skonfigurowany*. | <li> Pliki tymczasowe folder znajduje się na woluminie, który ma za mało miejsca. <li> Pliki tymczasowe folder został przeniesiony niepoprawnie do innej lokalizacji. <li> Brak pliku OnlineBackup.KEK. | <li>Przenieś pliki tymczasowe folderu lub lokalizacji pamięci podręcznej do woluminu z wolnego miejsca odpowiednikiem 5 – 10% całkowitego rozmiaru danych kopii zapasowej. Można poprawnie przenieść lokalizację pamięci podręcznej, skorzystaj z procedury opisanej w [pytania dotyczące agenta kopii zapasowej Azure](https://docs.microsoft.com/azure/backup/backup-azure-file-folder-backup-faq#backup).<li> Upewnij się, że plik OnlineBackup.KEK jest obecny. <br>*Domyślna lokalizacja dla pliki tymczasowe folder lub ścieżka lokalizacji pamięci podręcznej to C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch*.

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Kontakt z pomocą techniczną
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) uzyskać szybkie rozwiązanie problemu.

## <a name="next-steps"></a>Kolejne kroki
* Dowiedz się więcej [sposób wykonywania kopii zapasowej systemu Windows Server przy użyciu agenta kopii zapasowej Azure](tutorial-backup-windows-server-to-azure.md).
* Jeśli chcesz przywrócić kopię zapasową, w tym artykule znajdziesz informacje dotyczące [przywracania plików na maszynę z systemem Windows](backup-azure-restore-windows-server.md).
