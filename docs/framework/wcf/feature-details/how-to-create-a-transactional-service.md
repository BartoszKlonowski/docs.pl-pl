---
title: 'Instrukcje: tworzenie usługi transakcyjnej'
ms.date: 03/30/2017
ms.assetid: 1bd2e4ed-a557-43f9-ba98-4c70cb75c154
ms.openlocfilehash: c3d094dbd5822f6025e1cc6c90aab04b61459314
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96286295"
---
# <a name="how-to-create-a-transactional-service"></a>Instrukcje: tworzenie usługi transakcyjnej

W tym przykładzie przedstawiono różne aspekty tworzenia usługi transakcyjnej oraz użycie transakcji zainicjowanej przez klienta w celu koordynowania operacji usługi.  
  
### <a name="creating-a-transactional-service"></a>Tworzenie usługi transakcyjnej  
  
1. Utwórz kontrakt usługi i Dodaj adnotację do operacji z wymaganym ustawieniem z <xref:System.ServiceModel.TransactionFlowOption> wyliczenia, aby określić wymagania dotyczące transakcji przychodzących. Należy zauważyć, że można również umieścić <xref:System.ServiceModel.TransactionFlowAttribute> w implementowanej klasie usług. Dzięki temu pojedyncze implementacje interfejsu mogą korzystać z tych ustawień transakcji zamiast każdej implementacji.  
  
    ```csharp
    [ServiceContract]  
    public interface ICalculator  
    {  
        [OperationContract]  
        // Use this to require an incoming transaction  
        [TransactionFlow(TransactionFlowOption.Mandatory)]  
        double Add(double n1, double n2);  
        [OperationContract]  
        // Use this to permit an incoming transaction  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        double Subtract(double n1, double n2);  
    }  
    ```  
  
2. Utwórz klasę implementacji i Użyj, <xref:System.ServiceModel.ServiceBehaviorAttribute> Aby opcjonalnie określić <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> i <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A> . Należy zauważyć, że w wielu przypadkach wartość domyślna to <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A> 60 sekund i wartość domyślna <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> `Unspecified` to. Dla każdej operacji można użyć <xref:System.ServiceModel.OperationBehaviorAttribute> atrybutu, aby określić, czy prace wykonywane w ramach metody powinny należeć do zakresu transakcji zgodnie z wartością <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> atrybutu. W takim przypadku transakcja użyta dla `Add` metody jest taka sama jak obowiązkowa transakcja przychodząca, która jest przepływa z klienta, a transakcja użyta dla `Subtract` metody jest taka sama jak transakcja przychodząca, jeśli została przetworzona z klienta lub Nowa niejawnie i lokalnie utworzona transakcja.  
  
    ```csharp
    [ServiceBehavior(  
        TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable,  
        TransactionTimeout = "00:00:45")]  
    public class CalculatorService : ICalculator  
    {  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Add(double n1, double n2)  
        {  
            // Perform transactional operation  
            RecordToLog($"Adding {n1} to {n2}");
            return n1 + n2;  
        }  
  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Subtract(double n1, double n2)  
        {  
            // Perform transactional operation  
            RecordToLog($"Subtracting {n2} from {n1}");
            return n1 - n2;  
        }  
  
        private static void RecordToLog(string recordText)  
        {  
            // Database operations omitted for brevity  
            // This is where the transaction provides specific benefit  
            // - changes to the database will be committed only when  
            // the transaction completes.  
        }  
    }  
    ```  
  
