---
title: "aaaTroubleshooting hello Azure narzędzie importu/eksportu | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat niektórych typowych problemów hello widoczne, używając hello narzędzie importu/eksportu Azure oraz w jaki sposób toohandle je."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 254439c15797862dded5d80028b8780ad163b2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a>Rozwiązywanie problemów z hello Azure narzędzie importu/eksportu
Hello narzędzia importu/eksportu pakietu Microsoft Azure zwraca komunikaty o błędach, gdy jest ono uruchomione na problemy. W tym temacie wymieniono niektóre typowe problemy, które użytkownicy mogą napotkać.  
  
## <a name="a-copy-session-fails-what-i-should-do"></a>Kopiuj sesja nie powiedzie się, co należy zrobić?  
 W przypadku awarii sesji kopiowania dostępne są dwie opcje:  
  
 Jeśli hello Błąd powtarzający operację, na przykład jeśli udział sieciowy hello była w trybie offline, krótki okres, a teraz jest znowu w trybie online, możesz wznowić hello kopiowania sesji. Błąd hello nie jest powtarzający operację, na przykład, jeśli określony katalog pliku nieprawidłowe źródło hello w hello parametry wiersza polecenia, należy najpierw tooabort hello kopiowania sesji. Zobacz [przygotowywanie dyski twarde dla zadania importu](../storage-import-export-tool-preparing-hard-drives-import-v1.md) uzyskać więcej informacji o wznawianie i przerywanie sesji kopiowania.  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a>I nie można wznowić lub przerwania sesji kopiowania.  
 Jeśli sesja kopiowania hello jest hello pierwszej sesji kopii dysku, a następnie komunikat o błędzie hello powinny prezentować: "hello pierwszej sesji kopii nie można wznowić ani przerwane". W takim przypadku można usunąć starego pliku dziennika hello i ponownie uruchom polecenie hello.  
  
 Jeśli sesja kopiowania nie jest hello pierwszego dysku, można go zawsze wznowione lub zostało przerwane.  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a>Utratą hello pliku dziennika, może nadal utworzyć zadanie hello?  
 Hello plik dziennika dla dysku zawiera hello pełne informacje kopiowania danych toothis dysku i jest wymagane tooadd dysku toohello więcej plików i będą używane toocreate zadania importu. Jeśli plik dziennika hello zostaną utracone, konieczne będzie tooredo wszystkie sesje kopiowania hello hello dysku.  
  
## <a name="next-steps"></a>Następne kroki
 
* [Trwa konfigurowanie narzędzia importu/eksportu azure hello](../storage-import-export-tool-setup-v1.md)   
* [Przygotowywanie dysków twardych do zadania importu](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Sprawdzanie stanu zadania za pomocą plików dziennika kopiowania](../storage-import-export-tool-reviewing-job-status-v1.md)   
* [Naprawianie zadania importu](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Naprawianie zadania eksportu](../storage-import-export-tool-repairing-an-export-job-v1.md)
