---
title: "aaaMount usługi Azure file storage z maszyny Wirtualnej systemu Windows Azure | Dokumentacja firmy Microsoft"
description: "Przechowywanie plików w chmurze hello z usługą Magazyn plików Azure i instalowanie udziału plików w chmurze z maszyny wirtualnej platformy Azure (VM)."
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a>Udziały plików platformy Azure za pomocą maszyn wirtualnych systemu Windows 

Udziały plików platformy Azure można użyć jako sposobu toostore i dostęp do plików z maszyny Wirtualnej. Na przykład można przechowywać skrypt lub plik konfiguracji aplikacji, które mają tooshare maszyn wirtualnych. W tym temacie zostanie przedstawiony zostanie sposób udziału plików toocreate i instalacji platformy Azure i w jaki sposób tooupload i pobierania plików.

## <a name="connect-tooa-file-share-from-a-vm"></a>Połącz tooa udział plików z maszyny Wirtualnej

W tej sekcji założono, że masz już udział, które mają tooconnect do plików. Jeśli potrzebujesz toocreate jedną zobacz [utworzyć udział plików](#create-a-file-share) dalszej części tego tematu.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu po lewej stronie powitania kliknij **kont magazynu**.
3. Wybierz konto magazynu.
4. W hello **omówienie** w obszarze **usług**, wybierz pozycję **pliki**.
5. Wybierz udział plików.
6. Kliknij przycisk **Connect** tooopen strona zawierająca hello składni wiersza polecenia dla udziału plików hello instalowanie w systemie Windows lub Linux.
7. Wyróżnij hello Składnia polecenia hello i wklej go w Notatniku lub w innym miejscu gdzie możesz łatwo do niego dostęp. 
8. Edytuj hello składni tooremove hello wiodące ** > ** i Zastąp *[litera dysku]* z literą dysku hello (na przykład **/Y:**) miejsce chcesz udziału plików hello toomount.
8. Podłącz tooyour maszyny Wirtualnej, a następnie otwórz okno wiersza polecenia.
9. Wklej w hello edytować składni połączenia i trafień **Enter**.
10. Po utworzeniu połączenia hello otrzymasz wiadomość hello **hello polecenie zostało wykonane pomyślnie.**
11. Sprawdź połączenie hello, wpisując w hello dysku litery tooswitch toothat stacji, a następnie wpisz **dir** toosee zawartość hello hello udziału plików.



## <a name="create-a-file-share"></a>Tworzenie udziału plików 
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu po lewej stronie powitania kliknij **kont magazynu**.
3. Wybierz konto magazynu.
4. W hello **omówienie** w obszarze **usług**, wybierz pozycję **pliki**.
5. Na stronie usługi plików powitania kliknij **+ udział pliku** toocreate udostępnianie pierwszego pliku. \
6. Wprowadź nazwę udziału plików hello. Nazwy udziałów plików można użyć, małe litery, cyfry i łączniki pojedynczego. Nazwa Hello nie może rozpoczynać się od łącznika i nie można używać wielu łączników obok siebie. 
7. Wypełnij limit na rozmiar pliku hello można się too5120 GB.
8. Kliknij przycisk **OK** udziału plików hello toodeploy.
   
## <a name="upload-files"></a>Przekazywanie plików
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu po lewej stronie powitania kliknij **kont magazynu**.
3. Wybierz konto magazynu.
4. W hello **omówienie** w obszarze **usług**, wybierz pozycję **pliki**.
5. Wybierz udział plików.
6. Kliknij przycisk **przekazać** tooopen hello **przekazać pliki** strony.
7. Polecenie toobrowse ikona folderu hello lokalnego systemu plików dla tooupload pliku.   
8. Kliknij przycisk **przekazać** udziału plików toohello tooupload hello pliku.

## <a name="download-files"></a>Pobieranie plików
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu po lewej stronie powitania kliknij **kont magazynu**.
3. Wybierz konto magazynu.
4. W hello **omówienie** w obszarze **usług**, wybierz pozycję **pliki**.
5. Wybierz udział plików.
6. Kliknij prawym przyciskiem myszy na powitania plik i wybierz polecenie **Pobierz** toodownload on tooyour komputera lokalnego.
   

## <a name="next-steps"></a>Następne kroki

Można również tworzyć i Zarządzanie udziałami plików przy użyciu programu PowerShell. Aby uzyskać więcej informacji, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](../../storage/files/storage-dotnet-how-to-use-files.md).