3. Skonfiguruj powiązania w pliku konfiguracji, określając, że kontekst transakcji powinien być przepływem, i protokoły, które mają być używane w tym celu. Aby uzyskać więcej informacji, zobacz [Konfiguracja transakcji ServiceModel](servicemodel-transaction-configuration.md). W każdym przypadku typ powiązania jest określony w atrybucie elementu punktu końcowego `binding` . [\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-element.md)Element zawiera `bindingConfiguration` atrybut odwołujący się do konfiguracji powiązania o nazwie `transactionalOleTransactionsTcpBinding` , jak pokazano w poniższej konfiguracji przykładowej.  
  
    ```xml  
    <service name="CalculatorService">  
      <endpoint address="net.tcp://localhost:8008/CalcService"  
        binding="netTcpBinding"  
        bindingConfiguration="transactionalOleTransactionsTcpBinding"  
        contract="ICalculator"  
        name="OleTransactions_endpoint" />  
    </service>  
    ```  
  
     Przepływ transakcji jest włączony na poziomie konfiguracji przy użyciu `transactionFlow` atrybutu, a protokół transakcji jest określany przy użyciu `transactionProtocol` atrybutu, jak pokazano w poniższej konfiguracji.  
  
    ```xml  
    <bindings>  
      <netTcpBinding>  
        <binding name="transactionalOleTransactionsTcpBinding"  
          transactionFlow="true"  
          transactionProtocol="OleTransactions"/>  
      </netTcpBinding>  
    </bindings>  
    ```  
  
### <a name="supporting-multiple-transaction-protocols"></a>Obsługa wielu protokołów transakcji  
  
1. Aby uzyskać optymalną wydajność, należy użyć protokołu OleTransactions na potrzeby scenariuszy obejmujących klienta i usługę zapisaną przy użyciu Windows Communication Foundation (WCF). Jednak protokół WS-AtomicTransaction (WS-AT) jest użyteczny w scenariuszach, gdy wymagane jest współdziałanie z stosami protokołu innych firm. Usługi WCF można skonfigurować tak, aby akceptowały oba protokoły, dostarczając wiele punktów końcowych z odpowiednimi powiązaniami specyficznymi dla protokołu, jak pokazano w poniższej konfiguracji przykładowej.  
  
    ```xml  
    <service name="CalculatorService">  
      <endpoint address="http://localhost:8000/CalcService"  
        binding="wsHttpBinding"  
        bindingConfiguration="transactionalWsatHttpBinding"  
        contract="ICalculator"  
        name="WSAtomicTransaction_endpoint" />  
      <endpoint address="net.tcp://localhost:8008/CalcService"  
        binding="netTcpBinding"  
        bindingConfiguration="transactionalOleTransactionsTcpBinding"  
        contract="ICalculator"  
        name="OleTransactions_endpoint" />  
    </service>  
    ```  
  
     Protokół transakcji jest określony przy użyciu `transactionProtocol` atrybutu. Jednak ten atrybut jest nieobecny w dostarczonych przez system `wsHttpBinding` , ponieważ to powiązanie może korzystać tylko z protokołu WS-AT.  
  
    ```xml  
    <bindings>  
      <wsHttpBinding>  
        <binding name="transactionalWsatHttpBinding"  
          transactionFlow="true" />  
      </wsHttpBinding>  
      <netTcpBinding>  
        <binding name="transactionalOleTransactionsTcpBinding"  
          transactionFlow="true"  
          transactionProtocol="OleTransactions"/>  
      </netTcpBinding>  
    </bindings>  
    ```  
  
### <a name="controlling-the-completion-of-a-transaction"></a>Kontrolowanie ukończenia transakcji  
  
1. Domyślnie operacje WCF automatycznie uzupełniają transakcje, jeśli nie zostaną zgłoszone żadne Nieobsłużone wyjątki. To zachowanie można zmodyfikować przy użyciu <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> właściwości i <xref:System.ServiceModel.OperationContext.SetTransactionComplete%2A> metody. Gdy operacja jest wymagana w ramach tej samej transakcji, co inna operacja (na przykład Debet i kredyt), można wyłączyć zachowanie autouzupełniania, ustawiając <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> Właściwość na `false` tak jak pokazano w poniższym `Debit` przykładzie operacji. Transakcja, której `Debit` używa operacja, nie zostanie zakończona do momentu wywołania metody z <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> ustawioną właściwością `true` , jak pokazano w operacji `Credit1` , lub gdy <xref:System.ServiceModel.OperationContext.SetTransactionComplete%2A> wywoływana jest metoda, aby jawnie oznaczyć transakcję jako kompletną, jak pokazano w operacji `Credit2` . Należy zauważyć, że dwie operacje kredytowe są przedstawiane na potrzeby ilustracji i że pojedyncze operacje kredytowe byłyby bardziej typowe.  
  
    ```csharp
    [ServiceBehavior]  
    public class CalculatorService : IAccount  
    {  
        [OperationBehavior(  
            TransactionScopeRequired = true, TransactionAutoComplete = false)]  
        public void Debit(double n)  
        {  
            // Perform debit operation  
  
            return;  
        }  
  
        [OperationBehavior(  
            TransactionScopeRequired = true, TransactionAutoComplete = true)]  
        public void Credit1(double n)  
        {  
            // Perform credit operation  
  
            return;  
        }  
  
        [OperationBehavior(  
            TransactionScopeRequired = true, TransactionAutoComplete = false)]  
        public void Credit2(double n)  
        {  
            // Perform alternate credit operation  
  
            OperationContext.Current.SetTransactionComplete();  
            return;  
        }  
    }  
    ```  
  
