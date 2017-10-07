---
title: "aaaMove tooAzure maszyn wirtualnych systemu Windows usług AWS | Dokumentacja firmy Microsoft"
description: "Przenieś tooAzure wystąpienia Windows EC2 Amazon Web Services (AWS) maszyn wirtualnych przy użyciu programu Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: cynthn
ms.openlocfilehash: f912c28d3ffe585162c3add715a1318ac3cd4643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a>Przenieś Maszynę wirtualną systemu Windows z tooAzure Amazon Web Services (AWS) przy użyciu programu PowerShell

Jeśli dokonujesz oceny maszyn wirtualnych platformy Azure do obsługi obciążeń, można wyeksportować istniejącego wystąpienia maszyny Wirtualnej systemu Windows EC2 Amazon Web Services (AWS). następnie przekaż hello tooAzure wirtualnego dysku twardego (VHD). Raz hello, który jest przekazywany wirtualnego dysku twardego, można utworzyć nowej maszyny Wirtualnej na platformie Azure z hello wirtualnego dysku twardego. 

W tym temacie omówiono przeniesienie jednej maszyny Wirtualnej z usług AWS tooAzure. Jeśli chcesz, aby maszyny wirtualne toomove z usług AWS tooAzure na dużą skalę, zobacz [migracji maszyn wirtualnych w tooAzure Amazon Web Services (AWS) z usługą Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).

## <a name="prepare-hello-vm"></a>Przygotowanie hello maszyny Wirtualnej 
 
Możesz przekazać zarówno ogólnych i specjalnych tooAzure wirtualne dyski twarde. Każdy typ wymaga, aby przygotować hello maszyny Wirtualnej przed eksportem z usług AWS. 

- **Uogólniony wirtualny dysk twardy** -uogólniony wirtualny dysk twardy ma wszystkie informacje osobiste Konto usunięte za pomocą programu Sysprep. Jeśli planujesz hello toouse toocreate obrazu wirtualnego dysku twardego nowych maszyn wirtualnych z, wykonaj następujące czynności: 
 
    * [Przygotowywanie maszyny Wirtualnej systemu Windows](prepare-for-upload-vhd-image.md).  
    * Generalize hello maszyny wirtualnej za pomocą programu Sysprep.  

 
- **Specjalizowany wirtualnego dysku twardego** -specjalne wirtualnego dysku twardego przechowuje hello kont użytkowników, aplikacji i innych danych o stanie z oryginalnego maszyny Wirtualnej. Jeśli planujesz toouse hello wirtualnego dysku twardego — jest toocreate nowej maszyny Wirtualnej, upewnij się, hello następujące kroki zostały zakończone.  
    * [Przygotowanie tooAzure tooupload wirtualnego dysku twardego Windows](prepare-for-upload-vhd-image.md). **Nie** generalize hello maszyny Wirtualnej przy użyciu narzędzia Sysprep. 
    * Usuń wszystkie narzędzia wirtualizacji gościa i agentów, które są zainstalowane na powitania maszyny Wirtualnej (np. narzędzi VMware). 
    * Upewnij się, hello maszyna wirtualna jest skonfigurowana toopull jego adres IP i ustawienia DNS za pośrednictwem protokołu DHCP. To zapewnia, że ten serwer hello uzyskuje adres IP w ramach hello sieci wirtualnej podczas uruchamiania.  


## <a name="export-and-download-hello-vhd"></a>Eksportowanie i Pobierz hello wirtualnego dysku twardego 

Wyeksportuj hello EC2 wystąpienia tooa wirtualnego dysku twardego w zasobniku Amazon S3. Hello kroków opisanych w temacie dokumentacji Amazon hello [eksportowanie wystąpienia jako maszyny Wirtualnej przy użyciu maszyny Wirtualnej importu/eksportu](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) i wykonywania hello [tworzenie — wystąpienie export zadania](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) polecenia tooexport hello EC2 plik VHD tooa wystąpienia. 

Witaj wyeksportowany plik wirtualnego dysku twardego jest zapisywany w zasobniku hello Amazon S3, które określisz. Witaj podstawowa składnia eksportowanie hello wirtualnego dysku twardego jest poniżej, po prostu zastąpić tekst zastępczy hello w <brackets> z informacjami.

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

Po wyeksportowaniu hello wirtualnego dysku twardego, wykonaj te instrukcje hello [sposób pobrać obiektu z przedział S3?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello wirtualnego dysku twardego plik z zasobnika hello S3. 

> [!IMPORTANT]
> Usług AWS pobiera opłaty transferu danych do pobrania hello wirtualnego dysku twardego. Zobacz [Amazon S3 cennik](https://aws.amazon.com/s3/pricing/) Aby uzyskać więcej informacji.


## <a name="next-steps"></a>Następne kroki

Możesz teraz przekazać hello tooAzure wirtualnego dysku twardego i tworzenie nowej maszyny Wirtualnej. 

- Po przeprowadzeniu programu Sysprep w źródle zbyt**generalize** go przed wykonaniem operacji eksportowania, zobacz [przekazać uogólniony wirtualny dysk twardy i korzystać z niego toocreate nowych maszyn wirtualnych na platformie Azure](upload-generalized-managed.md)
- Jeśli nie zostało uruchomione narzędzie Sysprep przed wykonaniem operacji eksportowania, hello wirtualnego dysku twardego jest traktowany jako **specjalne**, zobacz [przekazywanie specjalne tooAzure wirtualnego dysku twardego i utworzyć nową maszynę Wirtualną](create-vm-specialized.md)

 
