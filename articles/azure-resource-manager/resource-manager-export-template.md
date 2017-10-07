---
title: "Szablon usługi Azure Resource Manager aaaExport | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager tooexport szablon z istniejącej grupy zasobów."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a>Eksportowanie szablonu usługi Azure Resource Manager z istniejących zasobów
W tym artykule dowiesz się, jak tooexport szablonem usługi Resource Manager z istniejących zasobów w ramach subskrypcji. Możesz użyć tego toogain wygenerowanego szablonu lepszego zrozumienia składni szablonu.

Istnieją dwa sposoby tooexport szablonu:

* Możesz wyeksportować hello **rzeczywiste szablon używany do wdrażania**. Hello wyeksportowanego szablonu obejmuje wszystkie hello parametry i zmienne, dokładnie tak, jak znalazły się na oryginalnym szablonie hello. Takie podejście jest przydatne podczas wdrażania zasobów za pośrednictwem portalu hello i mają toosee hello szablonu toocreate tych zasobów. Ten szablon jest gotowy do użycia. 
* Możesz wyeksportować **wygenerowane z szablonu, która reprezentuje bieżący stan grupy zasobów hello hello**. Witaj wyeksportowanego szablonu nie jest oparta na dowolnego szablonu, który został użyty do wdrożenia. Zamiast tego tworzy szablon, który jest migawką hello grupy zasobów. Witaj wyeksportowanego szablonu ma wiele wartości stałe i prawdopodobnie nie jako wiele parametrów, jak zwykle należy zdefiniować. Takie rozwiązanie jest przydatne, gdy hello grupy zasobów zostały zmodyfikowane po wdrożeniu. Taki szablon zwykle wymaga modyfikacji, zanim będzie go można użyć.

W tym temacie przedstawiono oba podejścia za pośrednictwem portalu hello.

## <a name="deploy-resources"></a>Wdrażanie zasobów
Zacznijmy od wdrażania tooAzure zasobów, używanej do eksportowania jako szablon. Jeśli masz już grupę zasobów w ramach subskrypcji, które mają tooexport tooa szablonu, możesz pominąć tę sekcję. Witaj dalszej części tego artykułu przyjęto założenie, że wdrożono hello aplikacji sieci web i rozwiązanie bazy danych SQL w tej sekcji. Jeśli używasz inne rozwiązanie środowiska mogą się nieco różnić, ale są tooexport szablon czynności hello hello takie same. 

1. W hello [portalu Azure](https://portal.azure.com), wybierz pozycję **nowy**.
   
      ![wybieranie nowego elementu](./media/resource-manager-export-template/new.png)
2. Wyszukaj **aplikacja sieci web i SQL** i wybierz ją z hello dostępnych opcji.
   
      ![wyszukiwanie aplikacji internetowej i bazy danych SQL](./media/resource-manager-export-template/webapp-sql.png)

3. Wybierz pozycję **Utwórz**.

      ![wybieranie pozycji Utwórz](./media/resource-manager-export-template/create.png)

4. Podaj wartości wymagane hello hello aplikacji sieci web i bazy danych SQL. Wybierz pozycję **Utwórz**.

      ![podawanie wartości dla aplikacji internetowej i bazy danych SQL](./media/resource-manager-export-template/provide-web-values.png)

Witaj wdrożenia może zająć kilka minut. Po zakończeniu wdrożenia hello subskrypcja zawiera hello rozwiązania.

## <a name="view-template-from-deployment-history"></a>Wyświetlanie szablonu z historii wdrożenia
1. Przejdź toohello bloku grupy zasobów dla nowej grupy zasobów. Należy zauważyć, że tego bloku hello przedstawia wynik hello hello ostatniego wdrożenia. Wybierz ten link.
   
      ![blok grupy zasobów](./media/resource-manager-export-template/select-deployment.png)
2. Zostanie wyświetlona historia wdrożeń dla grupy hello. W Twoim przypadku bloku hello wymieniono prawdopodobnie tylko jedno wdrożenie. Wybierz to wdrożenie.
   
     ![ostatnie wdrożenie](./media/resource-manager-export-template/select-history.png)
3. Blok Hello Wyświetla podsumowanie hello wdrożenia. Hello Podsumowanie zawiera stan hello hello wdrożenia i jego operacji oraz wartości hello, które podany dla parametrów. używany dla wdrożenia hello, wybierz szablon hello toosee **Wyświetl szablon**.
   
     ![wyświetlanie podsumowania wdrożenia](./media/resource-manager-export-template/view-template.png)
4. Usługa Resource Manager pobiera hello czynności siedem plików:
   
   1. **Szablon** -hello szablonu, który definiuje infrastrukturę Twojego rozwiązania hello. Po utworzeniu konta magazynu hello za pośrednictwem portalu hello Resource Manager używany toodeploy szablonu go i zapisała ten szablon do użytku w przyszłości.
   2. **Parametry** -pliku parametrów czy toopass można użyć w wartości podczas wdrażania. Zawiera wartości hello, które podane podczas pierwszego wdrażania hello. Podczas ponownego wdrażania szablonu hello można zmienić dowolne z tych wartości.
   3. **Interfejs wiersza polecenia** -Azure polecenia wiersza interfejsu (CLI) pliku skryptu służy toodeploy hello szablonu.
   3. **Interfejs wiersza polecenia 2.0** -Azure polecenia wiersza interfejsu (CLI) pliku skryptu służy toodeploy hello szablonu.
   4. **PowerShell** — czy toodeploy hello szablonu można użyć pliku skryptu programu Azure PowerShell.
   5. **.NET** -służy toodeploy hello szablonu klasy A .NET.
   6. **Ruby** -klasy A Ruby służy toodeploy hello szablonu.
      
      pliki Hello są dostępne za pośrednictwem łącza między hello bloku. Domyślnie bloku hello Wyświetla szablon hello.
      
       ![wyświetlanie szablonu](./media/resource-manager-export-template/see-template.png)
      
Ten szablon jest rzeczywista szablonu hello używanych toocreate aplikacji sieci web i bazy danych SQL. Należy zauważyć, że zawiera on parametry umożliwiające tooprovide różne wartości podczas wdrażania. toolearn więcej informacji na temat struktury hello szablonu, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).

