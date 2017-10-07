---
title: "aaaAdd usługi Azure Storage za pomocą usług połączonych w programie Visual Studio | Dokumentacja firmy Microsoft"
description: "Dodaj aplikację tooyour usługi Azure Storage za pomocą programu Visual Studio Dodaj połączone usługi hello — okno dialogowe"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a>Dodawanie magazynu platformy Azure przy użyciu programu Visual Studio usługami
Za pomocą programu Visual Studio, można połączyć żadnego powitania po tooAzure magazynu przy użyciu hello **dodać usług połączonych** okna dialogowego:

- Usługi w chmurze C#
- Usługi mobilnej zaplecza .NET
- Witryny sieci Web ASP.NET lub usługi
- Usługi platformy ASP.NET Core
- Usługa zadań WebJob Azure 

Witaj podłączonej usługi funkcja dodaje wszystkie odwołania hello potrzebne i projektu tooyour kodu połączenia i odpowiednio modyfikuje plików konfiguracji. 

Po zakończeniu hello **dodać usług połączonych** automatycznie wyświetlone okno dialogowe dokumentacji wyszczególnieniem toostart wymagane kroki hello Praca z magazynu obiektów blob, kolejek i tabel.

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a>Połącz tooAzure magazynu przy użyciu usług połączonych hello okna dialogowego
1. Otwórz projekt w programie Visual Studio

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **usług połączonych** węzeł i z menu kontekstowego hello, a następnie wybierz **dodać podłączonej usługi**.
   
    ![Dodaj Azure połączona usługa](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. W hello **usług połączonych** wybierz pozycję **magazynu w chmurze z usługą Azure Storage**.
   
    ![Dodawanie magazynu Azure](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. W hello **usługi Azure Storage** okno dialogowe, wybierz istniejące konto magazynu i wybierz **Dodaj**.
   
    Jeśli potrzebujesz toocreate konta magazynu, przejdź toohello następnego kroku. W przeciwnym razie Pomiń toostep 6.
    
    ![Dodaj istniejące tooproject konta magazynu](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. toocreate konta magazynu: 
   
   1. Wybierz **Utwórz nowe konto magazynu** u dołu okna dialogowego hello hello.

   1. Wypełnianie hello **Utwórz konto magazynu** okna dialogowego, a następnie wybierz **Utwórz**.
      
       ![Nowe konto magazynu Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. Gdy hello **usługi Azure Storage** zostanie wyświetlone okno dialogowe, hello nowe konto magazynu jest wyświetlana na liście hello. Wybierz nowe konto magazynu hello hello listy, a następnie wybierz **Dodaj**.

1. Witaj magazynu podłączonej usługi pojawia się w obszarze hello **odwołania do usług** węzła projektu.
   
## <a name="how-your-project-is-modified"></a>Jak zmienić jest projektu
Po zakończeniu okna dialogowego hello Visual Studio dodaje odwołania i modyfikuje niektórych plików konfiguracyjnych. zmiany Hello są zależne od typu projektu hello: 

- Projekt ASP.NET - [co się stało — projekty programu ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126)
- Projekt platformy ASP.NET Core - [co się stało — projekty programu ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124) 
- Projekt usługi w chmurze (role sieci web i proces roboczy) - [co się stało — projekty usługi w chmurze](http://go.microsoft.com/fwlink/p/?LinkId=516965)
- Projekt zadania WebJob — [co się stało — projekty zadania WebJob](visual-studio/vs-storage-webjobs-what-happened.md)

## <a name="next-steps"></a>Następne kroki
- [MSDN Forum: Usługa Azure Storage](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [Blog zespołu usługi Magazyn Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/)
- [Dokumentację magazynu platformy Azure](https://docs.microsoft.com/azure/storage/)
