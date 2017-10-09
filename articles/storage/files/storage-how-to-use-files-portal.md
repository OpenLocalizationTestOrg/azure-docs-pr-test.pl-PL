---
title: "toomanage aaaHow magazyn plików Azure z hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się toouse hello Azure toomanage portalu usługi Magazyn plików Azure."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 6ad2fbbf9ee2f86748b1b175d0f63274144dc5eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a>Jak magazyn plików Azure toouse z hello portalu Azure
Witaj [portalu Azure](https://portal.azure.com) udostępnia interfejs użytkownika do zarządzania usługi Magazyn plików Azure. Można wykonywać hello następujące akcje w przeglądarce sieci web:

* Tworzenie udziału plików
* Przekazywanie i pobieranie plików tooand z udziału plików.
* Monitorowanie hello rzeczywistego użycia każdego udziału plików.
* Dostosuj hello limitu przydziału rozmiaru udziału plików.
* Skopiuj hello instalacji poleceń toouse toomount udostępnić plik z klienta systemu Windows lub Linux.

## <a name="create-file-share"></a>Tworzenie udziału plików
1. Zaloguj się toohello portalu Azure.
2. W menu nawigacji powitania kliknij **kont magazynu** lub **kont magazynu (klasyczne)**.
    
    ![Zrzut ekranu pokazujący sposób udział plików toocreate w portalu hello](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. Wybierz konto magazynu.

    ![Zrzut ekranu pokazujący sposób udział plików toocreate w portalu hello](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. Wybierz usługę „Pliki”.

    ![Zrzut ekranu pokazujący sposób udział plików toocreate w portalu hello](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. Kliknij pozycję "Udziały plików" i wykonaj toocreate łącze hello udostępnianie pierwszego pliku.

    ![Zrzut ekranu pokazujący sposób udział plików toocreate w portalu hello](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. Wypełnij nazwę udziału plików hello i rozmiaru hello toocreate udziału (w górę too5120 GB) pliku hello pierwszego udziału plików. Po utworzeniu udziału plików hello, możesz go zainstalować z dowolnego systemu plików, który obsługuje protokół SMB 2.1 lub SMB 3.0. Można kliknąć na **przydziału** na rozmiar udziału plików hello hello toochange pliku hello się too5120 GB. Zobacz zbyt[Kalkulator cen platformy Azure](https://azure.microsoft.com/pricing/calculator/) tooestimate hello magazynu koszt używania usługi Magazyn plików Azure.

    ![Zrzut ekranu pokazujący sposób udział plików toocreate w portalu hello](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a>Przekazywanie i pobieranie plików
1. Wybierz utworzony udział plików.

    ![Zrzut ekranu pokazujący sposób tooupload i pobieranie plików z hello portalu](./media/storage-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. Kliknij przycisk **przekazać** otworzyć Interfejs użytkownika hello przekazywania plików.

    ![Zrzut ekranu pokazujący sposób tooupload plików z portalu hello](./media/storage-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a>Połącz toofile udziału
-  Kliknij przycisk **Connect** uzyskać hello wiersza polecenia dla udziału plików hello instalowanie z systemu Windows i Linux. W przypadku użytkowników systemu Linux, można także skorzystać zbyt[jak toouse magazyn plików Azure z systemem Linux](../storage-how-to-use-files-linux.md) instrukcje instalowania dla innych dystrybucje systemu Linux.

    ![Zrzut ekranu pokazujący sposób toomount hello udziału plików](./media/storage-how-to-use-files-portal/use-files-portal-connect.png)
-  Możesz skopiować hello polecenia służący do instalowania plików udziału w systemie Windows lub Linux i uruchom go, musisz maszyna wirtualna platformy Azure lub lokalnie.

    ![Zrzut ekranu pokazujący hello polecenia instalacji systemu Windows i Linux](./media/storage-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

**Porada:**  
klucz dostępu do konta magazynu hello toofind potrzeby instalacji, kliknij **kluczy dostępu do wyświetlania dla tego konta magazynu** u dołu hello hello połączenia strony.

## <a name="see-also"></a>Zobacz też
Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.

* [Często zadawane pytania](../storage-files-faq.md)
* [Rozwiązywanie problemów w systemie Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Rozwiązywanie problemów w systemie Linux](storage-troubleshoot-linux-file-connection-problems.md)    