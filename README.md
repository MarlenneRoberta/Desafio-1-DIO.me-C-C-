# Desafio-1-DIO.me-C-C-

public interface ContaBancaria {

  void sacar(double valor);

  double getSaldo();

}

public class ContaCorrente implements ContaBancaria {

  private double saldo;



  public ContaCorrente(double saldoInicial) {

    this.saldo = saldoInicial;

  }



  @Override

  public void sacar(double valor) {

    if (saldo >= valor) {

      saldo -= valor;

      System.out.println("Saque de " + valor + " realizado na conta corrente.");

    } else {

      System.out.println("Saldo insuficiente na conta corrente.");

    }

  }



  @Override

  public double getSaldo() {

    return saldo;

  }

}

public class ContaSalario implements ContaBancaria {

  private double saldo;



  public ContaSalario(double saldoInicial) {

    this.saldo = saldoInicial;

  }



  @Override

  public void sacar(double valor) {

    if (saldo >= valor) {

      saldo -= valor;

      System.out.println("Saque de " + valor + " realizado na conta salário.");

    } else {

      System.out.println("Saldo insuficiente na conta salário.");

    }

  }



  @Override

  public double getSaldo() {

    return saldo;

  }

}

public aspect VerificadorSaldoAspect {

  pointcut operacaoDeSaque(ContaBancaria conta, double valor):

    execution(* ContaBancaria.sacar(double)) && target(conta) && args(valor);



  before(ContaBancaria conta, double valor): operacaoDeSaque(conta, valor) {

    if (conta.getSaldo() < valor) {

      System.out.println("Saldo insuficiente na conta " + conta.getClass().getSimpleName() + ".");

    }

  }

}