2. Na potrzeby korelacji transakcji ustawienie <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> właściwości `false` wymaga użycia powiązania sesji. To wymaganie jest określone za pomocą `SessionMode` właściwości w <xref:System.ServiceModel.ServiceContractAttribute> .  
  
    ```csharp
    [ServiceContract(SessionMode = SessionMode.Required)]  
    public interface IAccount  
    {  
        [OperationContract]  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        void Debit(double n);  
        [OperationContract]  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        void Credit1(double n);  
        [OperationContract]  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        void Credit2(double n);  
    }  
    ```  
  
### <a name="controlling-the-lifetime-of-a-transactional-service-instance"></a>Kontrolowanie okresu istnienia wystąpienia usługi transakcyjnej  
  
1. Funkcja WCF używa <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A> właściwości, aby określić, czy bazowe wystąpienie usługi jest wydawany po zakończeniu transakcji. Ponieważ ta wartość domyślna to `true` , o ile nie zostanie skonfigurowany w inny sposób, usługa WCF wykazuje wydajne i przewidywalne zachowanie aktywacji "just-in-Time". Wywołania usługi w kolejnej transakcji są gwarantowane nowym wystąpieniem usługi bez postanowień poprzedniego stanu transakcji. Chociaż jest to często przydatne, czasami warto zachować stan w ramach wystąpienia usługi poza ukończeniem transakcji. Przykłady tego stanu byłyby kosztowne do pobrania lub odtworzenia zasobów. Można to zrobić, ustawiając <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A> Właściwość na `false` . W przypadku tego ustawienia wystąpienie i wszystkie powiązane Stany będą dostępne po kolejnych wywołaniach. W tym celu należy zwrócić szczególną uwagę na to, kiedy i w jaki sposób stan i transakcje zostaną wyczyszczone i zakończone. Poniższy przykład demonstruje, jak to zrobić, utrzymując wystąpienie ze `runningTotal` zmienną.  
  
    ```csharp
    [ServiceBehavior(TransactionIsolationLevel = [ServiceBehavior(  
        ReleaseServiceInstanceOnTransactionComplete = false)]  
    public class CalculatorService : ICalculator  
    {  
        double runningTotal = 0;  
  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Add(double n)  
        {  
            // Perform transactional operation  
            RecordToLog($"Adding {n} to {runningTotal}");
            runningTotal = runningTotal + n;  
            return runningTotal;  
        }  
  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Subtract(double n)  
        {  
            // Perform transactional operation  
            RecordToLog($"Subtracting {n} from {runningTotal}");
            runningTotal = runningTotal - n;  
            return runningTotal;  
        }  
  
        private static void RecordToLog(string recordText)  
        {  
            // Database operations omitted for brevity  
        }  
    }  
    ```  
  
    > [!NOTE]
    > Ponieważ okres istnienia wystąpienia jest zachowaniem wewnętrznym dla usługi i kontrolowanym przez <xref:System.ServiceModel.ServiceBehaviorAttribute> Właściwość, nie jest wymagane żadne modyfikacje w konfiguracji usługi lub kontrakcie usługi, aby można było ustawić zachowanie wystąpienia. Ponadto drut nie będzie zawierał żadnych reprezentacji.
