# calculadora-imc
import 'dart:io';

class Pessoa {
  String nome;
  double peso;
  double altura;

  Pessoa(this.nome, this.peso, this.altura);
}

void main() {
  try {
    print("Digite o nome da pessoa:");
    String nome = stdin.readLineSync();
    
    print("Digite o peso (em kg):");
    double peso = double.parse(stdin.readLineSync());

    print("Digite a altura (em metros):");
    double altura = double.parse(stdin.readLineSync());

    Pessoa pessoa = Pessoa(nome, peso, altura);

    double imc = calcularIMC(pessoa);
    print("O IMC de ${pessoa.nome} é: $imc");
  } catch (e) {
    print("Erro: $e");
  }
}

double calcularIMC(Pessoa pessoa) {
  if (pessoa.altura <= 0 || pessoa.peso <= 0) {
    throw ArgumentError("Altura e peso devem ser maiores que zero.");
  }
  
  double imc = pessoa.peso / (pessoa.altura * pessoa.altura);
  return imc;
}

import 'package:flutter_test/flutter_test.dart';

void main() {
  test('Teste de cálculo de IMC', () {
    Pessoa pessoa = Pessoa("João", 70, 1.75);
    expect(calcularIMC(pessoa), closeTo(22.86, 0.01)); // O IMC deve ser aproximadamente 22.86
  });

  test('Teste de exceção com altura zero', () {
    Pessoa pessoa = Pessoa("Maria", 55, 0);
    expect(() => calcularIMC(pessoa), throwsArgumentError);
  });

  test('Teste de exceção com peso zero', () {
    Pessoa pessoa = Pessoa("Pedro", 0, 1.80);
    expect(() => calcularIMC(pessoa), throwsArgumentError);
  });
}



