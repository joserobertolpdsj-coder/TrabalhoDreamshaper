# TrabalhoDreamshaper
Trabalho para a faculdade de Ciência da computação, o objeto é criar um programa em Java que abasteça uma planilha de faturamento.

#Programa principal
package principal;

import java.util.Scanner;

import colaborador.ColaboradorComissionado;
import colaborador.ColaboradorPadrao;
import colaborador.ColaboradorProducao;

public class Principal {	

	public static void main(String[] args) {
		//IMPORTANDO
		Scanner teclado = new Scanner(System.in);
		ColaboradorPadrao cp = new ColaboradorPadrao();
		ColaboradorComissionado cc = new ColaboradorComissionado();
		ColaboradorProducao cpp = new ColaboradorProducao();
		int op=0;
		//INTERACAO COM USUARIO
		do {
		
		System.out.println("****TRABALHO DREAMSHAPER****");
		System.out.println("---ESCOLHA O TIPO DE COLABORADOR---");
		System.out.println("[1] Colaborador padrão");
		System.out.println("[2] Colaborador comissionado");
		System.out.println("[3] Colaborador produção");
		System.out.println("[0] Sair do programa");
		System.out.println("Opção: ");
		op = teclado.nextInt();
		
		switch(op) {
		case 1: cp.Dados();cp.ExibirDados();	break;
		case 2: cc.DadosColaboradorComissionado(); cc.ExibirDados(); break;
		case 3: cpp.DadosColaboradorProducao(); cpp.ExibirDados(); break;
		case 0: System.out.println("----Encerrando o programa!!----"); break;
		default: System.out.println("OPÇÃO INVALIDA!!!");
		}
		}while(op!=0);
	}

}

#Colaboradores 
package colaborador;

import java.util.Scanner;

public class Colaborador {
	
	//SCANNER
	Scanner teclado = new Scanner(System.in);
	
	//VARIAVEIS
	private String nome;
	private int matricula;
	private double salarioBase = 2000;
	
	//RECEBER E ENVIAR OS DADOS RECEBIDOS PELAS VARIAVEIS PRIVADAS
	public String getNome() {
		return nome;
	}

	public void setNome(String nome) {
		this.nome = nome;
	}

	public int getMatricula() {
		return matricula;
	}

	public void setMatricula(int matricula) {
		this.matricula = matricula;
	}

	public double getSalarioBase() {
		return salarioBase;
	}

	public void setSalarioBase(double salarioBase) {
		this.salarioBase = salarioBase;
	}
	
	//FUNCOES
	public void Dados() {
		System.out.println("Digite o nome do colaborador: ");
		nome = teclado.nextLine();
		System.out.println("Digite a matrícula: ");
		matricula = teclado.nextInt();
	}
	
	public double CalcularSalarioFinal() {
		return salarioBase = 2000;
		
	}
	
	public void ExibirDados() {
		System.out.println("\n--- DADOS DO COLABORADOR ---");
		System.out.println("Nome:      " + nome);
		System.out.println("Matrícula: " + matricula);
		System.out.printf("Salário:   R$ %.2f\n", CalcularSalarioFinal());
		System.out.println("----------------------------\n");
		teclado.nextLine();
		teclado.nextLine();
	}
}

#
package colaborador;

public class ColaboradorPadrao extends Colaborador {
	//PODE DEIXAR VAZIO, POIS HERDOU AS MESMAS FUNÇÕES DE COLABORADOR
}

#
package colaborador;

public class ColaboradorComissionado extends Colaborador {
	//VV-> VALOR VENDA / PC -> PERCENTUAL COMISSAO
	private double vv;
	private double pc;
	
	//RECEBER E ENVIAR OS DADOS RECEBIDOS PELAS VARIAVEIS PRIVADAS
	public double getVv() {
		return vv;
	}
	public void setVv(int vv) {
		this.vv = vv;
	}
	public double getPc() {
		return pc;
	}
	public void setPc(double pc) {
		this.pc = pc;
	}
	
	//FUNÇÕES
	
	public void DadosColaboradorComissionado() {
		super.Dados();
		System.out.println("Digite o valor em vendas: ");
		vv = teclado.nextDouble();
		System.out.println("Digite o percentual da comissão: ");
		pc = teclado.nextDouble();
		
	}
	@Override //FORÇA O PROGRAMA A RESCREVER A FUNÇÃO INICIAL COM A NOVA FUNÇÃO
	public double CalcularSalarioFinal() {
		return getSalarioBase() + (vv * (pc / 100.0));
	}
	
}

#

package colaborador;

public class ColaboradorProducao extends Colaborador {
	//DEFININDO AS NOVAS VARIÁVEIS / QP-> QUANTIDADE DE PEÇAS / VP-> VALOR POR PEÇA
	private int qp;
	private double vp;

	//RECEBER E ENVIAR OS DADOS RECEBIDOS PELAS VARIAVEIS PRIVADAS
	public int getQp() {
		return qp;
	}

	public void setQp(int qp) {
		this.qp = qp;
	}

	public double getVp() {
		return vp;
	}

	public void setVp(double vp) {
		this.vp = vp;
	}

	//FUNÇÕES 
	
	public void DadosColaboradorProducao() {
		super.Dados();
		System.out.println("Digite o número de peças vendidas pelo colaborador: ");
		qp = teclado.nextInt();
		System.out.println("DIgite o valor por peça: ");
		vp = teclado.nextDouble();
	}

	public double Produtividade() {
		return qp * vp;
	}

	@Override
	public double CalcularSalarioFinal() {
		return getSalarioBase() + Produtividade();
	}
}