## <a name="export-hello-template-from-resource-group"></a>Eksportowanie szablonu hello z grupy zasobów
Jeśli ręcznie zmienić zasoby lub dodać zasoby w wielu wdrożeń, pobieranie szablonu z historii wdrożenia hello nie odzwierciedlały bieżący stan hello hello grupy zasobów. W tej sekcji przedstawiono, jak tooexport szablonu, które odzwierciedla hello bieżący stan hello grupy zasobów. 

> [!NOTE]
> Nie można eksportować szablonu dla grupy zasobów zawierającej ponad 200 zasobów.
> 
> 

1. tooview hello szablonu dla grupy zasobów, wybierz opcję **skryptu automatyzacji**.
   
      ![eksportowanie grupy zasobów](./media/resource-manager-export-template/select-automation.png)
   
     Menedżer zasobów szacuje hello zasoby w grupie zasobów hello oraz generuje szablon dla tych zasobów. Nie wszystkie typy zasobów obsługują hello eksportowania szablonu funkcji. Może zostać wyświetlony komunikat o błędzie informujący, że istnieje problem z hello eksportu. Dowiedz się, jak toohandle tych problemów w hello [kwestie związane z eksportem poprawka](#fix-export-issues) sekcji.
2. Ponownie Zobacz pliki sześciu hello służy tooredeploy hello rozwiązania. Jednak ten czas hello szablon jest nieco inne. Należy zauważyć, że hello wygenerowanego szablonu zawiera parametry mniej niż szablon hello w poprzedniej sekcji. Ponadto wiele hello wartości (takie jak lokalizacja i wartości jednostki SKU) jest ustalony w tym szablonie, a nie przyjmuje wartość parametru. Przed ponownym tego szablonu, może zaistnieć tooedit hello szablonu toomake lepiej wykorzystać parametrów. 
   
3. Masz kilka opcji dla dalszego toowork przy użyciu tego szablonu. Można pobrać szablonu hello i na nim pracować lokalnie za pomocą edytora JSON. Lub można zapisać hello szablonu tooyour biblioteki i pracy z nim za pośrednictwem portalu hello.
   
     Jeśli potrafisz za pomocą edytora JSON, takich jak [kodzie VS](https://code.visualstudio.com/) lub [programu Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), można wybrać Pobieranie szablonu hello lokalnie i za pomocą tego edytora. toowork lokalnie, wybierz opcję **Pobierz**.
   
      ![pobieranie szablonu](./media/resource-manager-export-template/download-template.png)
   
     Jeśli nie są skonfigurowane za pomocą edytora JSON można wybrać edycji szablonu hello za pośrednictwem portalu hello. Witaj pozostałej części tematu przyjęto założenie, że biblioteka tooyour szablonów hello zostały zapisane w portalu hello. Ważne jest, aby hello sama składnia zmienia toohello szablonu, czy działa lokalnie za pomocą edytora JSON lub za pośrednictwem portalu hello. Wybierz toowork za pośrednictwem portalu hello **dodać toolibrary**.
   
      ![Dodaj toolibrary](./media/resource-manager-export-template/add-to-library.png)
   
     Podczas dodawania biblioteki toohello szablonów, należy nadać szablonowi hello nazwę i opis. Następnie wybierz pozycję **Zapisz**.
   
     ![ustawianie wartości szablonu](./media/resource-manager-export-template/save-library-template.png)
4. tooview szablonu zapisana w bibliotece, wybierz **więcej usług**, typ **szablony** toofilter wyniki, wybierz opcję **szablony**.
   
      ![znajdowanie szablonów](./media/resource-manager-export-template/find-templates.png)
5. Wybierz szablon hello o nazwie hello, który został zapisany.
   
      ![wybieranie szablonu](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a>Dostosowywanie szablonu hello
Hello wyeksportowany szablon działa poprawnie, jeśli chcesz toocreate hello sam sieci web aplikacji i bazy danych SQL dla każdego wdrożenia. Usługa Resource Manager oferuje jednak opcje, dzięki którym można wdrażać szablony ze znacznie większą elastycznością. W tym artykule opisano, jak parametry tooadd hello bazy danych, nazwę i hasło administratora. Można użyć tego samego tooadd podejście większą elastyczność i innych wartości na powitania szablonu.

1. toocustomize hello szablonu, wybierz opcję **Edytuj**.
   
     ![wyświetlanie szablonu](./media/resource-manager-export-template/select-edit.png)
2. Wybierz szablon hello.
   
     ![edytowanie szablonu](./media/resource-manager-export-template/select-added-template.png)
3. toobe toopass stanie hello wartości, które toospecify podczas wdrażania, Dodaj hello następujące dwa parametry toohello **parametry** części szablonu hello:

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. nowe parametry hello toouse zastąpić definicji serwera SQL hello hello **zasobów** sekcji. Zwróć uwagę, że właściwości **administratorLogin** i **administratorLoginPassword** korzystają teraz z wartości parametrów.

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. Wybierz **OK** po zakończeniu edycji szablonu hello.
7. Wybierz **zapisać** toosave hello zmiany toohello szablonu.
   
     ![zapisywanie szablonu](./media/resource-manager-export-template/save-template.png)
8. tooredeploy hello zaktualizowany szablon, wybierz opcję **Wdróż**.
   
     ![wdrażanie szablonu](./media/resource-manager-export-template/redeploy-template.png)
9. Podaj wartości parametrów, a następnie wybierz zasób grupy toodeploy hello zasobów.


## <a name="fix-export-issues"></a>Rozwiązywanie problemów z eksportowaniem
Nie wszystkie typy zasobów obsługują hello eksportowania szablonu funkcji. Ten problem, ręcznie tooresolve hello Brak zasobów z powrotem dodać do szablonu. komunikat o błędzie Hello obejmuje hello typów zasobów, które nie mogą być eksportowane. Znajdź ten typ zasobów w [dokumentacji szablonu](/azure/templates/). Na przykład toomanually dodać bramę sieci wirtualnej, zobacz [odwołania do szablonu Microsoft.Network/virtualNetworkGateways](/azure/templates/microsoft.network/virtualnetworkgateways).

> [!NOTE]
> Problemy związane z eksportowaniem występują tylko podczas eksportowania szablonu na podstawie grupy roboczej, a nie z historii wdrożenia. Jeśli ostatniego wdrożenia dokładnie odzwierciedla bieżący stan hello hello grupy zasobów, możesz wyeksportować szablon hello z historii wdrożenia hello, a nie z hello grupy zasobów. Po dokonaniu zmiany toohello grup zasobów, nie są zdefiniowane w jednym szablonie tylko wyeksportować z grupy zasobów.
> 
> 

## <a name="next-steps"></a>Następne kroki
Wiesz już, jak tooexport szablonu z zasobów, które zostały utworzone w portalu hello.

* Szablon można wdrożyć przy użyciu [programu PowerShell](resource-group-template-deploy.md), [interfejsu wiersza polecenia platformy Azure](resource-group-template-deploy-cli.md) lub [interfejsu API REST](resource-group-template-deploy-rest.md).
* toosee tooexport szablonu za pomocą programu PowerShell, zobacz temat [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](powershell-azure-resource-manager.md).
* toosee tooexport szablonu za pomocą interfejsu wiersza polecenia Azure, zobacz temat [Użyj hello Azure CLI for Mac, Linux i Windows za pomocą Menedżera zasobów Azure](xplat-cli-azure-resource-manager.md).

