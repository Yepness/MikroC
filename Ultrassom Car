
// Nomes: Pablo Vinicius Oliveira 

#include "HC-SR04.h" // Inclui a Biblioteca do Sensor de Ultrassom
//Declaração de Nomes dos Bits dos Ports
//Exemplo: sbit BOTAO at PORTA.b0;
// SBITS LCD:
sbit LCD_RS at RB4_bit;
sbit LCD_EN at RB5_bit;
sbit LCD_D7 at RB3_bit;
sbit LCD_D6 at RB2_bit;
sbit LCD_D5 at RB1_bit;
sbit LCD_D4 at RB0_bit;
sbit LCD_RS_Direction at TRISB4_bit;
sbit LCD_EN_Direction at TRISB5_bit;
sbit LCD_D7_Direction at TRISB3_bit;
sbit LCD_D6_Direction at TRISB2_bit;
sbit LCD_D5_Direction at TRISB1_bit;
sbit LCD_D4_Direction at TRISB0_bit;
// SBITS Motores:
sbit M1A at PORTD.B4;
sbit M1B at PORTD.B5;
sbit M2A at PORTD.B6;
sbit M2B at PORTD.B7;
// SBITS Ultrassom:
sbit HCSR04_Trigger at PORTD.B0; //RD0_Bit
sbit HCSR04_Echo at PORTD.B1; //RD1_Bit
sbit HCSR04_Trigger_Direction at TRISD.B0; //TRISD0_Bit
sbit HCSR04_Echo_Direction at TRISD.B1; //TRISD1_Bit
// SBITS Leds:
sbit VERDE at PORTC.B1;
sbit VERMELHO at PORTC.B0;
// Variáveis globais
const float factor = 1.5; // 48MHz
// Void Motores:
void Tras()
{
M1A = 1;
M1B = 0;
M2A = 1;
M2B = 0;
}
void Frente()
{
M1A = 0;
M1B = 1;
M2A = 0;
M2B = 1;
}
void Parar()
{
M1A = 1;
M1B = 1;
M2A = 0;
M2B = 0;
}
void Esquerda()
{
M1A = 1;
M1B = 0;
M2A = 0;
M2B = 0;
}

// PROGRAMA PRINCIPAL

void main (void)
{
int distancia;
float temp;
char txt[7];
// Registradores de Configuração:
 ADCON1 = 0b00001111;
 CMCON = 0b00000111;
// Configuração dos PORTS de Entrada e Saida
// 0 -> configura o BIT como Saída
// 1 -> configura o BIT como Entrada
// Exemplo: TRISA = 0b00001111;
TRISC = 0b00000000;
TRISB = 0b00000000;
TRISD = 0b00000000;
HCSR04_Init(3); // Inicia as funções do Sensor de Ultrassom
LCD_Init();
LCD_Cmd(_LCD_CURSOR_OFF);
M1A = 0;
M1B = 0;
M2A = 0;
M2B = 0;

//Inicio do Loop principal

 while (1)
 {
 temp = HCSR04_Read(); // lê a distancia em milimetros
 distancia = temp/10; // distancia em cm
 inttostr(distancia,txt);
 ltrim(txt);
 LCD_Out(1,1,"Distancia: cm");
 LCD_Out(1,11,txt);
 delay_ms(300);
 LCD_Out(2,6," ");
 if(distancia > 20)
 {
 VERDE = 1;
 Frente();
 LCD_Out(2,2,"Frente ");
 }
 
 else
 {
 VERDE = 0;
 VERMELHO = 1;
 Parar();
 LCD_Out(2,2," Parar ");
 delay_ms(2000);
 Tras();
 LCD_Out(2,2,"Pra Tras ");
 delay_ms(2000);
 Esquerda();
 LCD_Out(2,2," Esquerda ");
 delay_ms(2000);
 Frente();
 VERDE = 1;
 VERMELHO = 0;
 LCD_Out(2,2," Frente ");
 }
 }//fecha o while
}//fecha o void main
