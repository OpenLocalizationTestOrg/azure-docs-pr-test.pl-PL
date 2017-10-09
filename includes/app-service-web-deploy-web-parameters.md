Usługi Azure Resource Manager Zdefiniuj parametry dla wartości ma toospecify po wdrożeniu hello szablonu. Szablon Hello zawiera sekcji parametrów zawierający wszystkie hello wartości parametrów.
Należy zdefiniować parametr dla tych wartości, które będą się różnić na podstawie hello projektu, który jest wdrażany lub opartych na środowisku hello, który jest wdrażany z. Definiuje parametry dla wartości, które będą zawsze hello takie same. Każda wartość parametru jest używany w hello szablonu toodefine hello zasoby, które zostały wdrożone. 

Określając parametry, użyj hello **allowedValues** toospecify pola, które wartości użytkownika można podać podczas wdrażania. Użyj hello **defaultValue** tooassign pola parametru toohello wartości, jeśli wartość nie zostanie podana podczas wdrażania.

Firma Microsoft będzie opisywać każdego parametru w szablonie hello.

### <a name="sitename"></a>Nazwa witryny
Nazwa Hello hello aplikacji sieci web, że chcesz toocreate.

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a>hostingPlanName
Nazwa Hello hello usługi aplikacji — planowanie toouse do obsługi aplikacji sieci web hello.

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a>Jednostka SKU
Witaj warstwę cenową dla planu hostingu hello.

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

Szablon Hello definiuje hello wartości, które są dozwolone dla tego parametru, a następnie przypisuje wartość domyślną (S1), jeśli nie określono wartości.

### <a name="workersize"></a>workerSize
rozmiar wystąpienia Hello hello planu (małych, średnich i dużych) hostingu.

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

Szablon Hello definiuje hello wartości, które są dozwolone dla tego parametru (0, 1 lub 2) i przypisuje wartość domyślną (0), jeśli nie określono wartości. wartości Hello odpowiadają toosmall, średnich i dużych.

