---
title: "Uzyskiwanie dostępu do maszyn wirtualnych platformy Azure z poziomu Eksploratora serwera | Dokumentacja firmy Microsoft"
description: "GET, omówienie sposobu wyświetlania tworzenie i zarządzanie nimi Azure maszynach wirtualnych (VM) w Eksploratorze serwera w programie Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/31/2017
ms.author: kraigb
ms.openlocfilehash: 75dcc603327b50718b279f3ce055663ec0bc2596
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>Uzyskiwanie dostępu do maszyn wirtualnych platformy Azure z poziomu Eksploratora serwera
Za pomocą Eksploratora serwera w programie Visual Studio, można wyświetlić informacje o maszynach wirtualnych obsługiwanych przez platformę Azure.

## <a name="accessing-virtual-machines-in-server-explorer"></a>Uzyskiwanie dostępu do maszyn wirtualnych w Eksploratorze serwera
Jeśli masz maszyn wirtualnych hostowanych na platformie Azure, możesz uzyskiwać do nich dostęp w Eksploratorze serwera. Musisz najpierw zalogować się do subskrypcji platformy Azure do wyświetlania usług mobilnych. Aby się zarejestrować, otwórz menu skrótów dla usługi Azure węzła w Eksploratorze serwera i wybierz **Connect do systemu Microsoft Azure**.

### <a name="to-get-information-about-your-virtual-machines"></a>Aby uzyskać informacje o maszynach wirtualnych
1. W Eksploratorze chmury wybierz maszynę wirtualną, a następnie wybierz klawisz F4 do wyświetlenia okna właściwości.
   
    W poniższej tabeli przedstawiono właściwości, które są dostępne, ale są one wszystkich tylko do odczytu. Aby je zmienić, należy użyć [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   
   | Właściwość | Opis |
   | --- | --- |
   | Nazwa DNS |Adres URL z internetowego adresu maszyny wirtualnej. |
   | Środowisko |Dla maszyny wirtualnej wartość tej właściwości jest zawsze produkcji. |
   | Nazwa |Nazwa maszyny wirtualnej. |
   | Rozmiar |Rozmiar maszyny wirtualnej, co wskazuje ilość pamięci i miejsca na dysku, który jest dostępny. Aby uzyskać więcej informacji, zobacz [rozmiarów maszyn wirtualnych](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs). |
   | Stan |Wartości obejmują uruchamianie, wprowadzenie, zatrzymywania, zatrzymane i pobierania stanu. Jeśli pojawi się podczas pobierania stanu, bieżący stan jest nieznany. Wartości dla tej właściwości różnią się od wartości, które są używane na [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). |
   | Identyfikator subskrypcji |Identyfikator subskrypcji dla konta platformy Azure. Informacje te można wyświetlić na [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) wyświetlając właściwości dla subskrypcji. |
2. Wybierz węzeł punktu końcowego, a następnie Wyświetl **właściwości** okna.
3. W poniższej tabeli opisano dostępne właściwości punktów końcowych, ale są one tylko do odczytu. Aby dodać lub edytować punktów końcowych dla maszyny wirtualnej, użyj [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). 
   
   | Właściwość | Opis |
   | --- | --- |
   | Nazwa |Identyfikator dla punktu końcowego. |
   | Port prywatny |Port dostępu do sieci wewnętrznej do aplikacji. |
   | Protokół |Protokół, który korzysta z warstwy transportowej dla tego punktu końcowego, TCP lub UDP. |
   | Port publiczny |Port używany na publiczny dostęp do aplikacji. |

## <a name="next-steps"></a>Następne kroki
Aby dowiedzieć się więcej o korzystaniu z platformy Azure ról w programie Visual Studio, zobacz [za pomocą pulpitu zdalnego z rolami Azure](vs-azure-tools-remote-desktop-roles.md).

