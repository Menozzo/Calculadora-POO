# Calculadora-POO

#include <iostream>

using namespace std;

class Operacao {
    
    protected:  // Changed from private to protected
        double valor1;
        double valor2;
    
    public:
        Operacao(double valor1, double valor2) {
            this->valor1 = valor1;
            this->valor2 = valor2;
        }
        
        void setOperacao(double valor1, double valor2) {
            this->valor1 = valor1;
            this->valor2 = valor2;
        }
        
        virtual double calcular() const = 0;  // Add pure virtual method
        
        virtual void exibir() const {
            cout << "Operação genérica" << endl;
        }
};

class Adicao : public Operacao {
    public:
        Adicao(double valor1 = 0, double valor2 = 0) : Operacao(valor1, valor2) {}
        
        double calcular() const override {
            return valor1 + valor2;
        }
        
        void exibir() const override {
            cout << valor1 << " + " << valor2 << " = " << calcular() << endl;
        }
};

class Subtracao : public Operacao {
    public:
        Subtracao(double valor1 = 0, double valor2 = 0) : Operacao(valor1, valor2) {}
        
        double calcular() const override {
            return valor1 - valor2;
        }
        
        void exibir() const override {
            cout << valor1 << " - " << valor2 << " = " << calcular() << endl;
        }
};

class Multiplicacao : public Operacao {
    public:
        Multiplicacao(double valor1 = 0, double valor2 = 0) : Operacao(valor1, valor2) {}
        
        double calcular() const override {
            return valor1 * valor2;
        }
        
        void exibir() const override {
            cout << valor1 << " × " << valor2 << " = " << calcular() << endl;
        }
};

class Divisao : public Operacao {
    public:
        Divisao(double valor1 = 0, double valor2 = 1) : Operacao(valor1, valor2) {}
        
        double calcular() const override {
            if (valor2 == 0) {
                throw runtime_error("Erro: Divisão por zero!");
            }
            return valor1 / valor2;
        }
        
        void exibir() const override {
            try {
                cout << valor1 << " ÷ " << valor2 << " = " << calcular() << endl;
            } catch (const runtime_error& e) {
                cout << e.what() << endl;
            }
        }
};

int main() {
    cout << "=== TESTE DA CALCULADORA ===\n" << endl;
    
    Adicao soma(10, 5);
    soma.exibir();
    
    Subtracao sub(10, 5);
    sub.exibir();
    
    Multiplicacao mult(10, 5);
    mult.exibir();
    
    Divisao div(10, 5);
    div.exibir();
    
    return 0;
}
